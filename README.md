Automated WordPress Vulnerability Scanning with GitHub Actions & WPScan

🛡️ Overview
This project demonstrates how to automate the vulnerability scanning process for a WordPress site using Docker containerization and WPScan, as part of the information gathering and discovery phase in a DevSecOps workflow.

⚙️ What the Workflow Does

- Spins up a vulnerable WordPress site (version 5.5) in Docker
- Uses GitHub Actions to automate scanning on push events
- Runs WPScan directly in the workflow to enumerate plugins, themes, users, and configuration backups
- Uses secure GitHub Secrets (`IONUT_COTOLAN_DB_PASS`, `IONUT_COTOLAN_DB_ROOT`) for database credentials
- Logs actionable results in the GitHub Actions panel

🔐 GitHub Secrets Used

| Secret Name               | Description                          |
|---------------------------|--------------------------------------|
| IONUT_COTOLAN_DB_PASS     | Password for the `wordpress` user    |
| IONUT_COTOLAN_DB_ROOT     | Root password for MySQL              |
| WPSCAN_TOKEN              | Token used to fetch vulnerability data from WPScan API (optional for richer output) |

🔍 Example WPScan Findings

- WordPress version detected: 5.5
- This version is **outdated** and contains known vulnerabilities
- Enumerated user: `admin`
- Plugin: Akismet detected – known XSS vulnerability in version 4.1.9
- The WordPress site was initially found in **install mode**, which could allow an attacker to create the first admin user

🧪 How to Re-run Locally

1. Ensure Docker Desktop is running
2. Create a .env file in the same directory as docker-compose.yml:

env:
IONUT_COTOLAN_DB_PASS=****
IONUT_COTOLAN_DB_ROOT=********


3. Start services:

bash docker-compose up -d

4. Visit [http://localhost:8080](http://localhost:8080) to complete WordPress setup.

5. Run WPScan via Docker (with your IP if localhost fails):

bash docker run -it --rm wpscanteam/wpscan   --url http://192.168.X.X:8080   --api-token YOUR_API_TOKEN   --disable-tls-checks --enumerate vp,vt,cb,u 

📋 Notes

- All secrets are personal and named according to instructions (e.g., IONUT_COTOLAN)
- No sensitive credentials are exposed in logs or code
- The workflow runs automatically on push to main

👤 Author

Ionuț Coțolan  
Master's student in Cybersecurity  
West University of Timișoara

---

For academic use and DevSecOps demonstrations only.