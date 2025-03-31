# Elastic Face Recognition with Manual Autoscaler

## Description
Developed the elastic face recognition application using IaaS resources from AWS. Implemented the application tier of a multi-tiered cloud application, integrated a machine learning model for face recognition, and built an autoscaling mechanism to enable dynamic scaling of the application tier on demand.

## AWS Resources Used
- EC2
- Simple Queue Service (SQS)
- S3
- SimpleDB

## Architecture of the Project
![image](https://github.com/user-attachments/assets/58e0dd84-89aa-4725-8f89-219ad9455ee4)

## Overview
- **Frontend API Server (`server.py`)**: Handles image uploads, sends processing requests, and returns results.
- **EC2 Auto-Scaling Controller (`controller.py`)**: Manages EC2 instances dynamically based on workload.
- **Backend Worker (`backend.py`)**: Processes images and sends results back via SQS.

### 1️⃣ `server.py` - **Frontend API Server**
✅ **Responsibilities:**
- Implements a **FastAPI-based** HTTP server.
- Uploads images to **AWS S3**.
- Sends image processing requests to the **SQS request queue**.
- Waits for responses from the **SQS response queue**.
- Returns the processed results to the user.

🔧 **Tech Stack:**
- FastAPI
- AWS S3
- AWS SQS
- Python

---

### 2️⃣ `controller.py` - **EC2 Auto-Scaling Controller**
✅ **Responsibilities:**
- Monitors the **SQS request queue** for incoming tasks.
- Starts EC2 instances when demand increases.
- Stops unused EC2 instances when demand decreases.
- Ensures efficient resource utilization.

🔧 **Tech Stack:**
- AWS SQS
- AWS EC2
- Python

---

### 3️⃣ `backend.py` - **Image Processing Backend**
✅ **Responsibilities:**
- Runs on EC2 instances to process tasks.
- Reads messages from the **SQS request queue**.
- Performs **image processing** (e.g., OCR, object detection).
- Sends results to the **SQS response queue**.

🔧 **Tech Stack:**
- Python
- AWS SQS
- AWS S3

## How It Works
1. **User uploads an image** via `server.py` (FastAPI).
2. **Server sends a request** to the **SQS request queue**.
3. **`controller.py` starts EC2 instances** based on the queue size.
4. **`backend.py` running on EC2** processes the image.
5. **Result is sent to the SQS response queue**.
6. **`server.py` retrieves and returns the response** to the user.
7. **`controller.py` stops EC2 instances** when no requests remain.

## Setup Instructions
### **Prerequisites**
- Python 3.x
- AWS IAM AccessKeys
- Required Python dependencies (`boto3`, `fastapi`, `uvicorn`)

### **Installation**
1. Clone the repository:
   ```sh
   git clone [https://github.com/your-username/your-repo.git](https://github.com/TejasParse/cloud-project-autoscaler.git)
   cd cloud-project-autoscaler
   ```

2. Install the dependencies
   ```sh
   pip3 install boto3 fastapi uvicorn
   ```
    
3. Update the `backend.py`, `controller.py` and `server.py` with AWS Access Keys
4. Start the `backend`, `controller` and `server` individually 
   ```sh
   python3 backend.py
   python3 controller.py
   python3 server.py
   ```
