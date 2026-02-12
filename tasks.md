# Implementation Plan: VyapaarSetu AI

## Overview

This implementation plan follows a bottom-up approach, building foundational data models and core AI agents first, then composing them into services, and finally integrating with external platforms. The system is designed as an event-driven microservices architecture with specialized AI agents for vision, speech, language processing, customer interaction, and market intelligence.

**Implementation Strategy:**
1. Data models and core types
2. AI agent implementations (Vision, Speech, LLM, Customer, Pricing)
3. Agent orchestration layer
4. Core services (Listing, Search, Notification, Inventory, Order)
5. External integrations (ONDC, WhatsApp, Payment)
6. Offline sync and mobile optimization
7. End-to-end integration and testing

## Tasks

- [ ] 1. Set up project structure and foundational types
  - Create TypeScript project with microservices structure
  - Define core type definitions for BharatLanguage, Location, BusinessType enums
  - Set up testing frameworks (Jest for unit tests, fast-check for property tests)
  - Configure ESLint, Prettier, and TypeScript strict mode
  - Set up Docker Compose for local development environment
  - _Requirements: All (foundational)_

- [ ] 2. Implement core data models
  - [ ] 2.1 Create Seller data model
    - Implement Seller interface with validation
    - Add methods for language preference management
    - _Requirements: 15.3_
  
  - [ ] 2.2 Create Product Listing data model
    - Implement Listing interface with multilingual support
    - Add ListingTranslation structure for multiple languages
    - Implement ListingStatus state machine
    - _Requirements: 3.1, 3.2, 7.1_
  
  - [ ] 2.3 Create Conversation State data model
    - Implement ConversationState with message history
    - Add ConversationContext for tracking product/order references
    - Implement Message model with content type variants
    - _Requirements: 5.5, 9.4_
  
  - [ ] 2.4 Create Event models
    - Implement ListingCreatedEvent, OrderReceivedEvent, CustomerInquiryEvent
    - Add event metadata and timestamp tracking
    - _Requirements: 14.1, 14.2_
  
  - [ ] 2.5 Create ONDC data models
    - Implement ONDCCatalogEntry and ONDCItem interfaces
    - Add ONDC taxonomy mapping structures
    - _Requirements: 7.1, 7.2_
  
  - [ ]* 2.6 Write property test for data model validation
    - **Property 42: Seller Data Isolation**
    - **Validates: Requirements 15.3**

- [ ] 3. Implement Vision AI Agent
  - [ ] 3.1 Create VisionAIAgent interface and implementation
    - Implement analyzeProductImage using pre-trained model (ResNet/EfficientNet)
    - Add extractTextFromImage using OCR
    - Implement detectImageQuality with quality scoring
    - Implement generateImageEmbedding for vector search
    - _Requirements: 1.1, 1.4_
  
  - [ ]* 3.2 Write property test for image analysis completeness
    - **Property 1: Image Analysis Completeness**
    - **Validates: Requirements 1.1**
  
  - [ ]* 3.3 Write property test for multi-image aggregation
    - **Property 2: Multi-Image Information Aggregation**
    - **Validates: Requirements 1.2**
  
  - [ ]* 3.4 Write property test for low quality image handling
    - **Property 3: Low Quality Image Handling**
    - **Validates: Requirements 1.3**
  
  - [ ]* 3.5 Write property test for OCR text incorporation
    - **Property 4: OCR Text Incorporation**
    - **Validates: Requirements 1.4**
  
  - [ ]* 3.6 Write property test for compression preserving recognition
    - **Property 5: Compression Preserves Recognition**
    - **Validates: Requirements 1.5**

