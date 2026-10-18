# DataFind — Big Data File Search Engine

A simple Flask web application for uploading and keyword-searching Excel, CSV, TXT, and Word documents. Designed as a beginner-friendly Big Data Framework project and deployable to Render.

## Features

- Upload one or more supported files.
- Extract and index text from Excel worksheets, CSV rows, text files, and Word paragraphs/tables.
- Case-insensitive keyword search.
- Show matching filenames, occurrence counts, and text previews.
- Simple responsive dashboard and index statistics.
- Clear the in-memory index.

## Supported formats

- `.xlsx` — Excel workbooks
- `.xls` — older Excel workbooks
- `.csv` — comma-separated values
- `.txt` — plain text
- `.docx` — Word documents

Legacy `.doc` files are not supported; save them as `.docx` first.

## Run locally

Python 3.10+ is recommended.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
python app.py
```

Open http://127.0.0.1:5000

## Deploy on Render

1. Create a GitHub repository and upload these project files.
2. Sign in to Render and choose **New + → Web Service**.
3. Connect the repository.
4. Render can use `render.yaml`, or enter:
   - Build command: `pip install -r requirements.txt`
   - Start command: `gunicorn app:app`
5. Deploy and open the generated `onrender.com` URL.

## Important notes

- The app currently keeps extracted document text in process memory. Uploaded files and the index are lost when the service restarts or redeploys, and separate service instances do not share an index.
- This starter app is best for demonstrations and small datasets. It is not a distributed search cluster such as Hadoop or Elasticsearch.
- Each request is limited to 25 MB total. The in-memory index is capped at 100 files to reduce accidental memory use.
- Do not upload sensitive or confidential documents to a public demo.
- For a production or genuinely large-scale version, use persistent object storage and a database/search index such as PostgreSQL full-text search, OpenSearch, or Elasticsearch.
