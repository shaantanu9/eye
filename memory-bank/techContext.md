# EYE Technical Context

## Technology Stack

### Backend Technologies
- **Framework**: FastAPI (Python 3.11+)
- **Database**: PostgreSQL 16 with SQLAlchemy ORM
- **Cache/Queue**: Redis 7 for job queuing and caching
- **Storage**: MinIO (S3-compatible object storage)
- **AI/ML**: 
  - YOLO-E for object detection (4000+ classes)
  - Ollama for LLM processing (Gemma3:12b)
  - FAISS for vector similarity search
- **Monitoring**: Prometheus for metrics collection

### Frontend Technologies
- **Framework**: Next.js 14 with TypeScript
- **Styling**: Tailwind CSS with custom design system
- **State Management**: Zustand for client state
- **Data Fetching**: TanStack Query (React Query)
- **UI Components**: Custom components with accessibility focus

### Infrastructure
- **Containerization**: Docker with Docker Compose
- **GPU Support**: NVIDIA CUDA integration
- **Networking**: Internal Docker network with service discovery
- **Development**: Hot reload for both frontend and backend

## Development Environment

### Prerequisites
- Docker Desktop with GPU support
- NVIDIA drivers (for GPU acceleration)
- Git for version control

### Setup Process
1. Clone repository
2. Run `python scripts/generate-config.py`
3. Execute `docker-compose up -d --build`
4. Access frontend at http://localhost:3003
5. Access backend API at http://localhost:8001

### Service Ports
- Frontend: 3003
- Backend API: 8001
- PostgreSQL: 5433
- Redis: 6380
- MinIO: 9002 (API), 9003 (Console)
- Prometheus: 9090
- Ollama: 11434

## Configuration Management

### Environment Variables
- `EYE_ENVIRONMENT`: development/production
- `NVIDIA_VISIBLE_DEVICES`: GPU configuration
- Database credentials and connection strings
- MinIO access keys and endpoints

### Configuration Files
- `config/eye.yaml`: Centralized configuration
- `docker-compose.yml`: Service orchestration
- `backend/settings.py`: Application settings
- `frontend/next.config.js`: Next.js configuration

## AI/ML Integration

### YOLO-E Integration
- **Purpose**: Object detection with 4000+ base classes
- **Features**: Few-shot learning, batch processing
- **Models**: yoloe-11s-seg.pt, yoloe-11l-seg.pt
- **GPU Support**: CUDA acceleration for inference

### Ollama Integration
- **Purpose**: LLM processing for text generation
- **Model**: Gemma3:12b (default)
- **Features**: Chat, text generation, vision processing
- **GPU Support**: Automatic GPU detection and usage

### Vector Search
- **Technology**: FAISS for similarity search
- **Embeddings**: Sentence transformers for text
- **Index Type**: IndexFlatIP for inner product similarity
- **Persistence**: Index saved to disk for persistence

## Data Storage Architecture

### Object Storage (MinIO)
- **Purpose**: Store image files and large binary data
- **Organization**: `/memories/{user_id}/{image_uuid}.{format}`
- **Features**: S3-compatible API, versioning, lifecycle policies

### Relational Database (PostgreSQL)
- **Purpose**: Store metadata, user data, processing status
- **Tables**: memory_records, users, jobs, etc.
- **Features**: ACID compliance, indexing, relationships

### Vector Database (FAISS)
- **Purpose**: Fast similarity search for memory retrieval
- **Index**: 384-dimensional vectors for text embeddings
- **Features**: GPU acceleration, persistence, batch operations

## Performance Considerations

### GPU Utilization
- **YOLO-E**: CUDA acceleration for object detection
- **Ollama**: GPU memory management for LLM inference
- **FAISS**: GPU-accelerated vector operations

### Memory Management
- **Image Processing**: Streaming for large files
- **Batch Processing**: Configurable batch sizes
- **Cache Strategy**: Redis for frequently accessed data

### Scalability Patterns
- **Horizontal Scaling**: Multiple worker processes
- **Load Balancing**: Docker service scaling
- **Resource Limits**: Memory and CPU constraints

## Security Considerations

### Data Privacy
- **Local Processing**: No external API calls for sensitive data
- **Encryption**: End-to-end encryption for data at rest
- **Access Control**: User-based data isolation

### Input Validation
- **File Types**: Strict image format validation
- **Size Limits**: Maximum file size restrictions
- **Content Validation**: Image format verification

### Network Security
- **CORS**: Configured for local development
- **HTTPS**: SSL/TLS for production deployment
- **Firewall**: Internal network isolation





