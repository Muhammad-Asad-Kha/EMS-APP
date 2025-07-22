# Equipment Management System (EMS) - EquipTrack

## Overview

EquipTrack is a comprehensive React-based Equipment Management System designed to streamline equipment tracking, user management, and maintenance operations. The application features role-based access control with user and admin roles, real-time data management through Firebase, and a responsive UI built with modern web technologies.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript for type safety and modern component development
- **Routing**: Wouter for lightweight client-side routing
- **UI Framework**: Tailwind CSS with shadcn/ui components for consistent, accessible design
- **State Management**: React Query (TanStack Query) for server state management and caching
- **Build Tool**: Vite for fast development and optimized production builds

### Backend Architecture
- **Server**: Express.js with TypeScript for API endpoints
- **Database**: PostgreSQL with Drizzle ORM for type-safe database operations
- **Authentication**: Firebase Authentication for secure user management
- **Data Storage**: Hybrid approach using Firebase Firestore for real-time data and PostgreSQL for structured data

### Authentication Strategy
- Firebase Authentication handles user login/signup with email/password
- Role-based access control (RBAC) with 'user' and 'admin' roles
- User data stored in both Firebase (for auth) and local database (for app-specific data)
- Protected routes with authentication state management through React Context

## Key Components

### Data Models
The application manages four primary entities:
1. **Users**: Authentication, profile information, and role assignments
2. **Equipment**: Asset tracking with status management (available, checked_out, maintenance, retired)
3. **Checkouts**: Equipment lending records with return tracking
4. **Maintenance Logs**: Service requests and maintenance history

### Core Features
- **Dashboard**: Real-time statistics, equipment status charts, and activity feeds
- **Equipment Management**: CRUD operations for equipment with status tracking
- **Checkout System**: Equipment lending with due date management and return processing
- **Maintenance Tracking**: Service request submission and maintenance scheduling
- **User Management**: Basic user listing for all users, enhanced admin controls
- **Admin Panel**: Advanced user management, reporting, and system configuration

### UI/UX Design
- Responsive design optimized for desktop and mobile devices
- Sidebar navigation with role-based menu items
- Top bar with global search, quick actions, and user profile management
- Consistent component library using shadcn/ui with Tailwind CSS styling

## Data Flow

### Authentication Flow
1. User submits login credentials through Firebase Auth
2. Firebase returns authentication token and user data
3. Application fetches additional user data from Firestore
4. User context provides authentication state throughout the app
5. Route protection redirects unauthenticated users to login

### Equipment Management Flow
1. Equipment data stored in Firestore for real-time updates
2. CRUD operations update both local state and Firebase
3. Status changes trigger UI updates across components
4. Search and filtering performed on client-side cached data

### Checkout Process
1. Admin/user selects available equipment and assignee
2. Checkout record created with expected return date
3. Equipment status automatically updated to 'checked_out'
4. Real-time listeners update dashboard and equipment lists
5. Return process reverses status and records actual return date

## External Dependencies

### Primary Services
- **Firebase**: Authentication, Firestore database, real-time updates
- **Neon Database**: PostgreSQL hosting for structured data (configured but not actively used)
- **Recharts**: Data visualization for dashboard charts and analytics

### Development Tools
- **Drizzle ORM**: Type-safe database operations with PostgreSQL
- **React Query**: Server state management and caching
- **Wouter**: Lightweight routing for single-page application
- **Vite**: Development server and build optimization

### UI Libraries
- **Radix UI**: Accessible component primitives
- **Tailwind CSS**: Utility-first styling framework
- **Lucide React**: Consistent icon library
- **shadcn/ui**: Pre-built component library with Tailwind integration

## Deployment Strategy

### Development Environment
- Vite development server with hot module replacement
- Express server for API endpoints (currently minimal implementation)
- Firebase emulators for local development and testing
- TypeScript compilation with strict type checking

### Production Considerations
- Static site generation through Vite build process
- Express server compilation with esbuild for Node.js deployment
- Environment variable management for Firebase configuration
- Database migrations handled through Drizzle Kit

### Scaling Approach
- Firebase Firestore provides automatic scaling for real-time features
- PostgreSQL backend prepared for complex queries and reporting
- Component-based architecture allows for feature-specific optimizations
- React Query caching reduces API calls and improves performance

### Security Implementation
- Firebase Authentication handles secure user sessions
- Role-based access control at both UI and data levels
- Protected API endpoints with authentication middleware
- Input validation and sanitization for all user inputs