# EventEye Certificate Automation System

## Overview

EventEye is an AI-powered certificate generation and delivery automation platform designed for event organizers. The system enables organizers to create professional certificates, verify participant names using AI, generate QR codes for authenticity, and track delivery status across multiple channels (email and WhatsApp). It provides a comprehensive dashboard for managing events, participants, certificate templates, and delivery analytics.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- React with TypeScript for type-safe component development
- Vite as the build tool and development server
- Wouter for lightweight client-side routing
- TanStack Query (React Query) for server state management and data fetching
- Tailwind CSS for utility-first styling with custom design tokens

**UI Component System:**
- Built on shadcn/ui component library using Radix UI primitives
- Custom design system following Material Design principles with Linear's data density
- Supports light/dark mode theming via ThemeProvider context
- Component path aliases configured for clean imports (@/components, @/lib, @/hooks)

**State Management Strategy:**
- React Query handles all server state with optimistic updates and cache invalidation
- Local UI state managed with React hooks (useState, useContext)
- Form state managed with React Hook Form and Zod validation
- Theme state persisted to localStorage

**Page Structure:**
- Dashboard: Event overview, delivery statistics, AI verification panel
- Certificates: Template builder with live preview
- Participants: Bulk upload, table management with search/filter
- Templates, Analytics, Settings: Placeholder routes for future expansion

### Backend Architecture

**Technology Stack:**
- Express.js server with TypeScript
- Drizzle ORM for database operations
- PostgreSQL database (Neon serverless driver)
- PDFKit for certificate PDF generation
- QRCode library for verification QR codes
- Multer for file upload handling (CSV/Excel participant lists)

**API Design:**
- RESTful API structure with resource-based endpoints
- Centralized error handling middleware
- Request/response logging for debugging
- CORS and security headers configured
- Session management (connect-pg-simple for session store)

**Data Flow:**
1. Client makes API requests through TanStack Query
2. Express routes validate request data using Zod schemas
3. Storage layer (MemStorage/Database) handles CRUD operations
4. Response data automatically cached by React Query
5. Optimistic updates provide immediate UI feedback

**Certificate Generation Pipeline:**
1. Participant data imported via CSV upload
2. AI verification suggests name corrections (confidence scoring)
3. Template applied with dynamic field replacement
4. PDF generated with PDFKit (A4 landscape format)
5. QR code embedded for authenticity verification
6. Certificate delivered via email/WhatsApp
7. Delivery status tracked (delivered, bounced, pending, opened)

### Database Schema

**Core Tables:**
- `events`: Event metadata (name, date, organizer)
- `certificate_templates`: Customizable certificate designs per event
- `participants`: Event attendee information with AI confidence scores
- `delivery_records`: Tracking delivery status, channels, and engagement

**Key Relationships:**
- Templates belong to events (1:N)
- Participants belong to events (1:N)
- Delivery records belong to participants (1:N)
- All tables use UUID primary keys for scalability

**Data Validation:**
- Drizzle Zod schemas auto-generated from table definitions
- Client and server share validation schemas via shared directory
- Type safety enforced end-to-end (database → API → UI)

### Design System

**Color Strategy:**
- HSL-based color tokens for light/dark mode compatibility
- Semantic color naming (primary, success, warning, destructive)
- Status-based colors for delivery tracking
- Custom CSS variables for elevation and borders

**Typography:**
- Inter font family for UI text
- JetBrains Mono for monospace data (IDs, codes)
- Responsive text scale (xs to 4xl)
- Dense data presentation with 1.5 line-height

**Layout System:**
- 280px fixed sidebar on desktop
- 12-column responsive grid with 4-unit gaps
- Consistent spacing scale (2, 4, 6, 8, 12, 16)
- Max-width constraints (max-w-7xl) for content readability

## External Dependencies

### Third-Party Services
- **Neon Database**: Serverless PostgreSQL hosting
- **Google Fonts**: Inter and JetBrains Mono font delivery
- **Email Service**: Certificate delivery (implementation pending)
- **WhatsApp Business API**: Alternative delivery channel (implementation pending)

### Key NPM Packages

**Core Framework:**
- `express`: Web server framework
- `react` + `react-dom`: UI library
- `typescript`: Type safety
- `vite`: Build tool and dev server

**Database & ORM:**
- `drizzle-orm`: Type-safe database toolkit
- `@neondatabase/serverless`: PostgreSQL driver
- `drizzle-kit`: Migration tooling

**UI Components:**
- `@radix-ui/*`: Accessible component primitives (dialog, dropdown, tabs, etc.)
- `@tanstack/react-query`: Server state management
- `tailwindcss`: Utility-first CSS framework
- `class-variance-authority`: Component variant management
- `wouter`: Lightweight routing

**Certificate Generation:**
- `pdfkit`: PDF document creation
- `qrcode`: QR code generation
- `canvas`: Server-side canvas rendering

**Form & Validation:**
- `react-hook-form`: Form state management
- `zod`: Schema validation
- `@hookform/resolvers`: Form/schema integration

**File Processing:**
- `multer`: Multipart form data handling
- `csv-parse`: CSV file parsing

**Developer Tools:**
- `@replit/vite-plugin-*`: Replit-specific dev tooling
- `tsx`: TypeScript execution
- `esbuild`: Production bundling

### Integration Points
- File uploads processed through Multer middleware
- CSV parsing converts participant lists to database records
- PDF generation creates certificates on-demand
- QR codes link to verification endpoints
- Session storage uses PostgreSQL for persistence