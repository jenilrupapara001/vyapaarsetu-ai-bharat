# VyapaarSetu AI

> Empowering Bharat's sellers through AI-driven commerce automation

VyapaarSetu AI is an autonomous commerce agent system that enables millions of small Indian sellers to participate in digital commerce by removing language barriers, technical complexity, and marketplace onboarding friction.

## Problem Statement

Millions of small Indian sellers cannot sell online due to:
- **Language barriers**: Most sellers speak only local languages and dialects
- **Technical knowledge gaps**: Complex marketplace interfaces require digital literacy
- **Onboarding complexity**: Multiple marketplaces with different requirements
- **Limited connectivity**: Rural areas have intermittent 2G/3G connections

## Solution

An AI-powered platform where sellers simply:
1. **Upload product photos** - Vision AI recognizes products automatically
2. **Speak in their language** - Voice input in 9 Indian languages with dialect support
3. **Let AI handle the rest** - Automatic listing generation, pricing, and customer service

## Key Features

### For Sellers
- 📸 **Image-to-Listing**: Upload photos, get complete product listings
- 🎤 **Voice-First Interface**: Speak in Hindi, Tamil, Telugu, Bengali, Marathi, Gujarati, Kannada, Malayalam, or Punjabi
- 💰 **Smart Pricing**: AI-powered market intelligence suggests competitive prices
- 🤖 **Autonomous Customer Service**: AI agent handles customer inquiries 24/7
- 📱 **WhatsApp Commerce**: Manage business through familiar WhatsApp interface
- 📡 **Offline Mode**: Work without internet, sync when connected
- 🌐 **Multi-Marketplace**: Automatic ONDC catalog generation for nationwide reach

### For Customers
- 🔍 **Semantic Search**: Find products using natural language in any supported language
- 💬 **Instant Responses**: AI agent answers questions immediately
- 🛒 **Guided Purchase**: Step-by-step checkout assistance

## Architecture

Event-driven microservices with multi-agent AI orchestration:

```
┌─────────────────────────────────────────────────────────────┐
│                     Client Layer                             │
│  Mobile App (React Native) | WhatsApp | Web Dashboard       │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                   API Gateway + Auth                         │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│              Agent Orchestration Layer                       │
│  • Agent Orchestrator  • Conversation State Manager         │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                    AI Agent Layer                            │
│  Vision AI | Speech Processing | Multilingual LLM           │
│  Customer Agent | Market Intelligence                       │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                  Core Services Layer                         │
│  Listing | Inventory | Order | Notification | Vector Search │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                  Integration Layer                           │
│  ONDC Adapter | WhatsApp Business | Payment Gateway         │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│                     Data Layer                               │
│  Kafka | PostgreSQL | MongoDB | Vector DB | Redis | S3      │
└─────────────────────────────────────────────────────────────┘
```

## Technology Stack

### AI Components
- **Vision AI**: ResNet/EfficientNet (fine-tuned on Indian products)
- **Speech-to-Text**: Whisper / IndicWav2Vec
- **Multilingual LLM**: GPT-4 / Llama (Indian language fine-tuning)
- **Vector Search**: Pinecone / Weaviate

### Backend
- **Runtime**: Node.js with TypeScript
- **Event Bus**: Apache Kafka
- **Databases**: PostgreSQL (transactional), MongoDB (flexible schemas)
- **Cache**: Redis
- **Storage**: AWS S3 / MinIO

### Frontend
- **Mobile**: React Native
- **State Management**: Redux Toolkit
- **Navigation**: React Navigation

### Infrastructure
- **Containerization**: Docker
- **Orchestration**: Kubernetes
- **Monitoring**: Prometheus + Grafana
- **Logging**: Winston + ELK Stack

## Project Structure

```
vyapaarsetu-ai/
├── .kiro/
│   └── specs/
│       └── vyapaarsetu-ai/
│           ├── requirements.md    # 15 requirements, 75 acceptance criteria
│           ├── design.md          # Architecture, components, data models
│           └── tasks.md           # 31 implementation tasks
├── packages/
│   ├── types/                     # Shared TypeScript types
│   ├── utils/                     # Common utilities
│   ├── config/                    # Configuration management
│   ├── vision-ai-agent/           # Vision AI service
│   ├── speech-agent/              # Speech processing service
│   ├── llm-agent/                 # Multilingual LLM service
│   ├── customer-agent/            # Customer interaction service
│   ├── market-intelligence/       # Pricing and market analysis
│   ├── orchestrator/              # Agent orchestration
│   ├── listing-service/           # Listing management
│   ├── inventory-service/         # Inventory tracking
│   ├── order-service/             # Order processing
│   ├── notification-service/      # Notifications (WhatsApp, SMS, push)
│   ├── vector-search/             # Semantic search
│   ├── api-gateway/               # API gateway and auth
│   └── mobile-app/                # React Native mobile app
├── infrastructure/
│   ├── docker-compose.yml         # Local development setup
│   └── kubernetes/                # K8s manifests
└── README.md
```

