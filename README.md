
# CodeMatch (Picture)

We detect stolen* code using LLM

The system repository is where we have the final application of CodeMatch.
In this repe we present the general workflow from how we retrieve the code from the web, to how we detect code clones with a given code snippet. 
The system is devided into three main components - Backend, Frontend and a Vector Database.

Gif/ Screenshots of the web app

## Table of Contents
..
..
..


---

## General Components

The system has two main components that make it fully run:
- System Workflow - the structure of backend + frontend and the connection to the database.
  (Image of the workflow)

- Populate Database - in order to have data in the database we should retrieve code projects from github - in this step we do this.
   (Image of the workflow)




## Installation and Run

### **Prerequisites**:

1. **Python**: 3.9+  
2. **Docker Desktop**:  
   [Download Docker Desktop](https://www.docker.com/products/docker-desktop)

3. **Qdrant**:  
   [Download and Run Qdrant](https://qdrant.tech/documentation/quickstart/) – Follow the **Download and Run** section for installation.

4. **Node.js and npm**:  
   a. Install from [Node.js](https://nodejs.org/en) – Keep the option checked to install necessary tools.  
   b. Verify installation:  
   ```bash
   npm -v
   ```

5. **Clone the Repository**:
   ```bash
   git clone https://github.com/codematch-llm/system.git
   ```

6. **Acquire Access to The-Stack-V2 Dataset**:   
   a. [Get access to The-Stack-V2 dataset](https://huggingface.co/datasets/bigcode/the-stack-v2-train-smol-ids)  
   b. [Create a Hugging Face personal access token](https://huggingface.co/settings/tokens/new?tokenType=read)  
   c. Add the token to the `.env` file in the root directory:  
   ```plaintext
   HUGGING_FACE_TOKEN=<paste your token here>
   ```

---

### **Running Locally**

#### **Installation**

1. **Backend**:
   ```bash
   cd backend
   pip install -r requirements.txt
   ```

2. **Frontend**:
   ```bash
   cd frontend
   npm install
   ```



#### **Run**

1. **Ensure you are in the project root directory (ends with `system`)**.

2. **Terminal 1**: Start the frontend:
   ```bash
   cd frontend
   npm run serve
   ```
   - Access the Vue.js frontend at [http://localhost:8080](http://localhost:8080).

3. **Terminal 2**: Start the backend:
   ```bash
   $env:PYTHONPATH = (Get-Location).Path  # Ensure the path ends with 'backend' (check with `Write-Output $env:PYTHONPATH`)
   cd backend
   uvicorn backend.main:app --reload
   ```
   - The backend API will be available at [http://localhost:8000](http://localhost:8000).

4. **Terminal 3**: Start the Qdrant database:  
   If installed separately, run Qdrant per its documentation. If a script (`qdrant_server.py`) is included in this project:
   ```bash
   cd backend
   python qdrant_server.py
   ```

5. **Populate the Vector Database**:
   ```bash
   cd backend
   python populate_database.py
   ```
   - Verify the database is populated by checking the Qdrant dashboard at [http://localhost:6333/dashboard](http://localhost:6333/dashboard).

---

### **Running with Docker**

1. **Ensure you are in the project root directory (`system`)**.

2. **Start all services**:
   ```bash
   docker-compose up
   ```
   - This launches:
     - Backend API at [http://localhost:8000](http://localhost:8000)
     - Frontend at [http://localhost:8080](http://localhost:8080)
     - Qdrant Dashboard at [http://localhost:6333/dashboard](http://localhost:6333/dashboard)

3. **Populate the Database**:
   ```bash
   cd backend
   $env:PYTHONPATH = (Get-Location).Path  # Ensure the path ends with 'backend' (check with `Write-Output $env:PYTHONPATH`)
   python populate_database.py
   ```

