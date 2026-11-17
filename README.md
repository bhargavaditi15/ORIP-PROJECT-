# Open Research Intelligence Platform (ORIP)

> A local-first AI-powered research intelligence platform for
> discovering, retrieving, comparing, and organizing biomedical and
> scientific literature.

**Project status:** Early development --- local development environment
and initial dependencies configured.\
**Primary language:** Python 3.12\
**Initial architecture:** Modular monolith\
**Intended users:** Researchers, students, and scientific teams

------------------------------------------------------------------------

## 1. What is ORIP?

The Open Research Intelligence Platform (ORIP) is being developed to
help people work more effectively with scientific and biomedical
research literature.

Research information is distributed across large collections of papers,
reports, and other documents. Finding relevant publications, locating
supporting passages, comparing findings, and keeping track of evidence
can require substantial manual effort.

ORIP aims to bring these activities into one research workspace. It will
ingest research documents, extract and organize their content, make that
content searchable, and help users explore evidence with traceable links
back to the source documents.

The platform is being built incrementally. Each capability will be
implemented, tested, evaluated, and documented before the next
capability is added.

## 2. Why are we building it?

The goal is not simply to create a chatbot that summarizes papers. The
goal is to build a research workflow in which users can move from a
research question to relevant source material and organized evidence.

### Business problem

Researchers may need to:

-   Collect and organize papers from different sources.
-   Search for a concept even when authors use different wording.
-   Find the exact passage that supports a statement.
-   Compare methods, datasets, findings, and limitations across papers.
-   Identify related concepts and possible evidence gaps.
-   Keep reusable notes and evidence tables.

These tasks can involve switching between documents and tools, repeating
searches, and manually recording findings.

### ORIP's intended value

ORIP aims to reduce this friction by providing a single workflow:

1.  Create a research workspace or collection.
2.  Add permitted research documents.
3.  Extract text, metadata, and document structure.
4.  Search across the collection.
5.  Ask questions and retrieve relevant source passages.
6.  Review citations against the original documents.
7.  Compare findings and organize research notes.
8.  Explore relationships between concepts and publications.
9.  Export useful research outputs.

The platform should make evidence easier to find and inspect. It must
not present generated text as a substitute for the original scientific
source.

## 3. Intended capabilities

The following capabilities describe the planned product direction. They
are not all implemented yet.

  -----------------------------------------------------------------------
  Capability                          Intended use
  ----------------------------------- -----------------------------------
  Document ingestion                  Add PDF, DOCX, TXT, and HTML
                                      research documents

  Text and metadata extraction        Extract document text, titles,
                                      authors, sections, and other
                                      available metadata

  OCR                                 Process scanned documents when
                                      required

  Provenance tracking                 Preserve the source document and
                                      location of extracted content

  Document chunking                   Split long documents into useful,
                                      traceable passages

  Keyword search                      Find exact words and phrases

  Semantic search                     Find conceptually related passages

  Hybrid retrieval                    Combine keyword and semantic search

  Research Q&A                        Answer questions using retrieved
                                      source material

  Citation validation                 Check that cited passages support
                                      generated statements

  Evidence comparison                 Organize methods, findings,
                                      limitations, and other evidence
                                      across papers

  Research notes and export           Save and export organized research
                                      findings

  Knowledge graph                     Represent relationships between
                                      papers, concepts, methods, and
                                      findings

  Agent workflows                     Coordinate multi-step research
                                      tasks with reviewable outputs

  Evaluation and monitoring           Measure retrieval, extraction,
                                      citation, and system quality
  -----------------------------------------------------------------------

## 4. Business workflow

``` mermaid
flowchart TD
    A[Research question] --> B[Create research collection]
    B --> C[Add permitted research documents]
    C --> D[Extract text and metadata]
    D --> E[Preserve source provenance]
    E --> F[Chunk and index content]
    F --> G[Search and retrieve evidence]
    G --> H[Review source passages]
    H --> I[Compare findings]
    I --> J[Create research notes and evidence tables]
    J --> K[Export research outputs]
    G --> L[Explore concept relationships]
    L --> H
```

## 5. Safety and scope boundaries

ORIP is a **research assistance and literature exploration platform**.

It is not intended to be:

-   A medical diagnostic system.
-   A clinical decision-support system.
-   A medical device.
-   An autonomous clinical decision-maker.
-   A source of patient-specific treatment recommendations.

