# EYE Codebase Analysis - Complete File Documentation

## Project Overview
EYE is an AI-first computer vision workspace for preserving memories and enabling intelligent conversations with personal photo/video collections. The system transforms traditional photo storage into an intelligent memory vault using advanced AI models.

## Architecture Summary
- **Backend**: FastAPI with Python, PostgreSQL, Redis, MinIO
- **Frontend**: Next.js with TypeScript, Tailwind CSS
- **AI/ML**: YOLO-E for object detection, Ollama for LLM processing
- **Infrastructure**: Docker Compose with GPU support
- **Storage**: MinIO for objects, FAISS for vectors, PostgreSQL for metadata

---

## Backend Structure (`/backend/`)

### Core Application Files

#### `main.py`
**Purpose**: FastAPI application entry point
**Key Features**:
- Main FastAPI app with CORS middleware
- Watermark header for branding
- Router registration for all API modules
- Custom exception handling for validation errors
**Usage**: Serves as the central API server, handling all HTTP requests

#### `config.py`
**Purpose**: Configuration import wrapper
**Key Features**:
- Imports centralized settings from `settings.py`
- Provides global settings access
**Usage**: Simple configuration access point

#### `settings.py`
**Purpose**: Centralized application settings
**Key Features**:
- Pydantic-based settings management
- Environment variable integration
- Database, Redis, MinIO, CVAT configuration
- JWT and security settings
**Usage**: Single source of truth for all application configuration

### API Modules (`/backend/api/`)

#### `routes.py`
**Purpose**: Core API routes and utilities
**Key Features**:
- Authentication endpoints
- File upload handling
- CVAT integration endpoints
- S3/MinIO adapter integration
**Usage**: Handles basic API operations and external service integration

#### `memory.py`
**Purpose**: Memory management API endpoints
**Key Features**:
- Memory upload and processing
- Search functionality with natural language
- Memory retrieval and management
- Background job processing
- Chat with memories feature
**Usage**: Core memory system API for image processing and retrieval

#### `yolo_e.py`
**Purpose**: YOLO-E object detection API
**Key Features**:
- Model loading and management
- Training job management
- Dataset upload and management
- Single and batch inference
- Base class retrieval
**Usage**: Computer vision processing for object detection and scene understanding

#### `ollama.py`
**Purpose**: LLM and vision model API
**Key Features**:
- Chat and text generation
- Vision processing with images
- Model management
- Streaming responses
- Health checks
**Usage**: Language model integration for AI conversations and descriptions

#### `annotations.py`
**Purpose**: Annotation system API
**Key Features**:
- CVAT integration
- Annotation project management
- Task creation and management
- Webhook handling
**Usage**: Integration with external annotation tools for data labeling

#### `jobs.py`
**Purpose**: Job management API
**Key Features**:
- Job status tracking
- Queue management
- Background task monitoring
**Usage**: Manages long-running background tasks

#### `queue.py`
**Purpose**: Queue management API
**Key Features**:
- Redis queue operations
- Job queuing and processing
- Queue status monitoring
**Usage**: Handles background job queuing and processing

#### `metrics.py`
**Purpose**: System metrics API
**Key Features**:
- Prometheus metrics
- System health monitoring
- Performance metrics
**Usage**: Monitoring and observability for the system

### Services (`/backend/services/`)

#### `memory_service.py`
**Purpose**: Core memory processing service
**Key Features**:
- Image upload and storage in MinIO
- FAISS vector index management
- PostgreSQL database operations
- AI description generation
- Memory search and retrieval
- Embedding generation
**Usage**: Central service for all memory-related operations

#### `memory_processing_service.py`
**Purpose**: Background memory processing
**Key Features**:
- Job queuing for memory processing
- Integration with YOLO-E and Ollama
- Processing status tracking
- Error handling and retry logic
**Usage**: Handles background processing of uploaded memories

#### `ollama_service.py`
**Purpose**: Ollama LLM service integration
**Key Features**:
- HTTP client for Ollama API
- Model management and pulling
- Chat and text generation
- Vision processing
- Streaming support
**Usage**: Service layer for LLM operations

#### `cvat_integration.py`
**Purpose**: CVAT annotation tool integration
**Key Features**:
- Project and task management
- Data import/export
- Webhook handling
**Usage**: Integration with external annotation tools