- [ ] 4. Implement Speech Processing Agent
  - [ ] 4.1 Create SpeechProcessingAgent interface and implementation
    - Implement transcribeVoice using Whisper or IndicWav2Vec
    - Add normalizeDialect for regional variation handling
    - Implement detectLanguage for automatic language detection
    - Add filterNoise for background noise removal
    - _Requirements: 2.1, 2.2, 2.3_
  
  - [ ]* 4.2 Write property test for language support coverage
    - **Property 6: Language Support Coverage**
    - **Validates: Requirements 2.4**
  
  - [ ]* 4.3 Write property test for ambiguous input clarification
    - **Property 7: Ambiguous Input Clarification**
    - **Validates: Requirements 2.5**
  
  - [ ]* 4.4 Write unit tests for noise filtering
    - Test various noise levels and audio quality scenarios
    - _Requirements: 2.3_

- [ ] 5. Implement Multilingual LLM Agent
  - [ ] 5.1 Create MultilingualLLMAgent interface and implementation
    - Implement generateListing with GPT-4 or Llama
    - Add translateContent for cross-language translation
    - Implement extractIntent for conversation understanding
    - Add generateResponse for contextual replies
    - _Requirements: 3.1, 3.2, 5.2_
  
  - [ ]* 5.2 Write property test for bilingual listing generation
    - **Property 9: Bilingual Listing Generation**
    - **Validates: Requirements 3.1, 3.2**
  
  - [ ]* 5.3 Write property test for marketplace format compliance
    - **Property 10: Marketplace Format Compliance**
    - **Validates: Requirements 3.3**
  
  - [ ]* 5.4 Write property test for voice-based listing edits
    - **Property 11: Voice-Based Listing Edits**
    - **Validates: Requirements 3.4**
  
  - [ ]* 5.5 Write property test for multilingual customer response
    - **Property 14: Multilingual Customer Response**
    - **Validates: Requirements 5.2**

- [ ] 6. Checkpoint - Core AI agents functional
  - Ensure all agent unit tests pass
  - Verify agents can be instantiated and called independently
  - Ask the user if questions arise

- [ ] 7. Implement Market Intelligence Agent
  - [ ] 7.1 Create MarketIntelligenceAgent interface and implementation
    - Implement suggestPricing with market data analysis
    - Add analyzeDemand for trend detection
    - Implement detectPriceAnomalies for outlier detection
    - Add explainPricing for human-readable explanations
    - _Requirements: 4.1, 4.2, 4.4_
  
  - [ ]* 7.2 Write property test for pricing suggestion generation
    - **Property 12: Pricing Suggestion Generation**
    - **Validates: Requirements 4.1**
  
  - [ ]* 7.3 Write property test for out-of-range price warnings
    - **Property 13: Out-of-Range Price Warnings**
    - **Validates: Requirements 4.5**
  
  - [ ]* 7.4 Write unit tests for demand analysis
    - Test with historical market data
    - _Requirements: 4.2_

- [ ] 8. Implement Customer Interaction Agent
  - [ ] 8.1 Create CustomerInteractionAgent interface and implementation
    - Implement handleCustomerQuery with context awareness
    - Add escalateToSeller for human handoff
    - Implement guidePurchase for checkout assistance
    - Add maintainContext for conversation tracking
    - _Requirements: 5.1, 5.3, 5.4, 5.5, 5.6_
  
  - [ ]* 8.2 Write property test for accurate product information retrieval
    - **Property 15: Accurate Product Information Retrieval**
    - **Validates: Requirements 5.3**
  
  - [ ]* 8.3 Write property test for seller escalation notification
    - **Property 16: Seller Escalation Notification**
    - **Validates: Requirements 5.4**
  
  - [ ]* 8.4 Write property test for conversation context preservation
    - **Property 17: Conversation Context Preservation**
    - **Validates: Requirements 5.5**
  
  - [ ]* 8.5 Write property test for autonomous WhatsApp customer handling
    - **Property 19: Autonomous WhatsApp Customer Handling**
    - **Validates: Requirements 6.3**

