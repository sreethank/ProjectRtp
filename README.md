# 🌿 Agri AI   — Intelligent Crop Disease Detection for Indian Farmers

<div align="center">

![Agri AI](https://img.shields.io/badge/Agri-AI-16a34a?style=for-the-badge&logo=leaf&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.17-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-0.110-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Supabase](https://img.shields.io/badge/Supabase-Auth-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)

**An AI-powered Progressive Web App that detects crop diseases from leaf images, delivers treatment recommendations in Telugu, and provides real-time market prices and weather advisories, built for rural farmers in Telangana, India.**

[Features](#-features) · [Demo](#-demo) · [Tech Stack](#-tech-stack) · [Installation](#-installation) · [API Docs](#-api-endpoints) · [ML Model](#-ml-model) · [Screenshots](#-screenshots)

</div>

---

## 📌 Overview

Agri AI empowers smallholder farmers with an intelligent, mobile-first tool that replaces the need to wait days for an agricultural extension officer. A farmer can photograph a diseased leaf, receive an instant diagnosis with pesticide recommendations, hear the advice spoken aloud in Telugu, check current mandi prices, and calculate expected crop profits. All from a basic Android smartphone.

> **"From field to diagnosis in under 2 seconds."**

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔬 **Disease Detection** | Upload leaf photo → EfficientNetB0 CNN classifies 15 disease classes across Tomato, Potato, and Pepper with 92%+ accuracy |
| 💊 **Treatment Advice** | Disease-specific pesticide, fertilizer, and immediate action recommendations from a curated agronomic knowledge base |
| 🔊 **Telugu Voice Output** | Diagnosis and treatment spoken aloud in Telugu via gTTS - accessible for low-literacy farmers |
| 🌤 **Weather Advisory** | Real-time weather via OpenWeather API with automated farming advice rules (delay spray before rain, fungal risk alerts, etc.) |
| 📊 **Market Prices** | Live APMC mandi prices from data.gov.in with fallback reference data when government API is unavailable |
| 🧮 **Profit Calculator** | Input land, yield, cost, and market price to compute net profit, ROI, and break-even price per kg |
| 📋 **Prediction History** | Every diagnosis saved per user in Supabase PostgreSQL with severity, confidence, and treatment details |
| 🔐 **Secure Auth** | Supabase Auth with JWT verification via JWKS (RS256) - email confirmation, auto token refresh |
| 🌐 **Multilingual** | English, Hindi, and Telugu UI support |
| 📱 **PWA — Installable** | Installable on Android from Chrome browser - no Play Store required |

---

## 🎯 Demo

```
Live URL:  (deploy to Vercel + Railway)
API Docs:  http://localhost:8000/docs   (Swagger UI)
```

**Test credentials** (after running locally):
```
Email:    test@agri.ai
Password: test123456
```

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                           AGRI AI SYSTEM                            │
├──────────────────┬──────────────────────┬───────────────────────────┤
│   React PWA      │    FastAPI Backend   │      External Services    │
│   (Vite + PWA)   │    (Python 3.11)     │                           │
│                  │                      │  ┌─────────────────────┐  │
│  ┌────────────┐  │  ┌────────────────┐  │  │  Supabase           │  │
│  │ Auth       │──┼─>│ /login         │  │  │  ├── PostgreSQL DB  │  │
│  │ Home       │  │  │ /register      │  │  │  ├── Auth (JWKS)    │  │
│  │ Detect     │──┼─>│ /predict       │  │  │  └── Row Level Sec  │  │
│  │ Weather    │──┼─>│ /weather       │  │  └─────────────────────┘  │
│  │ Market     │──┼─>│ /market-prices │  │                           │
│  │ Calculator │  │  │ /speak (gTTS)  │  │  ┌─────────────────────┐  │
│  │ History    │──┼─>│ /history       │  │  │  OpenWeather API    │  │
│  └────────────┘  │  └────────────────┘  │  │  data.gov.in API    │  │
│                  │         │            │  │  Google TTS (gTTS)  │  │
│                  │  ┌──────┴──────┐     │  └─────────────────────┘  │
│                  │  │EfficientNetB0│    │                           │
│                  │  │ 15 classes  │     │  ┌─────────────────────┐  │
│                  │  │ ~92% acc    │     │  │  PlantVillage DB    │  │
│                  │  └─────────────┘     │  │  20,654 images      │  │
│                  │                      │  │  15 disease classes │  │
│                  │                      │  └─────────────────────┘  │
└──────────────────┴──────────────────────┴───────────────────────────┘
```

---

## 🧰 Tech Stack

### Backend
| Technology | Version | Purpose |
|---|---|---|
| Python | 3.11 | Core backend language |
| FastAPI | 0.110 | REST API framework with async support |
| TensorFlow / Keras | 2.17 | ML model loading and inference |
| EfficientNetB0 | ImageNet pretrained | Transfer learning base model |
| gTTS | 2.5.3 | Telugu/Hindi/English text-to-speech |
| Supabase Python SDK | 2.3.0 | Database and auth client |
| PyJWT + cryptography | 2.8.0 | JWKS-based JWT verification (RS256) |
| Pillow | 10.4.0 | Image loading and preprocessing |
| Uvicorn | 0.27 | ASGI server |

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| React | 18 | UI framework |
| Vite | 5 | Build tool and dev server |
| vite-plugin-pwa | 0.19 | Service worker and PWA manifest |
| Axios | 1.6 | HTTP client with interceptors |
| localStorage | — | Token and user session storage |

### Infrastructure
| Service | Tier | Purpose |
|---|---|---|
| Supabase | Free (500MB) | PostgreSQL database + Auth |
| Railway | Free ($5 credits) | FastAPI backend hosting |
| Vercel | Free | React frontend hosting |
| OpenWeather API | Free (1M calls/mo) | 7-day weather forecast |
| data.gov.in | Free | Live APMC mandi prices |

**Total monthly cost: ₹0**

---

## 📁 Project Structure

```
agri/
│
├── backend/
│   ├── main.py                  # FastAPI app — all endpoints
│   ├── auth.py                  # JWT/JWKS verification + Supabase Auth
│   ├── database.py              # Supabase client singleton
│   ├── cropmodel_v2.h5          # Trained EfficientNetB0 weights (~95MB)
│   ├── class_indices.json       # Index → class name mapping (auto-generated)
│   ├── requirements.txt
│   └── .env.example
│
├── ml_model/
│   ├── train_fast.py            # Two-phase transfer learning pipeline
│   ├── diagnose.py              # Dataset + model diagnostic tool
│   └── PlantVillage/            # Dataset (not committed — see setup)
│       ├── Tomato_Late_blight/
│       ├── Tomato_Early_blight/
│       └── ...15 folders total
│
└── frontend/
    ├── public/
    │   ├── manifest.json        # PWA manifest
    │   ├── icon-192.png
    │   └── icon-512.png
    ├── src/
    │   ├── App.jsx              # Root component + auth gate
    │   ├── screens/
    │   │   ├── Auth.jsx         # Login + Register
    │   │   ├── Home.jsx         # Dashboard
    │   │   ├── Detect.jsx       # Disease detection
    │   │   ├── Weather.jsx      # Weather advisory
    │   │   ├── Market.jsx       # Market prices
    │   │   ├── Calculator.jsx   # Profit calculator
    │   │   └── History.jsx      # Prediction history
    │   └── utils/
    │       ├── api.js           # Axios instance + all API calls
    │       └── auth.js          # Token storage helpers
    ├── vite.config.js
    └── package.json
```

---

## 🚀 Installation

### Prerequisites

```bash
Python 3.11+
Node.js 18+
Git
```

### 1. Clone the Repository

```bash
git clone https://github.com/sreethan05/agri.git
cd agri
```

### 2. Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv .venv
.venv\Scripts\activate        # Windows
source .venv/bin/activate     # macOS/Linux

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your Supabase credentials (see Environment Variables section)
```

### 3. Download Dataset and Train Model

```bash
cd ml_model

# Download PlantVillage dataset from Kaggle
# https://www.kaggle.com/datasets/emmarex/plantdisease
# Extract to ml_model/PlantVillage/

# IMPORTANT: Rename the spurious metadata folder
# Rename PlantVillage/PlantVillage → PlantVillage/_PlantVillage

# Run diagnostic to verify setup
python diagnose.py

# Train the model (30-45 min on CPU, 5-10 min on GPU)
python train_fast.py

# Output: cropmodel_v2.h5 and class_indices.json
# Copy both files to backend/
cp cropmodel_v2.h5 class_indices.json ../backend/
```

### 4. Set Up Supabase

```
1. Create project at supabase.com
2. Go to SQL Editor → run the schema from database/schema.sql
3. Authentication → Settings:
   - JWT expiry: 604800 (7 days)
   - Enable email confirmation: ON
4. Authentication → URL Configuration:
   - Site URL: http://localhost:5173
   - Redirect URLs: http://localhost:5173
5. Copy credentials to backend/.env
```

### 5. Frontend Setup

```bash
cd frontend
npm install
```

### 6. Run the Application

```bash
# Terminal 1 — Backend
cd backend
uvicorn main:app --host 127.0.0.1 --port 8000

# Terminal 2 — Frontend
cd frontend
npm run dev
```

Open **http://localhost:5173** in your browser.

---

## ⚙️ Environment Variables

Create `backend/.env`:

```env
# Supabase
SUPABASE_URL=https://your-project-id.supabase.co
SUPABASE_KEY=your-service-role-key
SUPABASE_ANON_KEY=your-anon-key
SUPABASE_JWKS_URL=https://your-project-id.supabase.co/auth/v1/.well-known/jwks.json

# External APIs (optional — has fallback defaults)
WEATHER_API_KEY=your-openweather-api-key
MARKET_API_KEY=your-datagov-api-key
```

---

## 📡 API Endpoints

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `GET` | `/health` | ❌ | Server + model status |
| `GET` | `/ping` | ❌ | Liveness check |
| `POST` | `/register` | ❌ | Create farmer account |
| `POST` | `/login` | ❌ | Login → returns JWT |
| `POST` | `/refresh` | ❌ | Refresh expired token |
| `GET` | `/me` | ✅ | Get current user profile |
| `PUT` | `/me` | ✅ | Update profile |
| `POST` | `/predict` | ⚡ | Detect disease from leaf image |
| `GET` | `/speak` | ❌ | Text-to-speech MP3 stream |
| `GET` | `/weather` | ❌ | Live weather + farming advice |
| `GET` | `/market-prices` | ❌ | APMC mandi prices |
| `GET` | `/history` | ✅ | User's prediction history |
| `DELETE` | `/history/{id}` | ✅ | Delete a prediction |
| `GET` | `/classes` | ❌ | List all disease classes |

> ✅ Requires JWT · ⚡ Optional JWT (saves to history if authenticated)

**Interactive API docs:** `http://localhost:8000/docs`

---

## 🤖 ML Model

### Dataset
| Property | Value |
|---|---|
| Source | PlantVillage (Mohanty et al., 2016) |
| Total Images | 20,654 |
| Classes | 15 (Tomato × 10, Potato × 3, Pepper × 2) |
| Image Size | 224 × 224 × 3 (RGB) |
| Train / Val Split | 80% / 20% |

### Architecture
```
Input (224×224×3)
    ↓
EfficientNetB0 — pretrained on ImageNet (frozen in Phase 1)
    ↓
GlobalAveragePooling2D
    ↓
BatchNormalization
    ↓
Dense(256, ReLU)
    ↓
Dropout(0.4)
    ↓
Dense(15, Softmax)  ←  output: probability per disease class
```

### Training Strategy
```
Phase 1 — Frozen Base (fast, ~15-25 min on CPU)
  - Freeze all EfficientNetB0 layers
  - Train only custom head
  - LR: 0.001 | Epochs: 10 max | Early stopping: patience=4
  - Reaches ~88% validation accuracy

Phase 2 — Fine-tuning (precision, ~10-15 min on CPU)
  - Unfreeze last 30 EfficientNetB0 layers
  - LR: 0.0001 (10× smaller to protect pretrained weights)
  - Epochs: 5 max | Early stopping: patience=4
  - Reaches ~92% validation accuracy
```

### Critical Preprocessing Note
```python
# ✅ CORRECT — EfficientNetB0 expects inputs scaled to [-1, +1]
arr = tf.keras.applications.efficientnet.preprocess_input(arr)

# ❌ WRONG — causes 100% incorrect predictions
arr = arr / 255.0
```

### Supported Disease Classes
| # | Class | Crop |
|---|---|---|
| 0 | Bacterial Spot | Pepper |
| 1 | Healthy | Pepper |
| 2 | Early Blight | Potato |
| 3 | Late Blight | Potato |
| 4 | Healthy | Potato |
| 5 | Bacterial Spot | Tomato |
| 6 | Early Blight | Tomato |
| 7 | Late Blight | Tomato |
| 8 | Leaf Mold | Tomato |
| 9 | Septoria Leaf Spot | Tomato |
| 10 | Spider Mites | Tomato |
| 11 | Target Spot | Tomato |
| 12 | Yellow Leaf Curl Virus | Tomato |
| 13 | Mosaic Virus | Tomato |
| 14 | Healthy | Tomato |

---

## 🗄️ Database Schema

```sql
profiles          -- Farmer personal info (linked to Supabase auth.users)
predictions       -- Every disease detection saved per user
farmer_profiles   -- Agricultural details (land, crops, soil type)
```

All tables have **Row Level Security (RLS)** — users can only access their own data.

---

## 📱 Install as Mobile App (PWA)

```
1. Open Chrome on Android
2. Navigate to your app URL
3. Tap ⋮ menu → "Add to Home Screen"
4. App installs with icon — opens like a native app ✅
```

---

## 🚢 Deployment

### Backend → Railway
```bash
# Add Procfile to backend/
echo "web: uvicorn main:app --host 0.0.0.0 --port $PORT" > Procfile

# Push to GitHub
# Railway.app → New Project → Deploy from GitHub
# Add environment variables from .env
```

### Frontend → Vercel
```bash
# Add to frontend/.env.production
VITE_API_URL=https://your-railway-app.railway.app

# Vercel.com → New Project → Import from GitHub
# Set root directory to: frontend/
```

---

## 🧪 Running Tests

```bash
# Diagnose dataset and model
cd ml_model
python diagnose.py

# Test backend endpoints
cd backend
uvicorn main:app --host 127.0.0.1 --port 8000
# Open http://127.0.0.1:8000/docs

# Test JWKS connectivity
curl http://127.0.0.1:8000/jwks-test
```

---

## 🔮 Roadmap

- [ ] Expand to Rice, Cotton, and Groundnut crops
- [ ] Collect real field images from Telangana farmers for domain fine-tuning
- [ ] TensorFlow Lite quantization for on-device inference
- [ ] SMS alerts via Twilio for critical disease outbreaks
- [ ] Offline prediction using cached TFLite model
- [ ] Government scheme integration (PM-KISAN, PMFBY crop insurance)
- [ ] Pair with IoT soil sensors for proactive alerts

---

## 📚 References

- Mohanty, S.P., Hughes, D.P., Salathé, M. (2016). *Using Deep Learning for Image-Based Plant Disease Detection.* Frontiers in Plant Science.
- Tan, M., & Le, Q. (2019). *EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks.* ICML 2019.
- PlantVillage Dataset - https://www.kaggle.com/datasets/emmarex/plantdisease

---

## 🤝 Contributing

Contributions are welcome, especially:
- New crop disease classes and treatment data
- Telugu/Hindi translation improvements
- Field-condition image datasets from Indian farms

```bash
# Fork → clone → create branch
git checkout -b feature/add-rice-diseases

# Make changes → commit → push
git push origin feature/add-rice-diseases

# Open Pull Request
```

---

## 📄 License

This project is licensed under the **MIT License**. Free to use, modify, and distribute.

Built with ❤️ for Indian farmers 🇮🇳

---

<div align="center">

⭐ **Star this repository if it helped you!** ⭐

![Made in Telangana](https://img.shields.io/badge/Made%20in-Telangana%20🌿-16a34a?style=for-the-badge)
![For Farmers](https://img.shields.io/badge/Built%20For-Indian%20Farmers%20🌾-f59e0b?style=for-the-badge)

</div>


---

# DevOps & Automation Lab

---

## 1. Pipelines

### Create a simple pipeline using Jenkins.
**Job Name:** `SimplePipeline`  
**Program:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'echo Building Application'
            }
        }
        stage('Test') {
            steps {
                bat 'echo Testing Application'
            }
        }
    }
}
```

---

### Create a workspace file handling pipeline using Jenkins.
**Job Name:** `FilePipeline`  
**Program:**
```groovy
pipeline {
    agent any
    stages {
        stage('Create File') {
            steps {
                writeFile file: 'pipeline.txt', text: 'Created by Jenkins Pipeline'
            }
        }
        stage('Show File') {
            steps {
                echo readFile('pipeline.txt')
            }
        }
    }
}
```

---

### Implement a parameterized pipeline using Jenkins.
**Job Name:** `ParameterPipeline`  
**Program:**
```groovy
pipeline {
    agent any
    parameters {
        string(name: 'USERNAME', defaultValue: 'Student', description: 'Enter your name')
    }
    stages {
        stage('Greet') {
            steps {
                echo "Hello, ${params.USERNAME}!"
            }
        }
    }
}
```

---

### Implement a scheduled pipeline using Jenkins.
**Job Name:** `ScheduledPipeline`  
**Program:**
```groovy
pipeline {
    agent any
    triggers {
        cron('H/5 * * * *')
    }
    stages {
        stage('Show Time') {
            steps {
                bat 'echo Build time: %date% %time%'
            }
        }
    }
}
```

---

### Implement a multi-stage pipeline using Jenkins.
**Job Name:** `MultiStagePipeline`  
**Program:**
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'echo Build Completed'
            }
        }
        stage('Test') {
            steps {
                bat 'echo Test Completed'
            }
        }
        stage('Deploy') {
            steps {
                bat 'echo Deploy Completed'
            }
        }
    }
}
```

