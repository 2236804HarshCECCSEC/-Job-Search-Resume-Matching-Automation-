LinkedIn Job Search: Auto-Match & Resume Scorer

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/464a5f61-300c-42de-8f92-ab1be22d2dd6" />

This automated workflow streamlines the job application process by fetching LinkedIn job listings, comparing them against your professional resume using an AI Agent, and notifying you of high-quality matches.

Workflow Overview
The process is divided into four main phases: Data Extraction, Job Discovery, AI Analysis (The Loop), and Notification.

1. Data Input & Extraction
Schedule Trigger: Sets the workflow to run at a specific interval (e.g., daily at 8 AM).
Google Drive (Download File): Fetches your latest resume (PDF/Docx) stored in a designated Google Drive folder.
Extract From PDF: Converts the resume file into raw text format so the AI can process your skills and experiences.
Google Sheets (Get Rows): Reads a configuration sheet containing your search parameters (Job Title, Location, Seniority Level, etc.).

2. LinkedIn Job Discovery
Create Search URL: A Code/Function node that takes your search parameters and constructs a valid LinkedIn search URL.
Fetch Jobs from LinkedIn: An HTTP Request node that pulls the search results page.
Extract Job Links: Parses the HTML to find individual job posting URLs.
Split Out: Converts the list of jobs into individual items to be processed one by one.

3. AI Scoring & Analysis (The Loop)
For every job found, the workflow enters a loop:
Wait Node: Implements a 10-second delay between fetches to mimic human behavior and avoid being flagged/blocked by LinkedIn.
Fetch Job Page: Downloads the full details of a specific job posting.
Parse & Modify Attributes: Extracts the job title, company name, and full description.
AI Agent (Powered by OpenAI/Gemini):
The Engine: Takes your resume text and the job description as input.
The Task: It rates the match from 0–100, summarizes why it’s a match, and can even draft a tailored cover letter.
Parse AI Output: Converts the AI's natural language response into structured JSON data.

4. Results & Reporting
Google Sheets (Append/Update): Logs every job checked into a spreadsheet, including the AI's "Match Score" and analysis.
Score Filter: A conditional node that only proceeds if the match score is above a certain threshold (e.g., >80).
Discord (Send Message): Sends an instant notification to your phone with the job link and the AI’s reasoning for any high-scoring roles.

🛠 Prerequisites
n8n Instance: Installed locally or via cloud.

API Keys:
OpenAI (for the AI Agent).
Google Cloud (for Drive and Sheets).
Discord Webhook (for notifications).

Google Sheet Template: A sheet formatted with columns for Job Title, Company, Link, and Score.
