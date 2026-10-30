# Packaged Commodities Compliance Inspector

A student prototype for the Smart India Hackathon problem of checking packaged-commodity labels against the Legal Metrology (Packaged Commodities) Rules, 2011. The system is designed to extract label information from uploaded images and present a structured compliance assessment.

> **Project status:** Prototype / decision-support tool. Results should be reviewed against current applicable law by a qualified person. OCR and automated extraction can make mistakes; do not treat the output as a legally binding determination.

## Core Workflow

1. Upload a package-label image through the web interface.
2. The FastAPI backend validates and preprocesses the image.
3. OCR extracts visible text from the label.
4. Extraction logic organizes relevant declarations into structured attributes.
5. A deterministic rule engine evaluates applicable declaration checks.
6. The interface presents extracted information and the inspection outcome.
7. Inspection history is supported by the backend database.

## Tech Stack

### Backend
- Python
- FastAPI and Uvicorn
- RapidOCR ONNX Runtime
- OpenCV, Pillow, and NumPy for image preprocessing
- SQLAlchemy with SQLite persistence
- Pydantic and python-dotenv
- Pytest and HTTPX for testing

### Frontend
- React 18
- Vite
- Tailwind CSS
- Lucide React icons

## Repository Structure

| Path | Purpose |
| --- | --- |
| `backend/app/api/` | API routes for inspection, OCR/extraction, health, uploads, and history |
| `backend/app/ocr/` | OCR service and image preprocessing |
| `backend/app/extractor/` | Structured attribute extraction |
| `backend/app/rules/` | Compliance rules and evaluation logic |
| `backend/app/inspection/` | Inspection processing and result aggregation |
| `backend/app/db/` | SQLAlchemy models, sessions, and database operations |
| `frontend/` | React web interface |
| `samples/` | Sample files for development and testing |

## Run Locally

### 1. Start the backend

Use Python 3.10+ (confirm the project's supported version if your environment differs).

```bash
cd backend
python -m venv .venv
```

Activate the environment:

- Windows: `.venv\\Scripts\\activate`
- macOS/Linux: `source .venv/bin/activate`

Install dependencies and start the API:

```bash
pip install -r requirements.txt
uvicorn app.main:app --reload
```

If the ASGI module path differs in your local checkout, inspect the backend entry-point file and use its actual module path.

### 2. Start the frontend

In a second terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the local Vite URL printed in the terminal. The frontend may require an API base URL configuration matching the backend address; check the current frontend configuration before testing uploads.

## Configuration and Security

- Use `backend/.env.example` as a guide for local configuration.
- Never commit real API keys, credentials, or populated `.env` files.
- Keep upload validation and file-size limits enabled.
- Treat OCR output as untrusted input and handle unsupported/low-quality images explicitly.
- Verify that legal-rule interpretations and source references are current before relying on results.

## Recommended Demo

1. Open the application.
2. Upload a clear sample package-label image.
3. Review the extracted text and structured declarations.
4. Inspect the rule-by-rule result and any missing-information warnings.
5. Open inspection history and review a previous result.

Use sample data only, and explain the limitations of OCR and automated legal interpretation during demonstrations.

---

Developed as a student hackathon prototype for improving access to packaged-commodity label compliance checks.