---

## 2. Freestyle Projects

### Demonstrate file creation and copying using a Jenkins Freestyle Project.
**Job Name:** `FileCopy`  
**Commands:**
```cmd
echo Hello Jenkins > file1.txt
copy file1.txt file2.txt
type file2.txt
```

---

### Demonstrate Continuous Integration and Continuous Development using Jenkins.
**Job Name:** `CIProject`  
**Commands:**
```cmd
echo Starting CI Process
if not exist registration.html exit /b 1
echo Registration Form Verified
echo Build Successful
```

---

### Create a simple Hello World Freestyle Project and demonstrate workspace variables using Jenkins.
**Job Name:** `HelloWorld`  
**Commands:**
```cmd
echo Hello World
echo Job Name: %JOB_NAME%
echo Workspace: %WORKSPACE%
echo Build Number: %BUILD_NUMBER%
```

---

### Create a parameterized Freestyle Project using Jenkins.
**Job Name:** `ParameterizedFreestyle`  
**Commands:**
```cmd
echo Hello %NAME%
```

---

### Create a scheduled Freestyle Project using Jenkins.
**Job Name:** `ScheduledFreestyle`  
**Commands:**
```cmd
echo Scheduled Freestyle Job Running
```

---

## 3. Git Branching

### Create a Git Branching Story Project – "A Tale in Branches" using Git branches, where each branch represents a chapter, and finally merge all chapters into a single book.html file.
**Folder:** `StoryProject`  
**Filename:** `book.html`  

