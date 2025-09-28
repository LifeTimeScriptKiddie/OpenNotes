---
dg-publish: true
---


# **uploader.py Breakdown**

  

Scans a local folder for supported files, uploads them to an Open WebUI knowledge base, and records successful uploads to prevent duplication.

---

## **1. Configuration and Setup**

|**Variable**|**Purpose**|
|---|---|
|DOCS_FOLDER|Directory containing uploadable files (UPLOAD_FOLDER_PATH from .env)|
|LOG_PATH|File where logs are written (upload.log)|
|RECORD_PATH|Tracks already-uploaded filenames (uploaded_files.txt)|

Logging is configured to write detailed upload activity to upload.log.

---

## **2.**  **SUPPORTED_EXTENSIONS**

```
(".pdf", ".md", ".docx", ".txt", ".html", ".csv", ".epub", ".jpg", ".jpeg", ".png", ".gif", ".webp")
```

Only files with these extensions are considered for upload.

---

## **3. Core Functions
  

### `list_knowledge_bases() -> List[Dict]`

- Retrieves all existing knowledge bases from Open WebUI.
    
- Uses GET /api/knowledge.
    

---

### `get_or_create_default_kb() -> Optional[str]`

- Returns the ID of the default knowledge base (DEFAULT_KB_NAME from .env)
    
- If it doesn’t exist, creates a new one with DEFAULT_KB_DESC.
    

---

### `upload_file(knowledge_id: str, filepath: str) -> Optional[Dict]`

|**Input**|**Path to local file**|
|---|---|
|Output|JSON response if successful, None if failed|

Handles upload of individual files using:

```
POST /api/knowledge/{knowledge_id}/documents
```

---

### **load_uploaded_file_list() -> set**

  

Reads uploaded_files.txt to avoid re-uploading already processed files.

---

### **save_uploaded_file(filepath: str)**

  

Appends uploaded filename to uploaded_files.txt.

---

### **sync_folder_to_knowledge(folder_path: str, knowledge_id: str)**

|**Input**|**Path to folder, target knowledge base ID**|
|---|---|
|Output|Upload summary via log messages|

Scans folder for new files not in uploaded_files.txt and uploads them sequentially. Records outcome for each file.

---

## **4. CLI Entrypoint**

```
if __name__ == "__main__":
```

1. Logs startup.
    
2. Gets (or creates) knowledge base.
    
3. Invokes sync_folder_to_knowledge.
    
4. Logs final status.
    

---

## **Summary Table**

|**Function**|**Role**|
|---|---|
|list_knowledge_bases()|Query all existing KBs|
|get_or_create_default_kb()|Fetch or create default KB|
|upload_file()|Upload a single document|
|load_uploaded_file_list()|Read uploaded file record|
|save_uploaded_file()|Log successful upload|
|sync_folder_to_knowledge()|Bulk upload and sync|