Generated answers must be presented with their supporting sources where
available. Users must be able to inspect the original documents and
verify important claims. Missing evidence, uncertain extraction, and
unsupported answers should be made visible rather than hidden.

Only documents that the user has the right to process should be added to
a collection. Local-first operation is a design goal, but actual privacy
and security properties must be verified as the system is implemented.

## 6. Technology direction

The technology choices below are the current proposed direction. They
may be adjusted when experiments demonstrate a better fit.

  -----------------------------------------------------------------------
  Area                    Planned technologies    Purpose
  ----------------------- ----------------------- -----------------------
  Language                Python 3.12             Main application
                                                  language

  API                     FastAPI, Uvicorn        Backend API

  Data validation         Pydantic,               Request validation and
                          pydantic-settings       configuration

  Database access         SQLAlchemy, Alembic     Persistence and schema
                                                  migrations

  Initial database        SQLite                  Simple local
                                                  development and early
                                                  persistence

  Document processing     PyMuPDF, python-docx,   Read PDF, DOCX, and
                          BeautifulSoup, lxml     HTML documents

  OCR                     Tesseract with          Text extraction from
                          pytesseract             scanned pages when
                                                  needed

  Data analysis           NumPy, Pandas, DuckDB   Data manipulation and
                                                  analysis when required

  Machine learning        scikit-learn, PyTorch   Classical ML and deep
                                                  learning experiments

  NLP and embeddings      Transformers, Sentence  Language models and
                          Transformers            text embeddings

  Vector retrieval        FAISS or Qdrant         Similarity search over
                                                  embedded passages

  Knowledge graphs        NetworkX initially      Graph representation
                                                  and algorithms

  API testing             Pytest, HTTPX           Automated tests

  Code quality            Ruff, Mypy              Linting, formatting,
                                                  and static type
                                                  checking

  Environment and         `.venv`, pip, uv        Isolated environment
  packages                                        and dependency
                                                  management

  Version control         Git and GitHub          Change history and
                                                  remote repository
  -----------------------------------------------------------------------

Not every technology will be installed at the beginning. Dependencies
will be introduced when their corresponding feature or learning phase
requires them. This keeps the environment manageable and gives each
dependency a clear purpose.

## 7. Development environment

### Prerequisites

-   Windows, macOS, or Linux development machine.
-   Visual Studio Code.
-   Python 3.12.
-   Git.
-   A terminal (Command Prompt or PowerShell on Windows).

### Current Windows setup

The initial local environment was created using Python 3.12.10.

From the project root, create the virtual environment with:

``` cmd
py -3.12 -m venv .venv
```

Activate it in Windows Command Prompt:

``` cmd
.venv\Scripts\activate.bat
```

Activate it in Windows PowerShell:

``` powershell
.\.venv\Scripts\Activate.ps1
```

Verify the active interpreter:

``` cmd
python --version
python -c "import sys; print(sys.executable)"
python -m pip --version
```

The interpreter path should point inside the project's `.venv`
directory.

### Install initial dependencies

With the virtual environment activated:

``` cmd
python -m pip install -r requirements.txt
```

Check installed packages and dependency consistency:

``` cmd
python -m pip list
python -m pip check
```

The `requirements.txt` file is the installation list for the current
dependency set. Future AI/ML libraries should be added when their
implementation phase begins, rather than installing the entire planned
stack at once.

## 8. Repository structure

The repository will grow as features are implemented. The intended
direction is:

``` text
ORIP-Project/
│
├── .venv/                    # Local virtual environment; never commit
├── .gitignore                # Files and folders Git should ignore
├── README.md                 # Project overview and setup instructions
├── requirements.txt          # Current Python dependencies
├── pyproject.toml            # Project and tool configuration (planned)
│
├── src/
│   └── orip/                 # Main application package (planned)
│       ├── api/              # API routes
│       ├── core/             # Configuration and shared foundations
│       ├── ingestion/        # Document intake
│       ├── extraction/       # Text and metadata extraction
│       ├── retrieval/        # Search and retrieval
│       ├── rag/              # Retrieval-augmented generation
│       ├── graph/            # Knowledge graph capabilities
│       └── services/         # Application services
│
├── tests/                    # Automated tests (planned)
├── docs/                     # Architecture and engineering documentation
├── learning-lab/             # Isolated experiments and learning exercises
└── scripts/                  # Development and maintenance scripts
```