**Commands:**
```bash
# Step 1: Create project & initial book
mkdir StoryProject
cd StoryProject
git init
git branch -M main

# Create book.html:
# <html><body><h1>A Tale in Branches</h1></body></html>

git add book.html
git commit -m "Created book"

# Step 2: Create Chapter 1 branch
git switch -c chapter1

# Add to book.html:
# <h2>Chapter 1</h2><p>A boy started his journey.</p>

git add book.html
git commit -m "Added chapter 1"
git switch main
git merge chapter1

# Step 3: Create Chapter 2 branch
git switch -c chapter2

# Add to book.html:
# <h2>Chapter 2</h2><p>He reached a beautiful village.</p>

git add book.html
git commit -m "Added chapter 2"
git switch main
git merge chapter2
```

**Final book.html:**
```html
<html>
<body>
<h1>A Tale in Branches</h1>

<h2>Chapter 1</h2>
<p>A boy started his journey.</p>

<h2>Chapter 2</h2>
<p>He reached a beautiful village.</p>
</body>
</html>
```

---

### Practice Source Code Management (SCM) on GitHub.
**Folder:** `DevOpsLab`  
**Filename:** `registration.html`  

**File: registration.html**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Event Registration</title>
</head>
<body>
    <h2>Event Registration Form</h2>

    <form id="regForm">
        Name: <input type="text" id="name" required><br><br>

        Email: <input type="email" id="email" required><br><br>

        Phone: <input type="text" id="phone" required><br><br>

        Gender:
        <select id="gender" required>
            <option value="">Select</option>
            <option>Male</option>
            <option>Female</option>
            <option>Other</option>
        </select><br><br>

        Event:
        <select id="event" required>
            <option value="">Select</option>
            <option>Hackathon</option>
            <option>Workshop</option>
        </select><br><br>

        <button type="submit">Register</button>
    </form>

    <p id="message"></p>

    <script>
        document.getElementById("regForm").onsubmit = function(e) {
            e.preventDefault();
            document.getElementById("message").innerText =
                "Registration Successful!";
        };
    </script>
