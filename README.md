# gemini-curl-notebook
# Getting Started with the Gemini API on Agent Platform

## 🎯 Purpose & Core Objective
The primary purpose of this project is to learn how to interact directly with Google Cloud's **Gemini 3.5 Flash** model at the infrastructure/HTTP level using cURL and REST API endpoints, without relying on higher-level SDK wrappers. 

By executing raw HTTP requests, this lab demonstrates:
* How authentication tokens (`gcloud auth print-access-token`) are passed to Google Cloud service endpoints.
* How structured prompts, multimodal payloads (images/videos), and tool declarations (like Google Search Grounding) are serialized into JSON requests.
* How to enforce structured, schema-validated responses (e.g., forcing JSON output) for production app integration.

---

## 🛠️ Lab Tasks & Learning Objectives

### Task 1: Open Notebook in Agent Platform Workbench
* **Action:** Navigated to **Agent Platform > Notebooks > Workbench** in the Google Cloud Console.
* **Purpose:** Enabled core platform services (`Agent Platform API`, `Notebooks API`, `Compute Engine API`) and booted up a JupyterLab compute instance (`workbench-notebook`) on Google Cloud infrastructure.

### Task 2: Environment Setup
* **Action:** Selected the **Python 3 (Local)** kernel environment and configured shell variables.
* **Purpose:** Initialized environmental variables (`PROJECT_ID`, `LOCATION`, `API_ENDPOINT`) and set up standard bearer token authentication (`Authorization: Bearer $(gcloud auth print-access-token)`) to authorize REST API calls.

### Task 3: Text Generation & Structured Outputs (Gemini 3.5 Flash)
* **Action:** Executed `curl -X POST` requests targeting the `gemini-3.5-flash:generateContent` endpoint.
* **Purpose:** Passed text prompts in JSON payloads, configured response parameters (`response_mime_type: application/json` with a defined schema), and used the `jq` CLI tool to parse and filter JSON outputs.

### Task 4: Multimodal Inputs & Tool Grounding
* **Action:** Sent multimodal cURL payloads containing base64-encoded image data, Google Cloud Storage (`gs://`) paths, and Google Search tools.
* **Purpose:** Tested Gemini's vision capability to extract insights from raw images and enabled native **Google Search Grounding** to let the model fetch live, up-to-date web information when needed.

---

## 📂 Repository Contents

| File | Description |
| :--- | :--- |
| `intro_gemini_curl.ipynb` | Complete Jupyter Notebook containing all cURL API calls and execution outputs. |
| `response.json` | Output response file captured from model REST calls. |
| `image.jpg` | Sample multimodal image file used for vision processing. |

---

## 🚀 How to Run Locally / In Google Cloud

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/gemini-api-agent-platform.git](https://github.com/YOUR_USERNAME/gemini-api-agent-platform.git)
   cd gemini-api-agent-platform
	1.	Prerequisites:
⚬	Active Google Cloud Project with the Agent Platform API enabled.
⚬	Google Cloud CLI (gcloud) installed and authenticated.
⚬	jq utility installed for parsing JSON responses.
	2.	Set environment variables:
export PROJECT_ID="YOUR_PROJECT_ID"
export LOCATION="us-central1"
export API_ENDPOINT="${LOCATION}-aiplatform.googleapis.com"

	3.	Execute Sample REST Call:
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  "https://${API_ENDPOINT}/v1/projects/${PROJECT_ID}/locations/${LOCATION}/publishers/google/models/gemini-3.5-flash:generateContent" \
  -d '{
    "contents": {
      "role": "user",
      "parts": { "text": "Hello Gemini!" }
    }
  }'
