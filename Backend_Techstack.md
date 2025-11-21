# InvestLearn Backend Technology Stack

**Last Updated:** 2024  
**Purpose:** Comprehensive overview of all technologies, frameworks, and tools used in the InvestLearn backend

---

## Core Runtime & Language

### **Node.js**
- **Version:** v18 or higher (as specified in README)
- **Runtime:** JavaScript runtime built on Chrome's V8 engine
- **Usage:** Server-side application runtime

### **TypeScript**
- **Version:** ^5.7.3
- **Purpose:** Type-safe JavaScript with static typing
- **Configuration:** `tsconfig.json` with strict mode enabled
- **Features Used:**
  - Decorators (`experimentalDecorators: true`)
  - Metadata reflection (`emitDecoratorMetadata: true`)
  - ES2022 target
  - CommonJS modules

---

## Web Framework

### **Express.js**
- **Version:** ^4.21.2
- **Purpose:** Web application framework for Node.js
- **Usage:** HTTP server, middleware, routing foundation

### **Routing Controllers**
- **Version:** ^0.10.4
- **Purpose:** Decorator-based routing and controller organization
- **Features:**
  - Class-based controllers with decorators
  - Automatic route registration
  - Middleware integration
  - OpenAPI/Swagger integration

---

## Database & ORM

### **PostgreSQL**
- **Database:** PostgreSQL (relational database)
- **Connection:** Using `pg` library (^8.13.1)
- **Features:**
  - Connection pooling
  - SSL support
  - Transaction support

### **Drizzle ORM**
- **Version:** ^0.39.2 (drizzle-orm)
- **Version:** ^0.30.4 (drizzle-kit)
- **Purpose:** Type-safe ORM for PostgreSQL
- **Features:**
  - TypeScript-first ORM
  - Migration management
  - Query builder
  - Transaction support
  - Schema management

---

## Dependency Injection

### **InversifyJS**
- **Version:** ^6.2.2
- **Purpose:** Dependency injection container for TypeScript
- **Usage:**
  - Service registration and resolution
  - Controller dependency injection
  - Modular architecture
- **Integration:** Custom adapter for routing-controllers

---

## Authentication & Security

### **Firebase Admin SDK**
- **Version:** ^13.4.0
- **Purpose:** Server-side Firebase authentication
- **Usage:**
  - Token verification
  - User authentication
  - Firebase Auth integration

### **Helmet**
- **Version:** ^8.1.0
- **Purpose:** Security headers middleware
- **Features:**
  - XSS protection
  - Content Security Policy
  - HTTP security headers

### **Express Rate Limit**
- **Version:** ^8.1.0
- **Purpose:** Rate limiting middleware
- **Usage:** API request throttling

### **CORS**
- **Version:** ^2.8.5
- **Purpose:** Cross-Origin Resource Sharing
- **Configuration:** Custom CORS with wildcard support for Vercel

---

## Validation & Data Transformation

### **Class Validator**
- **Version:** ^0.14.1
- **Purpose:** Decorator-based validation
- **Usage:** Request validation, DTO validation

### **Class Transformer**
- **Version:** ^0.5.1
- **Purpose:** Object transformation and serialization
- **Usage:** DTO transformation, response serialization

### **Zod**
- **Version:** ^3.24.1
- **Purpose:** Schema validation library
- **Usage:** Runtime type validation, schema definition

---

## AI & External APIs

### **OpenAI SDK**
- **Version:** ^6.1.0
- **Purpose:** AI-powered financial assistant
- **Usage:**
  - Chat functionality
  - Personalized financial advice
  - Content generation

### **Alpha Vantage**
- **Version:** ^2.5.0
- **Purpose:** Financial market data API
- **Usage:**
  - Stock data
  - ETF data
  - Market analysis

---

## Caching & Performance

### **Redis**
- **Libraries:**
  - `redis`: ^5.5.6
  - `ioredis`: ^5.6.1
- **Purpose:** In-memory data store
- **Usage:**
  - Caching
  - Session management
  - Rate limiting storage

---

## Logging

### **Winston**
- **Version:** ^3.17.0
- **Purpose:** Logging library
- **Features:**
  - Multiple log levels
  - Structured logging
  - Pretty printing for development
  - Custom loggers

---

## API Documentation

### **OpenAPI / Swagger**
- **Libraries:**
  - `openapi3-ts`: 3.2.0
  - `routing-controllers-openapi`: ^4.1.0
  - `swagger-ui-express`: ^5.0.1
- **Purpose:** API documentation and interactive API explorer
- **Usage:** Auto-generated OpenAPI schema from controllers

---

## Development Tools

### **TypeScript Compiler**
- **tsc-watch**: ^6.2.1 (watch mode for development)
- **ts-node**: ^10.9.2 (TypeScript execution)