</body>
</html>
```

**Commands:**
```bash
git init
git branch -M main
git add registration.html
git commit -m "Added registration form"
git remote add origin https://github.com/USERNAME/DevOpsLab.git
git push -u origin main

git switch -c update
git add registration.html
git commit -m "Updated registration form"
git switch main
git merge update
git push origin main
```

---

## 4. Docker

### Create a simple containerized application using Docker.
**Folder:** `DockerHTML`  

**File 1: index.html**
```html
<!DOCTYPE html>
<html>
<body>
    <h1>Hello Docker</h1>
    <p>My First Containerized Application</p>
</body>
</html>
```

**File 2: Dockerfile**
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

**Commands:**
```cmd
docker build -t myweb .
docker run -d --name mywebcontainer -p 8082:80 myweb
```

---

### Run a Python file using Docker.
**Folder:** `DockerPython`  

**File 1: hello.py**
```python
print("Hello Python from Docker")
```

**File 2: Dockerfile**
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY hello.py .
CMD ["python", "hello.py"]
```

**Commands:**
```cmd
docker build -t pythonapp .
docker run --rm pythonapp
```

---

### Run a Java file using Docker.
**Folder:** `DockerJava`  

**File 1: Hello.java**
```java
class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Java from Docker");
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Hello.java .
RUN javac Hello.java
CMD ["java", "Hello"]
```