- [ ] 9. Implement Agent Orchestrator
  - [ ] 9.1 Create AgentOrchestrator interface and implementation
    - Implement orchestrateListingCreation coordinating Vision, Speech, LLM, Pricing agents
    - Add orchestrateCustomerQuery routing to appropriate agents
    - Implement handleAgentFailure with retry logic and exponential backoff
    - Add maintainConversationState for multi-turn interactions
    - _Requirements: 9.1, 9.2, 9.3, 9.4, 9.5_
  
  - [ ]* 9.2 Write property test for parallel agent execution
    - **Property 25: Parallel Agent Execution**
    - **Validates: Requirements 9.2**
  
  - [ ]* 9.3 Write property test for agent failure retry with exponential backoff
    - **Property 26: Agent Failure Retry with Exponential Backoff**
    - **Validates: Requirements 9.3**
  
  - [ ]* 9.4 Write property test for orchestrator state preservation
    - **Property 27: Orchestrator State Preservation**
    - **Validates: Requirements 9.4**
  
  - [ ]* 9.5 Write property test for agent conflict resolution
    - **Property 28: Agent Conflict Resolution**
    - **Validates: Requirements 9.5**

- [ ] 10. Checkpoint - Agent orchestration working
  - Ensure orchestrator can coordinate all agents
  - Test end-to-end listing creation flow
  - Ask the user if questions arise

- [ ] 11. Implement Listing Service
  - [ ] 11.1 Create ListingService interface and implementation
    - Implement createListing with database persistence
    - Add updateListing with optimistic locking
    - Implement publishListing to multiple marketplaces
    - Add generateONDCCatalog for ONDC compliance
    - _Requirements: 3.1, 7.1, 7.2_
  
  - [ ]* 11.2 Write property test for ONDC catalog completeness
    - **Property 20: ONDC Catalog Completeness**
    - **Validates: Requirements 7.1**
  
  - [ ]* 11.3 Write property test for ONDC category mapping validity
    - **Property 21: ONDC Category Mapping Validity**
    - **Validates: Requirements 7.2**
  
  - [ ]* 11.4 Write unit tests for listing lifecycle
    - Test draft → pending → active → inactive transitions
    - _Requirements: 3.1_

- [ ] 12. Implement Vector Search Service
  - [ ] 12.1 Create VectorSearchService interface and implementation
    - Implement indexListing with Pinecone or Weaviate
    - Add searchByText with multilingual support
    - Implement searchByImage for visual similarity
    - Add getSimilarProducts for recommendations
    - _Requirements: 10.1, 10.2, 10.3, 10.4, 10.5_
  
  - [ ]* 12.2 Write property test for multilingual vector search
    - **Property 29: Multilingual Vector Search**
    - **Validates: Requirements 10.2**
  
  - [ ]* 12.3 Write property test for embedding composition sensitivity
    - **Property 30: Embedding Composition Sensitivity**
    - **Validates: Requirements 10.3**
  
  - [ ]* 12.4 Write property test for zero-result search fallback
    - **Property 31: Zero-Result Search Fallback**
    - **Validates: Requirements 10.5**

- [ ] 13. Implement Event Bus and Event Sourcing
  - [ ] 13.1 Set up Kafka event bus infrastructure
    - Configure Kafka topics for different event types
    - Implement event publisher with at-least-once delivery
    - Add event consumer base class with error handling
    - _Requirements: 14.1, 14.2, 14.4, 14.5_
  
  - [ ] 13.2 Implement event sourcing for audit trail
    - Create event store with PostgreSQL
    - Add event replay functionality
    - Implement state reconstruction from events
    - _Requirements: 14.2, 14.3_
  
  - [ ]* 13.3 Write property test for event sourcing with audit trail
    - **Property 38: Event Sourcing with Audit Trail**
    - **Validates: Requirements 14.1, 14.2**
  
  - [ ]* 13.4 Write property test for event replay state recovery
    - **Property 39: Event Replay State Recovery**
    - **Validates: Requirements 14.3**
  
  - [ ]* 13.5 Write property test for at-least-once event delivery
    - **Property 40: At-Least-Once Event Delivery**
    - **Validates: Requirements 14.5**

