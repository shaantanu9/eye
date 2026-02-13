# EYE System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                EYE SYSTEM ARCHITECTURE                          │
└─────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Backend API   │    │   AI Services   │
│   (Next.js)     │    │   (FastAPI)     │    │                 │
│                 │    │                 │    │                 │
│ • Memory UI     │◄──►│ • Memory API    │◄──►│ • YOLO-E        │
│ • EYE AI Chat   │    │ • Ollama API    │    │ • Ollama        │
│ • Upload        │    │ • YOLO-E API    │    │ • FAISS         │
│ • Search        │    │ • Auth API      │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Storage       │    │   Queue         │    │   Monitoring    │
│   Layer         │    │   System        │    │                 │
│                 │    │                 │    │                 │
│ • MinIO         │    │ • Redis         │    │ • Prometheus    │
│ • PostgreSQL    │    │ • Workers       │    │ • Health Checks │
│ • FAISS         │    │ • Job Queue     │    │ • Metrics       │
└─────────────────┘    └─────────────────┘    └─────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                              DATA FLOW DIAGRAM                                  │
└─────────────────────────────────────────────────────────────────────────────────┘

Memory Upload Flow:
┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
│  User   │───►│Frontend │───►│Backend  │───►│ MinIO   │───►│Storage  │
│ Upload  │    │ Upload  │    │ API     │    │ Storage │    │Success  │
└─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘
                       │
                       ▼
                ┌─────────┐    ┌─────────┐    ┌─────────┐
                │ Redis   │───►│ Worker  │───►│ AI      │
                │ Queue   │    │ Process │    │ Analysis│
                └─────────┘    └─────────┘    └─────────┘
                       │
                       ▼
                ┌─────────┐    ┌─────────┐    ┌─────────┐
                │ YOLO-E  │───►│ Ollama  │───►│ FAISS   │
                │ Objects │    │ Desc    │    │ Vectors │
                └─────────┘    └─────────┘    └─────────┘

Search Flow:
┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
│  User   │───►│Frontend │───►│Backend  │───►│ FAISS   │───►│Results  │
│ Query   │    │ Search  │    │ API     │    │ Search  │    │ Display │
└─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                              SERVICE DETAILS                                    │
└─────────────────────────────────────────────────────────────────────────────────┘

Frontend Services:
├── Next.js Application (Port 3003)
│   ├── Memory Management UI
│   ├── EYE AI Chat Interface
│   ├── Upload Components
│   └── Search Interface

Backend Services:
├── FastAPI Application (Port 8001)
│   ├── Memory API (/api/v1/memory)
│   ├── Ollama API (/api/v1/ollama)
│   ├── YOLO-E API (/api/v1/yolo-e)
│   └── Auth API (/api/v1/auth)

AI Services:
├── YOLO-E Engine
│   ├── Object Detection (4000+ classes)
│   ├── Few-shot Learning
│   └── Batch Processing
├── Ollama Service (Port 11434)
│   ├── Gemma3:12b Model
│   ├── Chat & Text Generation
│   └── Vision Processing
└── FAISS Vector Search
    ├── 384-dimensional embeddings
    ├── Similarity search
    └── Index persistence

Storage Services:
├── MinIO (Port 9002/9003)
│   ├── Object Storage
│   ├── S3-compatible API
│   └── Image Files
├── PostgreSQL (Port 5433)
│   ├── Metadata Storage
│   ├── User Data
│   └── Processing Status
└── Redis (Port 6380)
    ├── Job Queue
    ├── Caching
    └── Session Storage

Infrastructure:
├── Docker Compose
│   ├── Service Orchestration
│   ├── Network Management
│   └── Volume Management
├── GPU Support
│   ├── NVIDIA CUDA
│   ├── GPU Memory Management
│   └── Acceleration
└── Monitoring
    ├── Prometheus (Port 9090)
    ├── Health Checks
    └── Metrics Collection

┌─────────────────────────────────────────────────────────────────────────────────┐
│                              TECHNOLOGY STACK                                   │
└─────────────────────────────────────────────────────────────────────────────────┘

Backend:
├── Python 3.11+
├── FastAPI
├── SQLAlchemy
├── Pydantic
├── Redis
├── MinIO
└── FAISS

Frontend:
├── Next.js 14
├── TypeScript
├── Tailwind CSS
├── React Query
├── Zustand
└── React Dropzone

AI/ML:
├── YOLO-E (Ultralytics)
├── Ollama
├── Gemma3:12b
├── Sentence Transformers
└── CUDA

Infrastructure:
├── Docker
├── Docker Compose
├── PostgreSQL
├── Redis
├── MinIO
└── Prometheus

┌─────────────────────────────────────────────────────────────────────────────────┐
│                              DEPLOYMENT ARCHITECTURE                           │
└─────────────────────────────────────────────────────────────────────────────────┘

Development Environment:
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Local Machine │    │   Docker        │    │   Services      │
│                 │    │   Compose       │    │                 │
│ • Code Editor   │───►│ • Containers    │───►│ • All Services  │
│ • Git           │    │ • Networks      │    │ • GPU Support   │
│ • Docker        │    │ • Volumes       │    │ • Hot Reload    │
└─────────────────┘    └─────────────────┘    └─────────────────┘

Production Environment:
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Load Balancer │    │   Application   │    │   Data Layer    │
│                 │    │   Servers        │    │                 │
│ • Nginx         │───►│ • Backend       │───►│ • PostgreSQL    │
│ • SSL/TLS       │    │ • Frontend      │    │ • MinIO         │
│ • Rate Limiting │    │ • Workers       │    │ • Redis         │
└─────────────────┘    └─────────────────┘    └─────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                              SECURITY ARCHITECTURE                             │
└─────────────────────────────────────────────────────────────────────────────────┘

Security Layers:
├── Network Security
│   ├── Docker Network Isolation
│   ├── Internal Service Communication
│   └── Port Management
├── Data Security
│   ├── Local Processing (No Cloud)
│   ├── Encryption at Rest
│   └── User Data Isolation
├── API Security
│   ├── Input Validation
│   ├── File Type Validation
│   └── Size Limits
└── Authentication
    ├── JWT Tokens
    ├── User Sessions
    └── Access Control