#### `jobs.py`
**Purpose**: Job management service
**Key Features**:
- Job creation and tracking
- Status updates
- Error handling
**Usage**: Manages background job lifecycle

#### `queue.py`
**Purpose**: Queue management service
**Key Features**:
- Redis queue operations
- Job processing
- Queue monitoring
**Usage**: Handles job queuing and processing

### Database Schemas (`/backend/schemas/`)

#### `auth.py`
**Purpose**: Authentication schemas
**Key Features**:
- User models
- Token schemas
- Authentication requests/responses
**Usage**: Data validation for authentication operations

---

## Frontend Structure (`/frontend/`)

### Core Application Files

#### `package.json`
**Purpose**: Frontend dependencies and scripts
**Key Features**:
- Next.js 14 with TypeScript
- Tailwind CSS for styling
- TanStack Query for data fetching
- Zustand for state management
- React Dropzone for file uploads
**Usage**: Defines frontend technology stack and build scripts

#### `next.config.js`
**Purpose**: Next.js configuration
**Key Features**:
- Development and production settings
- API proxy configuration
- Build optimization
**Usage**: Configures Next.js application behavior

#### `tailwind.config.js`
**Purpose**: Tailwind CSS configuration
**Key Features**:
- Custom design system
- Color palette
- Component styling
**Usage**: Defines styling system for the application

### Application Pages (`/frontend/src/app/`)

#### `page.tsx`
**Purpose**: Main landing page
**Key Features**:
- Hero section with project description
- Feature showcase
- Navigation and branding
- Call-to-action buttons
**Usage**: Main entry point for users, showcases project capabilities

#### `layout.tsx`
**Purpose**: Application layout wrapper
**Key Features**:
- Global layout structure
- Navigation components
- Theme management
**Usage**: Provides consistent layout across all pages

#### `eye-ai/page.tsx`
**Purpose**: EYE AI chat interface
**Key Features**:
- AI conversation interface
- Memory integration
- Chat history
**Usage**: Main interface for AI conversations about memories

#### `memory/page.tsx`
**Purpose**: Memory management interface
**Key Features**:
- Memory upload and display
- Search functionality
- Memory organization
**Usage**: Interface for managing personal memory collection

#### `annotation/page.tsx`
**Purpose**: Annotation interface
**Key Features**:
- Image annotation tools
- CVAT integration
- Label management
**Usage**: Interface for data annotation and labeling

#### `inference/page.tsx`
**Purpose**: Model inference interface
**Key Features**:
- Model testing interface
- Inference results display
- Parameter configuration
**Usage**: Interface for testing AI models

#### `training/page.tsx`
**Purpose**: Model training interface
**Key Features**:
- Training job management
- Dataset upload
- Training progress monitoring
**Usage**: Interface for training custom AI models

### Feature Modules (`/frontend/src/features/`)

#### Memory Features (`/features/memory/`)
- **Components**: Memory upload, display, search interfaces
- **Hooks**: Custom hooks for memory operations
- **API**: Memory service integration
**Usage**: Complete memory management functionality

#### EYE AI Features (`/features/eye-ai/`)
- **Components**: Chat interface, AI responses
- **Hooks**: AI service integration
- **API**: Ollama service integration
**Usage**: AI conversation and interaction features

#### Inference Features (`/features/inference/`)
- **Components**: Model testing interface
- **Hooks**: Inference operations
- **API**: YOLO-E service integration
**Usage**: Model testing and inference functionality

#### Annotation Features (`/features/annotations/`)
- **Components**: Annotation tools, canvas
- **Hooks**: Annotation operations
- **API**: CVAT integration
**Usage**: Data annotation and labeling tools

#### Projects Features (`/features/projects/`)
- **Components**: Project management
- **Hooks**: Project operations
- **API**: Project service integration
**Usage**: Project organization and management

#### Training Features (`/features/training/`)
- **Components**: Training interface
- **Hooks**: Training operations
- **API**: Training service integration
**Usage**: Model training functionality

#### YOLO-E Features (`/features/yolo_e/`)
- **Components**: YOLO-E interface
- **Hooks**: YOLO-E operations
- **API**: YOLO-E service integration
**Usage**: YOLO-E model management and testing