- [ ] 14. Implement Notification Service
  - [ ] 14.1 Create NotificationService interface and implementation
    - Implement sendVoiceMessage via WhatsApp Business API
    - Add sendOrderNotification with priority handling
    - Implement sendTextNotification for multiple channels
    - Add queueNotification with priority queue
    - _Requirements: 6.2, 6.5, 7.5, 8.5_
  
  - [ ]* 14.2 Write property test for voice notification language consistency
    - **Property 18: Voice Notification Language Consistency**
    - **Validates: Requirements 6.2, 6.5, 7.5, 8.5**
  
  - [ ]* 14.3 Write unit tests for notification delivery
    - Test WhatsApp, SMS, and push notification channels
    - _Requirements: 6.2_

- [ ] 15. Implement Inventory Service
  - [ ] 15.1 Create InventoryService interface and implementation
    - Implement updateInventory with optimistic locking
    - Add syncInventoryAcrossMarketplaces for real-time sync
    - Implement checkAvailability for order validation
    - _Requirements: 7.4_
  
  - [ ]* 15.2 Write property test for cross-marketplace inventory synchronization
    - **Property 22: Cross-Marketplace Inventory Synchronization**
    - **Validates: Requirements 7.4**

- [ ] 16. Implement Order Service
  - [ ] 16.1 Create OrderService interface and implementation
    - Implement createOrder with inventory validation
    - Add processPayment integration
    - Implement notifySellerOfOrder via notification service
    - _Requirements: 5.6, 7.5_
  
  - [ ]* 16.2 Write unit tests for order processing
    - Test order creation, payment, and fulfillment flows
    - _Requirements: 5.6_

- [ ] 17. Checkpoint - Core services operational
  - Ensure all services can communicate via event bus
  - Test listing creation → search indexing → order flow
  - Ask the user if questions arise

- [ ] 18. Implement ONDC Adapter
  - [ ] 18.1 Create ONDCAdapter for catalog submission
    - Implement submitCatalog to ONDC network
    - Add updateCatalog for specification changes
    - Implement receiveOrder from ONDC marketplaces
    - Add catalog validation against ONDC schema
    - _Requirements: 7.1, 7.2, 7.3, 7.5_
  
  - [ ]* 18.2 Write unit tests for ONDC integration
    - Test catalog submission and order reception
    - Mock ONDC API endpoints
    - _Requirements: 7.1, 7.5_

- [ ] 19. Implement WhatsApp Business Adapter
  - [ ] 19.1 Create WhatsAppAdapter for commerce integration
    - Implement receiveMessage webhook handler
    - Add sendMessage for text and voice
    - Implement sendCatalog for product sharing
    - Add processPayment via WhatsApp Pay
    - _Requirements: 6.1, 6.2, 6.3, 6.4, 6.5_
  
  - [ ]* 19.2 Write integration tests for WhatsApp flows
    - Test image upload → listing creation via WhatsApp
    - Test customer inquiry → agent response via WhatsApp
    - _Requirements: 6.1, 6.3_

- [ ] 20. Implement Offline Sync Manager
  - [ ] 20.1 Create OfflineSyncManager interface and implementation
    - Implement queueOfflineAction with local storage
    - Add syncWhenOnline with connectivity detection
    - Implement resolveConflicts for sync conflicts
    - Add prioritizeSync for critical operations
    - _Requirements: 8.1, 8.2, 8.3, 8.4_
  
  - [ ]* 20.2 Write property test for offline data round-trip
    - **Property 23: Offline Data Round-Trip**
    - **Validates: Requirements 8.1, 8.2, 8.3**
  
  - [ ]* 20.3 Write property test for offline voice queueing round-trip
    - **Property 8: Offline Voice Queueing Round-Trip**
    - **Validates: Requirements 2.6**
  
  - [ ]* 20.4 Write property test for bandwidth-limited operation prioritization
    - **Property 24: Bandwidth-Limited Operation Prioritization**
    - **Validates: Requirements 8.4**

