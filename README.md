This repository contains an n8n workflow (.json) that automates the process of scraping, enriching, and personalizing B2B leads. It extracts business data from Google Maps, finds contact information via the Snov.io API, and uses an LLM to generate custom icebreakers for outreach before dynamically exporting the data to Google Sheets.

🚀 Features
Automated Scraping: Extracts Google Maps data using Apify's actors.

Smart Routing: Uses conditional logic to split the workflow. Businesses without websites bypass the enrichment phases but are still securely captured and logged to prevent data loss.

Asynchronous Email Enrichment: Integrates with the Snov.io API (utilizing HTTP GET/POST requests and wait nodes) to discover and verify email addresses.

AI Personalization: Passes enriched lead data into a Basic LLM Chain powered by the NVIDIA Nemotron Chat Model to generate custom, context-aware icebreakers.

Dynamic Data Management: Automatically creates a new, timestamped worksheet in Google Sheets for each execution run, appends custom headers, and accurately maps all success and fallback data.

🛠 Prerequisites
To run this workflow, you will need an active instance of n8n and the following credentials configured within your environment:

Google Sheets Account: For triggering the workflow and appending the final dataset.

Apify API Key: For the Google Maps scraping node.

Snov.io API Credentials: API User ID and API Secret for lead enrichment (Header Auth).

NVIDIA API Key: For the Nemotron Chat Model.

📦 Installation & Setup
Clone this repository or download the .json workflow file directly.

Open your n8n workspace.

Navigate to Workflows and click Add Workflow.

Click the options menu (...) in the top right corner of the canvas and select Import from File.

Upload the .json file from this repository.

Once loaded, open the workflow and update the credential dropdowns for each respective node (Google Sheets, Apify, HTTP Requests for Snov.io, and the LLM).

Activate the workflow!

💡 Workflow Architecture
This pipeline is designed with strict fault tolerance for backend data processes. If Snov.io fails to find an email, or if a scraped business does not have a valid website URL, the workflow bypasses the AI generation step. Instead of dropping the item, it safely routes the raw Apify data into the final Google Sheet. This structural branching ensures maximum data extraction without crashing the workflow or misaligning columns.
