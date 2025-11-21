📌 1. Project Requirements
✅ Software Needed
Tool	Purpose
Python 3.9+	Running Flask backend
Docker + Docker Desktop	Running PostgreSQL instance
pip / virtualenv	Installing Python dependencies
PostgreSQL client (optional)	Manual DB inspection
📦 2. How to Start PostgreSQL in Docker

Run the following command to start your Postgres container:

docker run --name postgres-container \
    -e POSTGRES_PASSWORD=postgres123 \
    -e POSTGRES_USER=postgres \
    -e POSTGRES_DB=placement \
    -p 5433:5432 \
    -d postgres

🔍 Meaning of the command

5433:5432 → Your Flask app connects to port 5433

Username: postgres

Password: postgres123

Database: placement

Container name: postgres-container


🔧 4. Python Environment Setup
1️⃣ Create a virtual environment
python -m venv venv

2️⃣ Activate it
Windows:
venv\Scripts\activate

3️⃣ Install required packages
pip install flask psycopg2-binary pandas werkzeug


(Add more libraries if your jobs1.py needs them)

🛠️ 5. Update Database URL in app.py

Your Flask app is already configured:

DATABASE_URL = "postgresql://postgres:postgres123@localhost:5433/placement"


No changes needed as long as Docker uses port 5433.

🗄️ 6. First-Time Project Initialization

When you run the project for the first time:

It creates userinfo table

It creates companies table

It creates recommendations table

It loads companies_data.csv into DB


▶️ 7. Running the Flask App

Run:

python app.py


Server starts at:

http://127.0.0.1:5000/

🧪 8. How the Workflow Runs
🔹 User Side

User signs up

User logs in

User profile is fetched

Recommendations generated using recommend_jobs()

Results saved to DB

User sees job matches

🔹 Recruiter Side

Recruiter logs in using company ID

Company dashboard opens

Job postings shown (filtered using company id)

System lists candidates who matched with this company’s job

📊 9. Important Files
File	Purpose

companies_data.csv	Loaded into PostgreSQL

jobs_info.csv	Used by recommendation system

jobs1.py	Main recommendation logic

app.py	Entire Flask backend

🧩 10. Stopping the PostgreSQL Container

docker stop postgres-container

To start again:

docker start postgres-container

To delete completely:

docker rm postgres-container

🎯 11. Common Errors & Fixes
❌ Database connection failed

✔ Make sure Docker is running
✔ Make sure container is running:

docker ps

❌ Port already in use (5433)

Change the port:

-p 5434:5432


Update in app.py:

postgresql://postgres:postgres123@localhost:5434/placement