- [ ] 21. Implement low bandwidth optimizations
  - [ ] 21.1 Add data compression middleware
    - Implement request/response compression
    - Add image compression before upload
    - Implement progressive image loading
    - _Requirements: 12.1, 12.2, 12.4_
  
  - [ ]* 21.2 Write property test for data compression before transmission
    - **Property 33: Data Compression Before Transmission**
    - **Validates: Requirements 12.2**
  
  - [ ]* 21.3 Write property test for image compression size limit
    - **Property 35: Image Compression Size Limit**
    - **Validates: Requirements 12.4**

- [ ] 22. Implement caching layer
  - [ ] 22.1 Set up Redis cache infrastructure
    - Configure Redis for session state and data caching
    - Implement cache-aside pattern for frequently accessed data
    - Add cache invalidation on data updates
    - _Requirements: 12.3_
  
  - [ ]* 22.2 Write property test for cache hit for repeated requests
    - **Property 34: Cache Hit for Repeated Requests**
    - **Validates: Requirements 12.3**

- [ ] 23. Implement security and privacy controls
  - [ ] 23.1 Add encryption for data in transit and at rest
    - Configure TLS 1.3 for all API endpoints
    - Implement AES-256 encryption for stored data
    - Add encryption for voice recordings
    - _Requirements: 15.1_
  
  - [ ] 23.2 Implement role-based access control (RBAC)
    - Create middleware for seller data isolation
    - Add authorization checks on all data access
    - Implement audit logging for access attempts
    - _Requirements: 15.3_
  
  - [ ] 23.3 Add data retention and deletion policies
    - Implement automatic voice recording deletion after 30 days
    - Add data export functionality
    - Implement data deletion on user request
    - _Requirements: 15.2, 15.5_
  
  - [ ]* 23.4 Write property test for voice recording retention policy
    - **Property 41: Voice Recording Retention Policy**
    - **Validates: Requirements 15.2**
  
  - [ ]* 23.5 Write property test for data export and deletion
    - **Property 43: Data Export and Deletion**
    - **Validates: Requirements 15.5**

- [ ] 24. Checkpoint - Security and privacy verified
  - Run security audit and penetration tests
  - Verify RBAC prevents cross-seller data access
  - Ask the user if questions arise

- [ ] 25. Implement API Gateway and authentication
  - [ ] 25.1 Set up API Gateway with rate limiting
    - Configure API Gateway with request routing
    - Add rate limiting per seller
    - Implement request validation
    - _Requirements: All (infrastructure)_
  
  - [ ] 25.2 Implement authentication service
    - Add JWT-based authentication
    - Implement phone number verification
    - Add session management with Redis
    - _Requirements: 15.3_

- [ ] 26. Implement mobile app UI components
  - [ ] 26.1 Create mobile-first responsive layouts
    - Implement responsive design for 4-7 inch screens
    - Add large touch targets (44x44px minimum)
    - Implement portrait and landscape support
    - _Requirements: 11.1, 11.2, 11.5_
  
  - [ ] 26.2 Create voice and image input components
    - Implement camera integration for product photos
    - Add voice recording with visual feedback
    - Implement image preview and editing
    - _Requirements: 11.3_
  
  - [ ] 26.3 Implement listing management screens
    - Create listing creation flow
    - Add listing edit and review screens
    - Implement marketplace selection
    - _Requirements: 3.4, 11.4_
  
  - [ ]* 26.4 Write property test for UI element sizing standards
    - **Property 32: UI Element Sizing Standards**
    - **Validates: Requirements 11.2, 11.4**