**Commands:**
```cmd
docker build -t javaapp .
docker run --rm javaapp
```

---

### Implement a parameterized constructor in Java using Docker.
**Folder:** `DockerConstructor`  

**File 1: Student.java**
```java
class Student {
    String name;
    int age;

    Student(String n, int a) {
        name = n;
        age = a;
    }

    public static void main(String[] args) {
        Student s = new Student("Sreethan", 20);
        System.out.println("Name: " + s.name);
        System.out.println("Age: " + s.age);
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Student.java .
RUN javac Student.java
CMD ["java", "Student"]
```

**Commands:**
```cmd
docker build -t constructorapp .
docker run --rm constructorapp
```

---

### Implement a palindrome program in Java using Docker.
**Folder:** `DockerPalindrome`  

**File 1: Palindrome.java**
```java
import java.util.Scanner;

class Palindrome {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number: ");
        int n = sc.nextInt();
        int temp = n, rev = 0;

        while (n > 0) {
            rev = rev * 10 + n % 10;
            n = n / 10;
        }

        if (temp == rev)
            System.out.println("Palindrome");
        else
            System.out.println("Not Palindrome");
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Palindrome.java .
RUN javac Palindrome.java
CMD ["java", "Palindrome"]
```

**Commands:**
```cmd
docker build -t palindromeapp .
docker run -it --rm palindromeapp
```

