# Automated Threat Intelligence Hub - System Architecture Proposal

## Team Members

| Name                 | Role/Component           | GitHub Username |
| -------------------- | ------------------------ | --------------- |
| **Donald Reith**     | **Data Ingestion**       | @username1      |
| **Jonah Mitchell**   | **AI Processing**        | @jonahproj      |
| **Mervin Laforteza** | **Scoring**              | @username3      |
| **Kevin Medrano**    | **Integration & Output** | @username4      |

## Problem Statement

Organizations face an overwhelming volume of security threats daily from various data sources such as blogs, RSS feeds, and CVE databases. It’s challenging for security teams to aggregate, process, and prioritize these threats manually. Our project addresses this issue by automating the collection, summarization, and prioritization of security threat data, helping security analysts focus on critical threats in real-time.

## Target Users

* **Security Analysts**: Analysts in medium to large organizations responsible for monitoring, evaluating, and responding to security alerts.
* **Incident Response Teams**: Teams within companies focused on responding to emerging threats and vulnerabilities.
* **Threat Intelligence Platforms**: Organizations that aggregate and distribute threat intelligence data to other security teams.

## Architecture

![Architecture Diagram](docs/GroupProject.drawio.png)

## Component Breakdown

### 1. Data Ingestion: Feed Collector (Owner: **Donald Reith**)

* **Description**: The Feed Collector component uses an n8n workflow to scrape and pull data from various threat intelligence sources like RSS feeds, security blogs, and public threat feeds. The data is then normalized and stored in Airtable for processing.
* **Tools**: n8n, Airtable
* **Input**: Raw RSS/HTTP feeds from external sources.
* **Output**: Normalized threat records in Airtable.
* **Standalone Demo**: Demonstrate the Feed Collector scraping an RSS feed and storing normalized data in Airtable.

### 2. AI Processing: AI Summarizer & IOC Extractor (Owner: **Jonah Mitchell**)

* **Description**: This component processes the ingested threat data to generate summarized reports and extract key Indicators of Compromise (IOCs), such as IP addresses, domains, and file hashes. The processed data is enriched and written back into Airtable.
* **Tools**: Flowise, Groq/Hugging Face API
* **Input**: Raw threat data entries from Airtable.
* **Output**: Summarized threat information with structured IOCs in Airtable.
* **Standalone Demo**: Show the AI chain processing a sample threat entry, extracting IOCs, and summarizing it in Airtable.

### 3. Scoring: Relevance Scorer (Owner: **Mervin Laforteza**)

* **Description**: The Relevance Scorer assigns relevance scores to the threat entries based on the defined technology stack (e.g., Windows, Apache, Python). This allows for prioritizing which threats need immediate attention. The scoring results are saved back into Airtable.
* **Tools**: n8n, Groq API, Airtable
* **Input**: Threat entries with associated tech stack.
* **Output**: Relevance scores for threats, prioritized based on criteria.
* **Standalone Demo**: Demonstrate the prioritization of threats based on relevance scoring using sample data.

### 4. Integration & Output: Dashboard, Testing & Presentation (Owner: **Kevin Medrano**)

* **Description**: This component handles the integration of all workflows, builds a shared Airtable database, and creates a Streamlit dashboard to visualize the threat data, trends, and allow CSV export. It also involves the testing and documentation of the system, ensuring everything is functioning as expected.
* **Tools**: Airtable, GitHub Pages, Streamlit
* **Input**: Data from all components in Airtable.
* **Output**: Dashboards with visualizations, CSV exports, and weekly briefings.
* **Standalone Demo**: Show the integration of threat data into the dashboard, with visualizations and filtering options.

## Data Sources

* **Primary Data**: RSS feeds from security blogs, CVE databases, and public threat feeds.
* **Sample Data**: Raw threat data such as RSS feed entries, security blog reports, and threat alerts in JSON/CSV format.
* **Data Format**: CSV, JSON, API responses from external sources.

## AI Capabilities Table

| Capability                   | Purpose                                   | Model/API             |
| ---------------------------- | ----------------------------------------- | --------------------- |
| **Threat Summarization**     | Summarize threat reports                  | Flowise               |
| **IOC Extraction**           | Extract key indicators (IP, domain, hash) | Groq/Hugging Face API |
| **Threat Relevance Scoring** | Prioritize threats by relevance           | Groq API              |

## Success Criteria

1. **Data Collection**: The system must be able to ingest threat data from at least 3 external data sources (e.g., blogs, feeds, CVE databases).
2. **AI Processing Accuracy**: The AI model should summarize and extract IOCs from threat reports with at least 90% accuracy.
3. **Data Integration**: The integration between all components must be seamless, with data flowing from ingestion to scoring to the dashboard.
4. **Scalability**: The system should be able to handle a minimum of 500 new threat entries per day without significant performance degradation.
5. **User Interface**: The Streamlit dashboard should display relevant data, allow for filtering, and provide CSV export functionality for analysts.

## Timeline

| Week  | Milestone                                                                    |
| ----- | ---------------------------------------------------------------------------- |
| 3     | Complete project proposal, architecture diagram, and GitHub repository setup |
| 4-6   | Develop individual components and begin testing with sample data             |
| 7-9   | Implement AI processing, refine summarization and IOC extraction             |
| 10-12 | Integrate components, handle errors, and build out the dashboard UI          |
| 13-14 | Conduct final testing, polish the interface, and complete documentation      |
| 15    | Final project presentation and demo                                          |

---