- [ ] 27. Implement scalability and performance optimizations
  - [ ] 27.1 Add geographic data partitioning
    - Implement database sharding by region
    - Add region-based routing
    - Configure multi-region deployment
    - _Requirements: 13.3_
  
  - [ ] 27.2 Implement asynchronous processing with job queues
    - Set up SQS or RabbitMQ for async tasks
    - Add job workers for image and voice processing
    - Implement job status tracking
    - _Requirements: 13.4_
  
  - [ ] 27.3 Add auto-scaling configuration
    - Configure ECS auto-scaling policies
    - Add load balancer health checks
    - Implement circuit breakers for external services
    - _Requirements: 13.2_
  
  - [ ]* 27.4 Write property test for geographic data partitioning
    - **Property 36: Geographic Data Partitioning**
    - **Validates: Requirements 13.3**
  
  - [ ]* 27.5 Write property test for asynchronous input processing
    - **Property 37: Asynchronous Input Processing**
    - **Validates: Requirements 13.4**

- [ ] 28. Implement monitoring and observability
  - [ ] 28.1 Set up metrics collection
    - Configure CloudWatch or Prometheus for metrics
    - Add custom metrics for AI agent performance
    - Implement latency tracking (p50, p95, p99)
    - _Requirements: 13.5_
  
  - [ ] 28.2 Add structured logging
    - Implement JSON structured logging
    - Add correlation IDs for request tracing
    - Implement PII masking in logs
    - _Requirements: 15.1_
  
  - [ ] 28.3 Configure alerting
    - Set up PagerDuty for critical alerts
    - Add Slack notifications for warnings
    - Configure error rate spike detection
    - _Requirements: 13.5_

- [ ] 29. End-to-end integration testing
  - [ ]* 29.1 Test seller onboarding to listing creation flow
    - Test: Upload image → Voice description → Listing generated → ONDC published
    - _Requirements: 1.1, 2.1, 3.1, 7.1_
  
  - [ ]* 29.2 Test customer inquiry to resolution flow
    - Test: Customer query → Agent response → Escalation → Seller notification
    - _Requirements: 5.1, 5.4, 6.2_
  
  - [ ]* 29.3 Test offline to online sync flow
    - Test: Offline listing creation → Connectivity restored → Sync → Confirmation
    - _Requirements: 8.1, 8.2, 8.3, 8.5_
  
  - [ ]* 29.4 Test order placement and fulfillment flow
    - Test: ONDC order → Seller notification → Fulfillment → Customer update
    - _Requirements: 7.5, 6.5_

- [ ] 30. Performance and load testing
  - [ ]* 30.1 Run load tests for concurrent sellers
    - Test 10,000 concurrent sellers uploading images
    - Verify response times stay under 5 seconds
    - _Requirements: 13.1_
  
  - [ ]* 30.2 Run load tests for customer inquiries
    - Test 100,000 customer inquiries per minute
    - Verify agent response times under 30 seconds
    - _Requirements: 5.1, 13.1_
  
  - [ ]* 30.3 Run vector search performance tests
    - Test search across 1 million products
    - Verify search results within 2 seconds
    - _Requirements: 10.4_
  
  - [ ]* 30.4 Run event bus throughput tests
    - Test 100,000 events per second
    - Verify at-least-once delivery guarantee
    - _Requirements: 14.4_

- [ ] 31. Final checkpoint - System ready for deployment
  - Ensure all critical property tests pass (Properties 9, 20, 42, 23, 18)
  - Verify all integration tests pass
  - Run security audit and compliance checks
  - Ask the user if questions arise

## Notes

- Tasks marked with `*` are optional and can be skipped for faster MVP
- Each task references specific requirements for traceability
- Property tests validate universal correctness properties across all inputs
- Unit tests validate specific examples, edge cases, and integration points
- Checkpoints ensure incremental validation at major milestones
- Bottom-up approach ensures foundational components are solid before composition
- All property tests should run minimum 100 iterations with fast-check or Hypothesis
- Each property test must be tagged with: **Feature: vyapaarsetu-ai, Property {N}: {description}**
