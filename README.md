# FastAPI Task Manager with LLM Integration

This project is a FastAPI-based task management service that allows users to create, update, retrieve, and delete tasks. It also integrates LangChain and LangGraph to analyze task descriptions and categorize them automatically using an LLM.

## Features

- FastAPI-based CRUD operations for task management
- PostgreSQL database with SQLAlchemy ORM and Alembic migrations
- AI-powered task categorization using LangChain and OpenAI API
- Secure API key handling with environment variables
- Docker support for easy deployment (optional)

## Setup Instructions
2. Create and activate a virtual environment  
python -m venv venv source venv/bin/activate # macOS/Linux venv\Scripts\activate # Windows


3. Install dependencies  
pip install -r requirements.txt


4. Create a `.env` file and add the following:  
DATABASE_URL=postgresql://your_user:your_password@localhost/tasks_db OPENAI_API_KEY=sk-your-openai-api-key

Replace `your_user`, `your_password`, and `sk-your-openai-api-key` with actual values.

5. Apply database migrations  
alembic upgrade head


6. Start the FastAPI server  
uvicorn app.main:app --reload

The server will run at `http://127.0.0.1:8000/`

## API Endpoints

### Task Management
- `POST /tasks/` → Create a new task  
- `GET /tasks/{task_id}` → Retrieve a specific task  
- `PUT /tasks/{task_id}` → Update a task  
- `DELETE /tasks/{task_id}` → Delete a task  

Example request to create a task:  
curl -X POST "http://127.0.0.1:8000/tasks/" -H "Content-Type: application/json" -d '{"title": "Bug Fix", "description": "Fix login issue", "status": "pending"}'

### Task Categorization
- `POST /tasks/analyze/` → Categorizes a task based on description  

Example request:  
curl -X POST "http://127.0.0.1:8000/tasks/analyze/" -H "Content-Type: application/json" -d '{"description": "Fix the login bug"}'

Expected response: `{"category": "Bug"}`

## Docker Deployment (Optional)
To run the app with Docker, use:  
docker-compose up --build

This will start both PostgreSQL and the FastAPI service in containers.