This is a target structure, not a claim that all directories or modules
already exist.

## 9. Development approach

ORIP will be developed using the following cycle:

**Learn → Experiment → Understand → Integrate → Test → Document**

For each feature:

1.  Understand the user problem and business purpose.
2.  Learn the concepts and technologies required.
3.  Run a small experiment where appropriate.
4.  Design the smallest useful implementation.
5.  Implement incrementally.
6.  Add tests and verify actual behavior.
7.  Document decisions, limitations, and results.
8.  Update the project plan and progress record.

New frameworks should not be introduced just because they are popular.
Prefer the simplest approach that meets the requirement, and adopt a
framework when it provides a clear benefit.

## 10. Planned engineering phases

The broader learning and implementation roadmap is organized into twelve
phases:

1.  Python and software engineering foundations.
2.  Mathematics, statistics, SQL, and data engineering.
3.  Classical machine learning.
4.  Deep learning.
5.  NLP, computer vision, and document intelligence.
6.  Embeddings, vector databases, and semantic search.
7.  Generative AI, LLMs, and advanced RAG.
8.  Agentic AI and workflow orchestration.
9.  Knowledge graphs and Graph RAG.
10. Backend engineering and product integration.
11. MLOps, LLMOps, DevOps, and deployment.
12. System design, security, optimization, and production readiness.

The phases have dependencies and will be approached progressively. The
project will not attempt to implement all twelve phases at once.

## 11. Git workflow

Use Git to record meaningful, reviewable changes.

Check the current state:

``` cmd
git status
```

Stage selected files:

``` cmd
git add README.md requirements.txt .gitignore
```

Commit a completed change:

``` cmd
git commit -m "docs: add ORIP project README"
```

Review recent history:

``` cmd
git log --oneline
```

Push committed changes to the configured GitHub remote:

``` cmd
git push
```

Do not commit:

-   `.venv/` or other virtual environments.
-   `.env` files or credentials.
-   API keys, passwords, tokens, or private certificates.
-   Local databases or temporary data unless explicitly intended.
-   Research documents unless their licensing and sharing permissions
    allow it.

Never put secrets in source code or Git history. If a secret is
committed accidentally, removing the file in a later commit does not
erase it from history; rotate the exposed secret and follow an
appropriate history-cleanup process.

## 12. Quality and acceptance principles

A feature is not complete merely because code has been written.

Before marking a feature complete, record appropriate evidence, such as:

-   A successful test run.
-   A verified API request and response.
-   A sample document processed correctly.
-   Extraction output checked against the source.
-   Retrieval results reviewed for relevance.
-   Citations checked against original passages.
-   Known limitations and failure cases documented.

Useful future quality measures include:

-   Document extraction completeness.
-   Search and retrieval relevance.
-   Citation support and correctness.
-   Processing reliability and recovery behavior.
-   Reproducibility of research workflows.
-   Time required to locate and verify relevant evidence.

Metrics and acceptance thresholds will be defined as the corresponding
features are designed and evaluated.

## 13. Current project status

This README describes the project direction and setup. It does not imply
that all planned capabilities have been implemented.

  Area                                    Status
  --------------------------------------- --------------------------------------------
  Product purpose and business workflow   Defined
  Initial Python 3.12 environment         Set up locally
  Virtual environment                     Created and activated locally
  Initial dependency list                 Prepared and installed locally
  Git identity                            Configuration in progress / verify locally
  Local Git repository                    To be verified
  GitHub remote and first push            To be verified
  Application implementation              Not yet started / not yet verified

Update this table as milestones are completed. Only mark a milestone
complete after checking the actual result.

## 14. Project continuity

This repository is intended to be the single source of truth for ORIP's
implementation and engineering decisions.

At the start of each development session:

1.  Read this README and the current master project plan.
2.  Review the latest progress and next milestone.
3.  Check the current Git status and recent commits.
4.  Resume from the last verified step.
5.  Record important decisions and implementation outcomes.

Do not claim that a feature, test, deployment, or milestone is complete
without verification.

------------------------------------------------------------------------

**ORIP in one sentence:** A local-first research intelligence platform
that helps researchers move from scientific questions to discoverable,
traceable, and organized evidence.