### Shared Components (`/frontend/src/shared/`)

#### Components (`/shared/components/`)
- **Button.tsx**: Reusable button component
- **index.ts**: Component exports
**Usage**: Shared UI components across the application

#### Hooks (`/shared/hooks/`)
- **useAuth.ts**: Authentication hook
- **index.ts**: Hook exports
**Usage**: Shared custom hooks for common functionality

#### Types (`/shared/types/`)
- **index.ts**: TypeScript type definitions
**Usage**: Shared type definitions across the application

---

## Engine Components (`/engines/`)

#### `base.py`
**Purpose**: Base engine interface
**Key Features**:
- Abstract base class for all engines
- Common interface methods
- Engine lifecycle management
**Usage**: Foundation for all AI engine implementations

#### `yolo_e_node.py`
**Purpose**: YOLO-E engine implementation
**Key Features**:
- YOLO-E model loading and inference
- Few-shot learning capabilities
- Batch processing support
- GPU acceleration
**Usage**: Computer vision processing engine

#### `custom_node.py`
**Purpose**: Custom engine implementation
**Key Features**:
- Custom model support
- Flexible inference pipeline
**Usage**: Support for custom AI models

#### `forge_node.py`
**Purpose**: Forge engine implementation
**Key Features**:
- Forge model integration
- Specialized processing
**Usage**: Integration with Forge AI models

#### `spectra_node.py`
**Purpose**: Spectra engine implementation
**Key Features**:
- Spectra model integration
- Advanced processing capabilities
**Usage**: Integration with Spectra AI models

#### `ultra_node.py`
**Purpose**: Ultra engine implementation
**Key Features**:
- Ultra model integration
- High-performance processing
**Usage**: Integration with Ultra AI models

---

## Infrastructure (`/orchestrator/`)

#### `dispatcher.py`
**Purpose**: Job dispatcher
**Key Features**:
- Job routing and distribution
- Load balancing
- Priority management
**Usage**: Manages job distribution across workers

#### `scheduler.py`
**Purpose**: Job scheduler
**Key Features**:
- Job scheduling and timing
- Cron-like functionality
- Resource management
**Usage**: Schedules and manages job execution

#### `monitor.py`
**Purpose**: System monitoring
**Key Features**:
- System health monitoring
- Performance metrics
- Alert management
**Usage**: Monitors system health and performance

#### `workers/redis_worker.py`
**Purpose**: Redis-based worker
**Key Features**:
- Redis queue processing
- Job execution
- Status tracking
**Usage**: Processes background jobs from Redis queue

#### `workers/simple_worker.py`
**Purpose**: Simple worker implementation
**Key Features**:
- Basic job processing
- Error handling
**Usage**: Simple background job processing

#### `workers/yolo_e_worker.py`
**Purpose**: YOLO-E specialized worker
**Key Features**:
- YOLO-E job processing
- GPU resource management
- Model loading optimization
**Usage**: Specialized worker for YOLO-E operations

---

## Storage Layer (`/storage/`)

#### `adapters/s3.py`
**Purpose**: S3-compatible storage adapter
**Key Features**:
- MinIO/S3 integration
- File upload/download
- Bucket management
- Metadata handling
**Usage**: Abstraction layer for object storage operations

---

## Configuration (`/config/`)

#### `eye.yaml`
**Purpose**: Centralized configuration
**Key Features**:
- Service configuration
- AI/ML settings
- Security configuration
- Feature flags
**Usage**: Single source of truth for system configuration

#### `docker-compose.generated.yml`
**Purpose**: Generated Docker Compose configuration
**Key Features**:
- Service definitions
- Network configuration
- Volume management
**Usage**: Generated Docker Compose file for deployment

#### `PORT_MAPPING.md`
**Purpose**: Port mapping documentation
**Key Features**:
- Service port definitions
- Port conflict resolution
**Usage**: Documentation for service port assignments

---

## Monitoring (`/monitoring/`)

#### `prometheus/`
**Purpose**: Prometheus monitoring setup
**Key Features**:
- Metrics collection
- Alerting rules
- Dashboard configuration
**Usage**: System monitoring and observability

