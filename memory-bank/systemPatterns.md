# EYE System Patterns

## Architecture Overview
EYE follows a microservices architecture with clear separation of concerns:

### Core Services
- **Backend API**: FastAPI-based REST API with modular routers
- **Frontend**: Next.js application with feature-based organization
- **Memory Service**: Intelligent memory processing and storage
- **AI Services**: YOLO-E for vision, Ollama for LLM processing
- **Storage Services**: MinIO for objects, PostgreSQL for metadata, FAISS for vectors
- **Worker System**: Redis-based job queue for background processing

## Key Design Patterns

### 1. Service-Oriented Architecture
Each major functionality is encapsulated in its own service:
- `MemoryService`: Handles image processing and storage
- `OllamaService`: Manages LLM interactions
- `YOLOENode`: Computer vision processing
- `S3Adapter`: Storage abstraction layer

### 2. API-First Design
- RESTful endpoints with clear resource modeling
- Pydantic models for request/response validation
- OpenAPI documentation generation
- Consistent error handling and status codes

### 3. Background Processing Pattern
- Redis-based job queue for long-running tasks
- Worker processes for CPU/GPU intensive operations
- Job status tracking and progress reporting
- Retry mechanisms for failed operations

### 4. Storage Abstraction
- MinIO for object storage (S3-compatible)
- PostgreSQL for structured data
- FAISS for vector similarity search
- Unified storage interface through adapters

### 5. Configuration Management
- Centralized configuration through `settings.py`
- Environment-based configuration
- YAML configuration files for complex settings
- Docker Compose for service orchestration

## Component Relationships

### Memory Processing Pipeline
1. **Upload**: Image uploaded via API
2. **Storage**: Stored in MinIO with UUID
3. **Queue**: Processing job queued in Redis
4. **Analysis**: YOLO-E extracts objects, Ollama generates descriptions
5. **Embedding**: Text descriptions converted to vectors
6. **Indexing**: Vectors stored in FAISS for search
7. **Metadata**: Results stored in PostgreSQL

### AI Integration Pattern
- **Vision Processing**: YOLO-E for object detection and scene understanding
- **Language Processing**: Ollama with Gemma3:12b for text generation
- **Multimodal**: Combined vision and language for rich descriptions
- **GPU Acceleration**: CUDA support for performance

## Data Flow Patterns

### Memory Upload Flow
```
Frontend → Backend API → Memory Service → MinIO Storage
                ↓
         Redis Queue → Worker → AI Processing → Database Update
```

### Search Flow
```
Query → Embedding Generation → FAISS Search → Database Lookup → Results
```

### AI Processing Flow
```
Image → YOLO-E Analysis → Object Detection → Text Description → LLM Processing → Rich Context
```

## Error Handling Patterns
- **Graceful Degradation**: System continues operating with reduced functionality
- **Retry Logic**: Automatic retry for transient failures
- **Circuit Breaker**: Prevents cascade failures
- **Comprehensive Logging**: Detailed logs for debugging

## Security Patterns
- **Input Validation**: Pydantic models validate all inputs
- **File Type Validation**: Strict image format checking
- **Size Limits**: Prevents resource exhaustion
- **Local Processing**: No external API calls for sensitive data





