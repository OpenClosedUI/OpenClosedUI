# OpenClosedUI Design Document

## Overview
OpenClosedUI is a framework for exposing and controlling user interfaces of applications that don't provide native APIs. The project aims to provide secure, flexible, and efficient ways to interact with various types of applications through UI automation.

### Applications

#### Dating Apps Swiper

Currently implemented as a module in the OpenClosedUI Android/iOS app using Kotlin Multiplatform, the dating apps swiper helps you get chicks online without wasting time on swiping like a retard. Focus on filtering the matches only. Later, we may expose Dating Apps Swiper as a separate Android/iOS app.

#### OpenClosedAI

OpenClosedAI exposes AI chats through an API by currently using Steel since most of them are available as a website. It allows to bring different chats such as but not limited to ChatGPT from ClosedAI, Gemini from Google, Claude from Anthropic to different applications. These include:
- OpenWebUI - allows checking different models side by side without having to pay for API per token to compare which is better
- OpenRouter - same idea
- MCP server - allows to give access to the services you pay subscription for to your IDE or other MCP compatible services without having to pay for API per token.

## Architecture

### Components

#### UI Gateway

UI gateway connects the controlled app in a safe way to a UI controller residing in the app such as OpenWebUI, Dating Apps Swiper inside OpenClosedUI Android/iOS app, etc. It exposes an API accessed by a token and allows only actions allowed in current user's configuration. For now, the configuration is simply in config but later may be stored in a KV storage to allow creating intermediate gateway providers so users can have flexibility without having to deploy their own version of UI gateway.

UI Gateway can controll the following things:
- Steel Browser whether 

### Possible Solutions

OpenClosedUI's architecture enables


<!-- everything below is based on brainstorming with AI: -->

## Core Components

### 1. Browser Control System
- **Technology Stack**: Steel Browser with Playwright (not puppeteer)
- **Deployment Options**:
  - Local Steel Browser deployment (we should consider that steel currently doesn't support multiple sessions, so it should be one deployment per OpenClosedAI/other service)
  - Personal server Steel Browser deployment (same concerns, we may extend Steel or build a separate Steel Orchestrator to mimick Steel Cloud)
  - Steel Cloud deployment (requires API key)
  - Can switch between deployment options as needed
- **Key Features**:
  - Browser automation with Steel Browser integration
  - Secure session management
  - HTTPS-based secure communication

### 2. Mobile App Control System
- **Technology Stack**: Kotlin Multiplatform
  - Shared business logic across platforms
- **App Selector Concept**:
  - Single OpenClosedUI app that can control multiple installed apps
  - Initial support for dating apps
  - Expandable to other app categories
- **Android Support**:
  - User intervention interface for complex interactions
  - Direct MediaProjection API access via DisplayManager
- **iOS Support**:
  - Use MultiPlatform unless features requre native APIs

### 3. Security Framework
- **Access Control**:
  - API key-based authentication
  - Encrypted data transfer
  - Rate limiting (can simply be done by using Cloudflare)

## Implementation Examples

### 1. Dating Apps Swiper (Android)
#### Architecture
- **Core Components**:
  - Profile Analyzer
  - Decision Engine
  - Action Executor

#### Feature Processing
- **Threshold System**:
  ```
  Feature Value < Acceptable Limit → Swipe Right (100%)
  Acceptable Limit ≤ Feature Value < No-Go-Zone → Swipe Right (58%), Left (42%)
  Feature Value ≥ No-Go-Zone → Swipe Left (100%)
  ```
  Default thresholds:
  - Age:
    * Acceptable limit: 36 (configurable)
    * No-go-zone: 42
  - Height:
    * Acceptable limit: 176 (configurable)
    * No-go-zone: 180

### 2. OpenClosedAI (Browser-based)
- Integration with OpenWebUI
- Integration with OpenRouter
- Integration with MCP
- Core functionality to be determined based on integration requirements

#### Security Considerations
- (default: true): Restrict to only OpenClosedAI initiated chats
  - Server won't access chats not prefixed by special phrase
  - Default phrase: 'OpenClosedAI: '
- TODO: Add more security options such as accessing settings, modifying them, etc

#### Integrations
- OpenWebUI integration:
  - Compare local models with ClosedAI, Google, Anthropic, Perplexity
  - Implement one-shot search across multiple AI chats and search engines
  - UI propagation using Steel Browser
  - Separate server providing API over Steel Browser using API key
- MCP integration:
  - TODO: Add details

## Implementation Phases

### Phase 1: Core Framework
- Ability to control an Android app
- Ability to support browser control system with Steel Browser
- Security framework with API key authentication
- API gateway

### Phase 2: Dating Apps Swiper Implementation
- Compose Multiplatform for shared UI components
- Kotlin Multiplatform business logic:
  - Profile analysis system
  - Decision engine
  - Feature processing
- Platform-specific integrations:
  - Android: MediaProjection API via native view
- Unified user intervention interface

### Phase 3: OpenClosedAI Implementation
- Steel Browser integration
- OpenWebUI integration
- MCP integration
- OpenRouter integration

## Development Guidelines
1. Follow SOLID principles
2. Implement comprehensive testing
3. Maintain security-first approach
4. Document all APIs and components (prefer documentation in the code + .md files to generate WEB version later)
5. Regular security audits

## Monitoring and Maintenance
1. Performance metrics
2. Security monitoring
3. Usage analytics
4. Error tracking
5. Regular updates and patches

## Communication Protocols
1. **FlatBuffers** - Primary serialization protocol
   - Zero-copy deserialization for high-performance rendering
   - Schema files (.fbs) will be version-controlled
   - Generated code for Python/TypeScript/React Native/Kotlin/Swift

## Core Processing Architecture

### OmniParser 2 Hybrid System
**Device Components**:
- Basic UI control/interaction
- Lightweight event detection
- Local session management

**Server Components**:
- OmniParser 2 heavy processing
- Complex decision making
- VRAM-intensive analysis

**Network Behavior**:
- Processing only during WiFi if we used up the limit set by the user
- Optimized data protocol

## Mobile Control Implementation

### Android System (MediaProjection API with Virtual Display)
**Key Features**:
- Low detection risk
- Standard Android APIs
- Vision-model compatible