#### `exporters/health_exporter.py`
**Purpose**: Health metrics exporter
**Key Features**:
- Health check metrics
- Service status monitoring
**Usage**: Exports health metrics for monitoring

#### `alerts/`
**Purpose**: Alert configuration
**Key Features**:
- Alert rules
- Notification channels
**Usage**: System alerting configuration

#### `dashboards/`
**Purpose**: Dashboard configuration
**Key Features**:
- Grafana dashboards
- Visualization configuration
**Usage**: Monitoring dashboard setup

---

## Scripts (`/scripts/`)

#### `generate-config.py`
**Purpose**: Configuration generation
**Key Features**:
- Dynamic config generation
- Environment-specific settings
**Usage**: Generates configuration files for deployment

#### `setup_ollama.py`
**Purpose**: Ollama setup script
**Key Features**:
- Ollama installation
- Model downloading
- Configuration setup
**Usage**: Sets up Ollama service and models

#### `download_yolo_e_weights.py`
**Purpose**: YOLO-E model download
**Key Features**:
- Model weight downloading
- Verification
**Usage**: Downloads YOLO-E model weights

#### `test_*.py`
**Purpose**: Various test scripts
**Key Features**:
- API testing
- System testing
- Integration testing
**Usage**: Testing and validation scripts

---

## Documentation (`/docs/`)

#### `API_REFERENCE.md`
**Purpose**: API documentation
**Key Features**:
- Endpoint documentation
- Request/response examples
- Authentication guide
**Usage**: Complete API reference for developers

#### `DEPLOYMENT.md`
**Purpose**: Deployment guide
**Key Features**:
- Installation instructions
- Configuration guide
- Troubleshooting
**Usage**: Deployment and setup documentation

#### `CONFIGURATION.md`
**Purpose**: Configuration guide
**Key Features**:
- Configuration options
- Environment variables
- Service configuration
**Usage**: Configuration documentation

#### `OLLAMA_*.md`
**Purpose**: Ollama integration documentation
**Key Features**:
- Ollama setup
- Model configuration
- Integration guide
**Usage**: Ollama service documentation

#### `YOLO_E_*.md`
**Purpose**: YOLO-E integration documentation
**Key Features**:
- YOLO-E setup
- Model configuration
- Usage examples
**Usage**: YOLO-E service documentation

---

## Business Documentation (`/business/`)

#### `README.md`
**Purpose**: Business overview
**Key Features**:
- Business model
- Market analysis
- Strategy overview
**Usage**: Business context and strategy

#### `models/BUSINESS_MODEL.md`
**Purpose**: Business model documentation
**Key Features**:
- Revenue streams
- Value proposition
- Market positioning
**Usage**: Business model definition

#### `strategies/PARTNERSHIP_PROGRAM.md`
**Purpose**: Partnership strategy
**Key Features**:
- Partnership opportunities
- Collaboration models
- Integration strategies
**Usage**: Partnership and collaboration strategy

#### `case-studies/CUSTOMER_SUCCESS.md`
**Purpose**: Customer success stories
**Key Features**:
- Use cases
- Success metrics
- Customer testimonials
**Usage**: Customer success documentation

---

## Key Usage Patterns

### Memory Processing Flow
1. **Upload**: User uploads image via frontend
2. **Storage**: Image stored in MinIO with UUID
3. **Queue**: Processing job queued in Redis
4. **Analysis**: YOLO-E extracts objects, Ollama generates descriptions
5. **Embedding**: Text descriptions converted to vectors
6. **Indexing**: Vectors stored in FAISS for search
7. **Metadata**: Results stored in PostgreSQL

### AI Integration Pattern
- **Vision Processing**: YOLO-E for object detection
- **Language Processing**: Ollama for text generation
- **Multimodal**: Combined vision and language processing
- **GPU Acceleration**: CUDA support throughout

### Service Communication
- **Internal**: Docker network with service discovery
- **External**: REST APIs with proper authentication
- **Background**: Redis queue for job processing
- **Storage**: MinIO for objects, PostgreSQL for metadata

This comprehensive analysis shows EYE as a well-architected system with clear separation of concerns, robust AI integration, and a focus on privacy-first local processing. The codebase demonstrates professional development practices with proper documentation, testing infrastructure, and scalable architecture.