---

### Implement single inheritance in Java using Docker.
**Folder:** `DockerInheritance`  

**File 1: Inheritance.java**
```java
class Animal {
    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

class Inheritance {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
        d.bark();
    }
}
```

**File 2: Dockerfile**
```dockerfile
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY Inheritance.java .
RUN javac Inheritance.java
CMD ["java", "Inheritance"]
```

**Commands:**
```cmd
docker build -t inheritanceapp .
docker run --rm inheritanceapp
```

---

## 5. Kubernetes

### Integrate Kubernetes with Docker.
**Folder:** `DockerHTML`  
**Filename:** `deployment.yaml`  

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myweb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myweb
  template:
    metadata:
      labels:
        app: myweb
    spec:
      containers:
        - name: myweb
          image: myweb:latest
          imagePullPolicy: Never
          ports:
            - containerPort: 80
```

**Commands:**
```cmd
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
```

---

### Automate the execution of a containerized application using Kubernetes.
**Folder:** `DockerHTML`  
**Filename:** `service.yaml`  

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myweb-service
spec:
  selector:
    app: myweb
  ports:
    - port: 80
      targetPort: 80
  type: ClusterIP
```

**Commands:**
```cmd
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get pods
kubectl get services
kubectl port-forward service/myweb-service 8083:80
```

