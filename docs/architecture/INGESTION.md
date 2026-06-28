Ingestion System Design

The engine that converts official exam information into structured knowledge

⸻

Purpose

The ingestion system is responsible for collecting, cleaning, validating, and structuring all official examination data.

It is the only trusted entry point for knowledge into ExamVerseOS.

⸻

Core Principle

If data does not pass through ingestion, it does not exist in ExamVerseOS.

No manual database edits for core knowledge.

Everything flows through this pipeline.

⸻

High-Level Pipeline

Official Sources
      │
      ▼
Fetcher Layer
      │
      ▼
Raw Storage (PDF / HTML / Docs)
      │
      ▼
Parser Engine
      │
      ▼
Structured Extraction
      │
      ▼
Validator Layer
      │
      ▼
Normalizer
      │
      ▼
Knowledge Graph Builder
      │
      ▼
Database (ExamVerse Core)

⸻

System Components

1. Source Manager

Responsible for managing official sources.

Responsibilities

* Maintain list of official exam websites
* Track syllabus PDFs
* Track notifications
* Detect updates
* Schedule re-fetch cycles

Example Sources

* UPSC.gov.in
* SSC.nic.in
* NTA portals
* State PSC sites

⸻

2. Fetcher Layer

Responsible for downloading raw content.

Responsibilities

* HTTP requests
* Browser automation (if needed)
* PDF downloads
* HTML scraping
* Retry handling
* Rate limiting

Tools

* Playwright
* Axios / Fetch
* Puppeteer (optional fallback)

⸻

3. Raw Storage

Stores unprocessed data.

Structure

/raw
   /upsc
      /2026
         syllabus.pdf
         notification.html

Rules

* Never modify raw files
* Store versioned copies
* Keep checksum for integrity

⸻

4. Parser Engine

Converts raw content into structured text.

Responsibilities

* PDF text extraction
* Table extraction
* HTML parsing
* OCR for scanned documents
* Noise removal

Tools

* pdfplumber
* PyMuPDF
* Tesseract OCR

⸻

5. Structured Extractor

Transforms text into schema-based data.

Output Examples

* Subjects
* Topics
* Subtopics
* Dates
* Eligibility criteria
* Exam patterns

⸻

6. Validator Layer

Ensures correctness.

Responsibilities

* Check missing fields
* Detect malformed syllabus structures
* Validate against existing schema
* Flag inconsistencies

⸻

7. Normalizer

Standardizes data across exams.

Responsibilities

* Unify naming conventions
* Merge duplicate topics
* Standardize subject structure
* Map synonyms (e.g., “Polity” = “Indian Constitution”)

⸻

8. Knowledge Graph Builder

Creates relationships between entities.

Examples

* Topic → PYQ
* Topic → Subtopic
* Subject → Topic
* Topic → Current Affairs link

⸻

9. Database Writer

Final step of ingestion.

Responsibilities

* Insert structured data
* Version control entries
* Maintain audit logs
* Prevent overwrites

⸻

Data Flow Example (UPSC)

UPSC Syllabus PDF
        ↓
Fetcher downloads file
        ↓
Parser extracts text
        ↓
Extractor identifies:
    - GS1, GS2, GS3, GS4
        ↓
Normalizer standardizes structure
        ↓
Graph builder links topics
        ↓
Database stores versioned syllabus

⸻

Update Detection

System must detect changes in official sources.

Triggers

* PDF checksum change
* Page content change
* New notification release

Action

* Create new version
* Do not overwrite existing data

⸻

Error Handling

* Failed fetch → retry queue
* Parse failure → manual review queue
* Validation failure → rejection log
* Partial extraction → flagged dataset

⸻

Output Format

All ingestion output must conform to:

* Exam schema (ExamVerse DB)
* Versioned structure
* Graph-compatible format
* AI-ready embeddings

⸻

Scalability Design

System should support:

* Multiple exams simultaneously
* Parallel ingestion pipelines
* Scheduled updates
* Distributed processing in future

⸻

Security Considerations

* Only fetch from official/public sources
* Respect rate limits
* Do not bypass authentication systems
* Log all ingestion actions

⸻

Future Enhancements

* AI-assisted syllabus structuring
* Auto-topic detection from PYQs
* Current affairs auto-linking
* Multi-language support
* Human-in-the-loop validation dashboard

⸻

Key Principle

Raw data is noise. Structured knowledge is power.

The ingestion system is what transforms ExamVerseOS from a collection of documents into a living knowledge system.