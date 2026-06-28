Database Design

Canonical data model for ExamVerseOS

⸻

Philosophy

ExamVerseOS is not designed around PDFs.

It is designed around knowledge.

Every examination, topic, question, and learner is represented as structured data with explicit relationships.

The database must be:

* Exam agnostic
* Modular
* Extensible
* Versioned
* Searchable
* AI-ready

⸻

Core Entities

Exam
│
├── Notification
├── Syllabus
├── Subject
│      ├── Topic
│      │      ├── Subtopic
│      │      │      ├── PYQ
│      │      │      ├── Note
│      │      │      ├── Quiz
│      │      │      └── Resource
│      │
│      └── Weightage
│
├── Study Plan
├── Revision
├── Progress
└── Analytics

⸻

Primary Tables

Exam

Represents a single examination.

Fields

* id
* code
* name
* organization
* country
* level
* category
* description
* official_website
* status
* created_at
* updated_at

Examples

* UPSC CSE
* SSC CGL
* JEE Advanced
* GATE CSE

⸻

Notification

Stores official notifications.

Fields

* id
* exam_id
* title
* year
* pdf_url
* release_date
* version
* checksum

⸻

Syllabus

Stores syllabus versions.

Fields

* id
* exam_id
* version
* effective_from
* source
* raw_text
* structured_json

⸻

Subject

Examples

* History
* Polity
* Physics
* Mathematics

Fields

* id
* exam_id
* name
* sequence

⸻

Topic

Examples

* Fundamental Rights
* Mughal Empire
* Electromagnetism

Fields

* id
* subject_id
* parent_topic
* title
* description
* difficulty

⸻

Subtopic

Examples

* Article 14
* Article 19
* Directive Principles

Fields

* id
* topic_id
* title
* description

⸻

Previous Year Question (PYQ)

Fields

* id
* exam_id
* year
* paper
* subject_id
* topic_id
* question_text
* answer_key
* explanation
* marks
* difficulty

⸻

Book

Fields

* id
* title
* author
* publisher
* edition
* isbn

⸻

Resource

Fields

* id
* topic_id
* type
* title
* url
* source

⸻

Note

Fields

* id
* topic_id
* created_by
* content
* version

⸻

Quiz

Fields

* id
* topic_id
* difficulty
* questions

⸻

User Domain

User

Fields

* id
* name
* email
* role
* avatar
* created_at

⸻

Study Plan

Fields

* id
* user_id
* exam_id
* target_date
* daily_hours
* strategy

⸻

Progress

Fields

* id
* user_id
* topic_id
* status
* mastery_score
* updated_at

Status

* Not Started
* Learning
* Revising
* Mastered

⸻

Revision

Fields

* id
* user_id
* topic_id
* next_revision
* interval
* confidence

⸻

Analytics

Tracks learning insights.

Examples

* Accuracy
* Time studied
* Weak topics
* Strong topics
* Revision streak
* Completion %

⸻

AI Domain

Prompt History

Stores AI interactions.

Fields

* id
* user_id
* prompt
* response
* model
* timestamp

⸻

Embeddings

Semantic search vectors.

Fields

* id
* entity_type
* entity_id
* embedding

⸻

Relationships

Exam
 ├── Subjects
 │      ├── Topics
 │      │      ├── Subtopics
 │      │      ├── PYQs
 │      │      ├── Notes
 │      │      ├── Resources
 │      │      └── Quizzes
 │
 ├── Notifications
 ├── Syllabus
 │
 └── Users
        ├── Study Plans
        ├── Progress
        ├── Revisions
        └── Analytics

⸻

Design Principles

Normalized

Avoid duplicated information.

⸻

Versioned

Official information must never be overwritten.

Every syllabus and notification should retain history.

⸻

Searchable

Every entity should support full-text and semantic search.

⸻

AI Ready

The database should support Retrieval-Augmented Generation (RAG) and future AI workflows.

⸻

Extensible

Adding a new examination should require data insertion rather than schema redesign.

⸻

Future Extensions

The model is designed to support:

* Coaching institutes
* Universities
* Professional certifications
* Corporate training
* Language learning
* Research knowledge bases

without changing the core schema.

⸻

Database Principle

Store knowledge, not documents.

Every table should represent a meaningful concept in the learning ecosystem, making ExamVerseOS a reusable knowledge platform rather than a collection of files.