---

## 6. Selenium Testing

### Write a simple JavaScript program to perform testing using Selenium.
**Folder:** `C:\selenium`  

**File 1: index.html**
```html
<html>
<body>
    <h2>JavaScript Testing</h2>

    <button id="btn" onclick="show()">Click Me</button>

    <p id="msg"></p>

    <script>
        function show() {
            document.getElementById("msg").innerHTML = "Hello World";
        }
    </script>
</body>
</html>
```

**File 2: JavaScriptTest.java**
```java
import org.openqa.selenium.*;
import org.openqa.selenium.edge.EdgeDriver;

public class JavaScriptTest {
    public static void main(String[] args) {
        WebDriver driver = new EdgeDriver();

        driver.get("file:///C:/selenium/index.html");

        JavascriptExecutor js = (JavascriptExecutor) driver;

        js.executeScript("document.getElementById('btn').click()");

        System.out.println(driver.findElement(By.id("msg")).getText());
    }
}
```

**Execution Steps:**
1. Save `index.html` in `C:\selenium`.
2. Create `JavaScriptTest.java` in NetBeans.
3. Add Selenium libraries.
4. Right-click the Java file ➔ Run File.

---

### Develop test cases for a containerized application using Selenium.
**Folder:** `RegistrationApp`  

**File 1: registration.html**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Event Registration</title>
</head>
<body>
    <h2>Event Registration Form</h2>

    <form id="regForm">
        Name: <input type="text" id="name" required><br><br>

        Email: <input type="email" id="email" required><br><br>

        Phone: <input type="text" id="phone" required><br><br>

        Gender:
        <select id="gender" required>
            <option value="">Select</option>
            <option>Male</option>
            <option>Female</option>
            <option>Other</option>
        </select><br><br>

        Event:
        <select id="event" required>
            <option value="">Select</option>
            <option>Hackathon</option>
            <option>Workshop</option>
        </select><br><br>

        <button type="submit">Register</button>
    </form>

    <p id="message"></p>

    <script>
        document.getElementById("regForm").onsubmit = function(e) {
            e.preventDefault();
            document.getElementById("message").innerText =
                "Registration Successful!";
        };
    </script>
</body>
</html>
```

**File 2: Dockerfile**
```dockerfile
FROM nginx:alpine
COPY registration.html /usr/share/nginx/html/index.html
```

**File 3: RegistrationTest.java**
```java
import org.openqa.selenium.*;
import org.openqa.selenium.edge.EdgeDriver;

public class RegistrationTest {
    public static void main(String[] args) {
        WebDriver driver = new EdgeDriver();

        driver.get("http://localhost:8084");

        driver.findElement(By.id("name")).sendKeys("Sreethan");
        driver.findElement(By.id("email")).sendKeys("test@gmail.com");
        driver.findElement(By.id("phone")).sendKeys("9876543210");
        driver.findElement(By.id("gender")).sendKeys("Male");
        driver.findElement(By.id("event")).sendKeys("Hackathon");

        driver.findElement(By.tagName("button")).click();

        String msg = driver.findElement(By.id("message")).getText();

        if (msg.equals("Registration Successful!"))
            System.out.println("Test Passed");
        else
            System.out.println("Test Failed");
    }
}
```

**Execution Commands:**
```cmd
docker build -t registrationapp .
docker run -d -p 8084:80 registrationapp
```


---

## 👤 Developer Profile

### Kasagoni Sai Sreethan (sreethank)
- **Role:** Computer Science Student & DevOps Enthusiast
- **GitHub:** [https://github.com/sreethank](https://github.com/sreethank)
- **Email:** sreethankasagoni@gmail.com
- **Skills:** Java, Python, HTML, Git & GitHub, Docker, Jenkins, Kubernetes, Selenium, TensorFlow, FastAPI, React
- **Projects:** 
  - Agri AI (Intelligent Crop Disease Detection for Indian Farmers)
  - Event Registration Form & Automated CI/CD
  - DevOps Lab Programs & CI/CD Pipelines
- **Programs & Scripts Reference:** Complete DevOps, Docker, Kubernetes, and Selenium reference scripts are available in [`Rtp.txt`](./Rtp.txt).