### **Code Quality**
- **ESLint**: ^9.20.0
  - `@typescript-eslint/eslint-plugin`: ^8.23.0
  - `@typescript-eslint/parser`: ^8.23.0
  - `eslint-config-prettier`: ^10.0.1
  - `eslint-plugin-prettier`: ^5.2.3
- **Prettier**: ^3.4.2 (code formatting)

### **Module Aliases**
- **module-alias**: ^2.2.3
- **Purpose:** Path aliases (`@/*` for `src/*`)

### **Source Maps**
- **source-map-support**: ^0.5.21
- **Purpose:** Better error stack traces in production

---

## Utilities

### **UUID**
- **Version:** ^11.0.5
- **Purpose:** Unique identifier generation

### **Dotenv**
- **Version:** ^16.4.7
- **Purpose:** Environment variable management

### **Reflect Metadata**
- **Version:** ^0.2.2
- **Purpose:** Metadata reflection for decorators (required by Inversify)

---

## Architecture Patterns

### **Dependency Injection (DI)**
- **Pattern:** InversifyJS container
- **Benefits:**
  - Loose coupling
  - Testability
  - Modular design

### **Decorator-Based Routing**
- **Pattern:** Routing Controllers
- **Benefits:**
  - Clean controller code
  - Automatic route registration
  - Middleware composition

### **Repository Pattern**
- **Pattern:** Service layer abstraction
- **Benefits:**
  - Business logic separation
  - Database abstraction

### **DTO Pattern**
- **Pattern:** Data Transfer Objects
- **Benefits:**
  - Type safety
  - Validation
  - API contract definition

---

## Project Structure

```
src/
├── controllers/     # Route controllers (routing-controllers)
├── modules/        # Business logic modules
├── dto/            # Data Transfer Objects
├── models/         # Database models (Drizzle ORM)
├── db/             # Database configuration & helpers
├── middlewares/    # Express middlewares
├── config/         # Configuration files
├── utils/          # Utility functions
│   └── di/         # Dependency Injection setup
├── services/       # Service layer
└── errors/         # Custom error classes
```

---

## Development Workflow

### **Scripts**
- `npm run dev` - Development server with watch mode
- `npm run build` - TypeScript compilation
- `npm run start` - Production server
- `npm run db:migrate` - Run database migrations
- `npm run db:generate` - Generate migrations
- `npm run db:studio` - Drizzle Studio (database GUI)
- `npm run lint` - ESLint checking
- `npm run format` - Prettier formatting

### **Code Generation**
- `npm run gen:controller` - Generate controller template
- `npm run gen:module` - Generate module template

---

## Deployment

### **Environment**
- **Platform:** Render (based on `render.yaml`)
- **Database:** PostgreSQL (managed)
- **Frontend:** Vercel (based on CORS config)

### **Docker**
- **Dockerfile:** Present in project
- **docker-compose.yml:** Local development setup

---

## Security Features

1. **Firebase Authentication** - Token-based auth
2. **Helmet** - Security headers
3. **Rate Limiting** - API throttling
4. **Input Sanitization** - XSS protection
5. **CORS** - Cross-origin protection
6. **Request Size Limits** - DoS protection
7. **Audit Logging** - Security monitoring

---

## Key Integrations

1. **Firebase** - Authentication
2. **OpenAI** - AI chat assistant
3. **Alpha Vantage** - Market data
4. **PostgreSQL** - Primary database
5. **Redis** - Caching (optional)

---

## Technology Highlights

### **Type Safety**
- Full TypeScript coverage
- Drizzle ORM provides type-safe queries
- Class-validator for runtime validation
- Zod for schema validation

### **Modern Patterns**
- Decorator-based architecture
- Dependency injection
- Modular design
- Service-oriented architecture

### **Developer Experience**
- Hot reload (tsc-watch)
- Auto-generated API docs
- Code generation scripts
- Comprehensive logging

### **Scalability**
- Connection pooling (PostgreSQL)
- Redis caching support
- Rate limiting
- Modular architecture

---

## Summary

**Core Stack:**
- **Runtime:** Node.js + TypeScript
- **Framework:** Express.js + Routing Controllers
- **Database:** PostgreSQL + Drizzle ORM
- **DI:** InversifyJS
- **Auth:** Firebase Admin
- **AI:** OpenAI
- **Validation:** Class-validator + Zod
- **Logging:** Winston
- **Docs:** OpenAPI/Swagger

**Architecture Style:**
- Decorator-based controllers
- Dependency injection
- Service layer pattern
- DTO pattern
- Repository pattern

**Key Strengths:**
- ✅ Type-safe end-to-end
- ✅ Modern TypeScript patterns
- ✅ Well-structured architecture
- ✅ Comprehensive security
- ✅ Developer-friendly tooling

---

**End of Tech Stack Documentation**

