# AI Career Path Advisor — Architecture & Build Plan

**Goal:** Build an AWS-powered system that ingests a student resume, extracts skills, matches career paths based on market demand, calculates skill gaps, and returns a personalized learning roadmap plus a visual dashboard.

---

## 1) High-level Architecture (ASCII)

```
[ User ]
   │
   │ Upload resume (web UI / S3 direct)
   ▼
[ S3 - resumes bucket ]
   │  └── raw files, access logs
   │
   ▼  (S3 event)
[ Lambda - resume-trigger ]
   │  └─ converts DOCX/PDF -> text
   │  └─ calls Amazon Comprehend (DetectEntities/KeyPhrases)
   │
   ▼
[ Comprehend ] ---> Extracted skills & entities
   │
   ▼
[ Lambda - postprocess ]
   │  └─ normalize skills (mapping, synonyms)
   │  └─ store user profile in DynamoDB (user_id, skills, resume_meta)
   │
   ▼
[ SageMaker ] <--- Job/Course/Market datasets from S3
   │  └─ clustering + classification models
   │  └─ inference endpoint for career-path suggestions
   │
   ▼
[ Lambda - orchestrator ]
   │  └─ call SageMaker endpoint for recommendations
   │  └─ compute skill-gap (required_skills - user_skills)
   │  └─ map missing skills to courses (from Course DB)
   │  └─ write roadmap JSON to DynamoDB
   │
   ▼
[ DynamoDB ]  // user profiles, roadmaps, history
   │
   ▼
[ QuickSight ] ← dataset connectors (DynamoDB / S3)
   │  └─ dashboards: skill-gap, career suggestions, progress
   │
   ▼
[ Optional Frontend ] - S3/Amplify
   └─ UI for uploading, viewing dashboard, marking course complete

Background pipelines:
- EventBridge (scheduled) → Lambda → fetch market/job postings → S3
- Glue jobs (optional) → ETL for job/course datasets → S3
```

---

## 2) Components & Responsibilities

- **S3**

  - `ai-career-resumes` – raw resumes
  - `ai-career-data` – job listings, course metadata, model artifacts
  - lifecycle rules: move raw > Glacier after 90 days

- **Lambda functions**

  - `resume_processor` (triggered by S3  PutObject)
  - `text_normalizer` (skill normalization)
  - `orchestrator` (aggregates results, calls SageMaker)
  - `market_fetcher` (scheduled by EventBridge)

- **Amazon Comprehend**

  - Use DetectKeyPhrases / DetectEntities to pull skills, roles, education
  - Optional: custom entity recognizer if you train for domain-specific skills

- **SageMaker**

  - Training notebooks: feature engineering, clustering (KMeans/DBSCAN), classification (XGBoost / RandomForest)
  - Deploy endpoint for online inference
  - Store model artifacts in S3

- **DynamoDB** (single-table recommended)

  - Partition key: `user_id`
  - Attributes: `skills[]`, `career_suggestions[]`, `roadmap{steps}`, `last_updated`

- **QuickSight**

  - Datasets from DynamoDB/S3
  - Dashboards: Skill Radar, Career Match Scores, Course Recommendations, Progress Tracker

- **EventBridge / Scheduler**

  - `market_fetcher` runs daily/weekly to refresh job trend data

- **Security & IAM**

  - Least-privilege IAM roles for Lambda and SageMaker (S3 read-only where applicable)
  - KMS to encrypt S3/DynamoDB at rest
  - Cognito (optional) for user authentication in frontend

---

## 3) Data Flow (step-by-step)

1. Student uploads resume via web form (or direct S3 upload). S3 triggers `resume_processor`.
2. `resume_processor` converts document → plain text (use `textract` or a Python library).
3. Lambda calls **Comprehend** to extract key phrases, entities, skill mentions.
4. Post-processed skills are normalized (lowercase, map synonyms) using a mapping table stored in S3 or DynamoDB.
5. Normalized profile stored in DynamoDB.
6. `orchestrator` queries latest job-market dataset (S3) and calls SageMaker endpoint with user skills vector.
7. SageMaker returns ranked career clusters & match scores.
8. `orchestrator` computes skill gap and matches missing skills to courses in course DB.
9. Roadmap stored in DynamoDB; user receives notification (SNS / email) if desired.
10. QuickSight picks up data to render dashboard.

---

## 4) Data Schemas & Examples

**Resume profile (DynamoDB JSON sample)**

```json
{
  "user_id": "u123",
  "name": "Maanasa K",
  "skills": ["python","sql","pandas","machine learning"],
  "education": "BTech AI&ML",
  "career_suggestions": [{"title":"Data Analyst","score":0.92}],
  "roadmap": {"missing_skills":["tableau"],"courses":[{"title":"Tableau Essentials","url":"..."}]}
}
```

**Job listing (Row)**

- `job_id`, `title`, `skills[]`, `location`, `posted_date`, `description`

**Course catalog**

- `course_id`, `title`, `provider`, `skills_taught[]`, `length_hours`, `url`

---

## 5) ML Approach (SageMaker)

- **Features**

  - Binary skill vector for a curated skill vocabulary
  - Experience years, education level, certifications
  - Market-demand score (from job datasets)

- **Modeling**

  - **Clustering** (KMeans / Hierarchical) to identify career clusters
  - **Classifier or ranking model** (XGBoost / logistic regression) to produce match score
  - Evaluate using labeled examples (map real job titles to profiles) or synthetic labels

- **Training workflow**

  - Use SageMaker notebooks to preprocess data (Glue/Spark optional)
  - Train locally on smaller data, use SageMaker for full run
  - Hyperparameter tuning via SageMaker Experiments if desired

---

## 6) Implementation Checklist (first MVP)

1. Create AWS account & S3 buckets
2. Prepare sample datasets (job listings + course catalog)
3. Build `resume_processor` Lambda (S3 trigger) + Comprehend integration
4. Store extracted skills into DynamoDB
5. Create a basic SageMaker notebook that clusters jobs and returns 3 career titles for a sample input
6. Create `orchestrator` Lambda to call SageMaker endpoint and store roadmap
7. QuickSight: connect to DynamoDB and make a simple dashboard
8. Build a minimal frontend (upload resume, view JSON response) and host on S3/Amplify

---

## 7) Security, Cost & Dev Tips

- **Security**: avoid storing PII in S3 publicly. Use KMS-managed encryption.
- **Costs**: turn off SageMaker endpoints when not in use; use small test instances for training; use Lambda free tier for many steps.
- **Testing**: build unit tests for Lambda, mock Comprehend responses locally; use sample resumes.

---

## 8) Timeline (Suggested MVP)\*\*

- **Week 1:** Data collection, S3 setup, resume upload pipeline, Comprehend integration
- **Week 2:** Normalize skills, DynamoDB storage, basic SageMaker prototyping (clustering)
- **Week 3:** Deploy SageMaker endpoint, orchestrator Lambda, generate roadmaps, QuickSight dashboard
- **Week 4:** Polishing, frontend, testing, documentation, video demo recording

---

## 9) Next Actions

- Provide sample job + course datasets (I can link sources & example CSVs)
- Generate Lambda starter code for resume processing (Python)
- Provide a SageMaker notebook starter for feature engineering & clustering
- Create QuickSight dataset templates or sample dashboard screenshots

---