## Getting Started

### Prerequisites

- Node.js 18+ and pnpm
- Docker and Docker Compose
- PostgreSQL 15+
- MongoDB 6+
- Redis 7+
- Apache Kafka 3+

### Local Development Setup

1. **Clone the repository**
```bash
git clone https://github.com/your-org/vyapaarsetu-ai.git
cd vyapaarsetu-ai
```

2. **Install dependencies**
```bash
pnpm install
```

3. **Start infrastructure services**
```bash
docker-compose up -d
```

4. **Set up environment variables**
```bash
cp .env.example .env
# Edit .env with your API keys and configuration
```

5. **Run database migrations**
```bash
pnpm run migrate
```

6. **Start development servers**
```bash
pnpm run dev
```

### Running Tests

```bash
# Run all tests
pnpm test

# Run unit tests
pnpm test:unit

# Run property-based tests
pnpm test:property

# Run integration tests
pnpm test:integration

# Run end-to-end tests
pnpm test:e2e
```

## Implementation Roadmap

The project follows a bottom-up implementation approach with 31 tasks organized into phases:

### Phase 1: Foundation (Tasks 1-5)
- Project setup and infrastructure
- Core data models and types
- Database layer with geographic partitioning
- Event bus infrastructure with Kafka
- **Checkpoint**: Verify infrastructure

### Phase 2: AI Agents (Tasks 6-9)
- Vision AI agent for product recognition
- Speech processing agent with dialect support
- Multilingual LLM agent for listing generation
- Market intelligence agent for pricing

### Phase 3: Orchestration (Tasks 10-14)
- Customer interaction agent
- Agent orchestrator with parallel execution
- Vector search service
- **Checkpoint**: Verify core services

### Phase 4: Services (Tasks 15-20)
- Listing service with ONDC integration
- Inventory and order services
- Notification service
- WhatsApp interface
- **Checkpoint**: Verify services integration

### Phase 5: Optimization (Tasks 21-25)
- Offline sync manager
- Caching and compression
- API gateway and authentication
- Asynchronous processing
- **Checkpoint**: Verify backend complete

### Phase 6: Frontend & Security (Tasks 26-28)
- React Native mobile app
- Security and compliance
- Event replay and recovery

### Phase 7: Production Ready (Tasks 29-31)
- Monitoring and observability
- Integration testing
- **Final Checkpoint**: Complete system verification

See [tasks.md]([https://github.com/jenilrupapara001/vyapaarsetu-ai-bharat/blob/main/tasks.md]) for detailed task breakdown.

## Target Users

- 🌾 **Rural Entrepreneurs**: Farmers and artisans in villages
- 🏪 **Small Retailers**: Kirana stores and local shops
- 🏠 **Home-Based Businesses**: Women entrepreneurs running businesses from home
- 🏭 **Local Manufacturers**: Small-scale manufacturers and craftspeople
- 👩‍💼 **Women Entrepreneurs**: Women starting or growing their businesses

## Supported Languages

- Hindi (हिन्दी)
- Tamil (தமிழ்)
- Telugu (తెలుగు)
- Bengali (বাংলা)
- Marathi (मराठी)
- Gujarati (ગુજરાતી)
- Kannada (ಕನ್ನಡ)
- Malayalam (മലയാളം)
- Punjabi (ਪੰਜਾਬੀ)

## Non-Functional Requirements

- **Performance**: <5s response time for core operations
- **Scalability**: Support 10M+ active sellers
- **Availability**: 99.9% uptime SLA
- **Bandwidth**: Functional on 64 kbps (2G) connections
- **Offline**: Full offline mode with automatic sync
- **Security**: TLS 1.3, AES-256 encryption, PCI DSS compliance
- **Privacy**: GDPR/Indian data protection compliance

## Expected Impact

- 📈 **Income Growth**: Enable sellers to reach nationwide customers
- 🌐 **Digital Inclusion**: Bring millions of sellers online
- 💪 **Empowerment**: Remove technical and language barriers
- 🚀 **Scale**: Democratize access to digital commerce infrastructure
- 🇮🇳 **Bharat Focus**: Designed specifically for Indian market needs

## Documentation

- [Requirements Document](.kiro/specs/vyapaarsetu-ai/requirements.md) - Detailed requirements and acceptance criteria
- [Design Document](.kiro/specs/vyapaarsetu-ai/design.md) - Architecture, components, and data models
- [Implementation Plan](.kiro/specs/vyapaarsetu-ai/tasks.md) - Task breakdown and execution plan

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

[MIT License](LICENSE)

## Contact

- **Project Lead**: [Your Name]
- **Email**: contact@vyapaarsetu.ai
- **Website**: https://vyapaarsetu.ai

---

**VyapaarSetu AI** - Bridging Bharat to Digital Commerce 🇮🇳
