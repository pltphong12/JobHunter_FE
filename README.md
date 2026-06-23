# JobHunter — Frontend

A modern, full-featured **Job Hunting Platform** built with **React 18**, **TypeScript**, and **Ant Design**. JobHunter connects job seekers with companies by providing an intuitive interface for browsing jobs, submitting resumes, and managing the entire recruitment lifecycle through a powerful admin dashboard.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Environment Variables](#environment-variables)
- [API Modules](#api-modules)
- [State Management](#state-management)
- [Authentication & Authorization](#authentication--authorization)
- [Routing](#routing)
- [Styling](#styling)
- [Build & Deployment](#build--deployment)
- [License](#license)

---

## Features

### Client-Side (Public)

- **Home Page** — Landing page with job search functionality
- **Job Search & Browse** — Search, filter, and paginate through job listings
- **Job Detail** — View comprehensive job information (skills, salary, location, etc.)
- **Company Directory** — Browse companies with detailed profiles
- **Resume Submission** — Upload and submit resumes directly to job postings
- **Authentication** — User registration and login with JWT-based authentication
- **Skill Subscription** — Subscribe to receive notifications for jobs matching specific skills

### Admin Dashboard

- **Dashboard** — Overview with key metrics and statistics
- **User Management** — Create, update, and delete user accounts
- **Company Management** — Full CRUD operations for company profiles
- **Job Management** — Create and manage job postings with rich text editing
- **Resume Management** — Review and update resume statuses (Pending / Approved / Rejected)
- **Role Management** — Define roles with name, description, and active status

---

## Tech Stack

| Category            | Technology                                                                 |
| ------------------- | -------------------------------------------------------------------------- |
| **Framework**       | [React 18](https://react.dev/) with TypeScript                             |
| **Build Tool**      | [Vite 4](https://vitejs.dev/) + SWC (via `@vitejs/plugin-react-swc`)      |
| **UI Library**      | [Ant Design 5](https://ant.design/) + [Ant Design Pro Components](https://procomponents.ant.design/) |
| **State Management**| [Redux Toolkit](https://redux-toolkit.js.org/) + React-Redux               |
| **Routing**         | [React Router DOM v6](https://reactrouter.com/)                            |
| **HTTP Client**     | [Axios](https://axios-http.com/) with custom interceptors                  |
| **Rich Text Editor**| [React Quill](https://github.com/zenoamaro/react-quill)                   |
| **Styling**         | SCSS Modules                                                               |
| **Icons**           | Ant Design Icons + React Icons                                             |
| **Utilities**       | Lodash, Day.js, query-string, uuid                                         |
| **Language**        | TypeScript 5                                                               |

---

## Prerequisites

- **Node.js** >= 16.x
- **npm** >= 8.x (or **yarn** / **pnpm**)
- A running instance of the **JobHunter Backend API** (Spring Boot REST API on port `8080` by default)

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/pltphong12/JobHunter_FE.git
cd JobHunter_FE
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Copy the provided `.env.development` and adjust values as needed:

```env
NODE_ENV=development
PORT=3000
VITE_BACKEND_URL=http://localhost:8080
```

> **Note:** `VITE_BACKEND_URL` should point to your running backend API server.

### 4. Start the development server

```bash
npm run dev
```

The application will be available at **http://localhost:3000**.

### 5. Build for production

```bash
npm run build
```

The optimized output will be generated in the `dist/` directory.

### 6. Preview the production build

```bash
npm run preview
```

---

## Project Structure

```
src/
├── App.tsx                     # Root component with route definitions
├── main.tsx                    # Application entry point
├── vite-env.d.ts               # Vite environment type declarations
│
├── assets/                     # Static assets (images, icons, etc.)
│
├── components/
│   ├── admin/                  # Admin dashboard components
│   │   ├── layout.admin.tsx    # Admin layout with sidebar navigation
│   │   ├── company/            # Company management components
│   │   ├── job/                # Job management components (including upsert form)
│   │   ├── resume/             # Resume management components
│   │   ├── role/               # Role management components
│   │   ├── skill/              # Skill management components
│   │   └── user/               # User management components
│   │
│   ├── client/                 # Public-facing client components
│   │   ├── header.client.tsx   # Site header with navigation & search
│   │   ├── footer.client.tsx   # Site footer
│   │   ├── search.client.tsx   # Search component
│   │   ├── card/               # Job/company card components
│   │   ├── data-table/         # Data table components
│   │   └── modal/              # Modal dialog components
│   │
│   └── share/                  # Shared/common components
│       ├── layout.app.tsx      # App-wide layout wrapper
│       ├── loading.tsx         # Loading spinner component
│       ├── not.found.tsx       # 404 Not Found page
│       └── protected-route.ts/ # Route guard for authenticated routes
│
├── config/
│   ├── api.ts                  # All API call functions (organized by module)
│   ├── axios-customize.ts      # Axios instance with interceptors & token refresh
│   └── utils.ts                # Utility/helper functions
│
├── pages/
│   ├── admin/                  # Admin pages
│   │   ├── dashboard.tsx       # Dashboard with statistics
│   │   ├── company.tsx         # Company management page
│   │   ├── user.tsx            # User management page
│   │   ├── job/                # Job management pages
│   │   ├── resume.tsx          # Resume management page
│   │   └── role.tsx            # Role management page
│   │
│   ├── auth/                   # Authentication pages
│   │   ├── login.tsx           # Login page
│   │   └── register.tsx        # Registration page
│   │
│   ├── company/                # Public company pages
│   │   ├── index.tsx           # Company listing
│   │   └── detail.tsx          # Company detail view
│   │
│   ├── home/                   # Homepage
│   │   └── index.tsx
│   │
│   └── job/                    # Public job pages
│       ├── index.tsx           # Job listing
│       └── detail.tsx          # Job detail view
│
├── redux/
│   ├── store.ts                # Redux store configuration
│   ├── hooks.ts                # Typed Redux hooks (useAppDispatch, useAppSelector)
│   └── slice/
│       ├── accountSlide.ts     # Authentication & account state
│       ├── companySlide.ts     # Company state management
│       ├── jobSlide.ts         # Job state management
│       ├── resumeSlide.ts      # Resume state management
│       ├── roleSlide.ts        # Role state management
│       ├── skillSlide.ts       # Skill state management
│       └── userSlide.ts        # User state management
│
├── styles/
│   ├── reset.scss              # CSS reset / base styles
│   ├── app.module.scss         # Global app styles
│   ├── admin.module.scss       # Admin layout styles
│   ├── auth.module.scss        # Authentication page styles
│   └── client.module.scss      # Client-facing page styles
│
└── types/
    ├── backend.d.ts            # TypeScript interfaces for API responses
    └── file.d.ts               # File-related type declarations
```

---

## Environment Variables

| Variable             | Description                                      | Default                    |
| -------------------- | ------------------------------------------------ | -------------------------- |
| `NODE_ENV`           | Application environment (`development` / `production`) | `development`         |
| `PORT`               | Development server port                          | `3000`                     |
| `VITE_BACKEND_URL`   | Backend API base URL                             | `http://localhost:8080`    |

---

## API Modules

The application communicates with a **Spring Boot RESTful API** backend. All API functions are centralized in `src/config/api.ts` and organized by module:

| Module           | Endpoints                          | Description                           |
| ---------------- | ---------------------------------- | ------------------------------------- |
| **Auth**         | `/api/v1/auth/*`                   | Register, login, logout, refresh token, fetch account |
| **Files**        | `/api/v1/files`                    | Single file upload (multipart/form-data) |
| **Companies**    | `/api/v1/companies`                | CRUD operations for companies         |
| **Skills**       | `/api/v1/skills`                   | CRUD operations for skills/tags       |
| **Users**        | `/api/v1/users`                    | CRUD operations for user accounts     |
| **Jobs**         | `/api/v1/jobs`                     | CRUD operations for job postings      |
| **Resumes**      | `/api/v1/resumes`                  | CRUD + status management for resumes  |
| **Roles**        | `/api/v1/roles`                    | CRUD for roles                        |
| **Subscribers**  | `/api/v1/subscribers`              | Manage job notification subscriptions |

---

## State Management

The application uses **Redux Toolkit** for global state management with the following slices:

- **accountSlice** — Manages user authentication state, account info, and token refresh logic
- **companySlice** — Handles company listing state and pagination
- **jobSlice** — Manages job listing state and pagination
- **resumeSlice** — Handles resume listing and status updates
- **roleSlice** — Manages role definitions
- **skillSlice** — Handles skill/tag data
- **userSlice** — Manages user listing for admin panel

Custom typed hooks (`useAppDispatch`, `useAppSelector`) are provided in `src/redux/hooks.ts` for type-safe Redux usage throughout the application.

---

## Authentication & Authorization

### JWT Token Flow

1. **Login** — User submits credentials → receives `access_token` (stored in `localStorage`) and `refresh_token` (stored as HTTP-only cookie)
2. **Request Interceptor** — Automatically attaches `Authorization: Bearer <token>` to all API requests
3. **Token Refresh** — On `401` responses, the app automatically attempts to refresh the token via `/api/v1/auth/refresh` using a **mutex lock** to prevent race conditions
4. **Session Expiry** — If token refresh fails on admin routes, a Redux action dispatches a notification prompting re-login

### Role-Based Access Control

- **Protected Routes** — Admin routes are wrapped with `<ProtectedRoute>` component requiring authentication
- **Role-Based Authorization** — Access control is enforced by the backend based on the user's assigned role (e.g., ADMIN, HR, USER)
- **Admin Sidebar** — All menu items are visible to authenticated admin users; the backend enforces role-based restrictions on API calls

---

## Routing

| Path                  | Component              | Access    | Description              |
| --------------------- | ---------------------- | --------- | ------------------------ |
| `/`                   | `HomePage`             | Public    | Landing page             |
| `/job`                | `ClientJobPage`        | Public    | Job listing              |
| `/job/:id`            | `ClientJobDetailPage`  | Public    | Job detail view          |
| `/company`            | `ClientCompanyPage`    | Public    | Company listing          |
| `/company/:id`        | `ClientCompanyDetailPage` | Public | Company detail view      |
| `/login`              | `LoginPage`            | Public    | User login               |
| `/register`           | `RegisterPage`         | Public    | User registration        |
| `/admin`              | `DashboardPage`        | Protected | Admin dashboard          |
| `/admin/company`      | `CompanyPage`          | Protected | Company management       |
| `/admin/user`         | `UserPage`             | Protected | User management          |
| `/admin/job`          | `JobTabs`              | Protected | Job management           |
| `/admin/job/upsert`   | `ViewUpsertJob`        | Protected | Create/edit job          |
| `/admin/resume`       | `ResumePage`           | Protected | Resume management        |
| `/admin/role`         | `RolePage`             | Protected | Role management          |

---

## Styling

The project uses **SCSS Modules** for component-scoped styling:

- `reset.scss` — Global CSS reset and base element styles
- `app.module.scss` — Root application layout styles
- `admin.module.scss` — Admin panel specific styles
- `auth.module.scss` — Login and registration page styles
- `client.module.scss` — Public-facing client page styles

Path aliases are configured in both `vite.config.ts` and `tsconfig.json` for clean imports:

```typescript
import styles from 'styles/client.module.scss';
import Header from 'components/client/header.client';
import { callLogin } from 'config/api';
```

---

## Build & Deployment

### Development

```bash
npm run dev        # Start dev server with HMR
npm run start      # Alias for npm run dev
```

### Production

```bash
npm run build      # TypeScript compilation + Vite production build
npm run preview    # Preview the production build locally
```

### Bundle Analysis

The project includes `rollup-plugin-visualizer` for analyzing bundle size. Uncomment the visualizer plugin in `vite.config.ts` to generate a report:

```typescript
plugins: [
  react(),
  visualizer() as PluginOption  // Uncomment this line
],
```

### Deployment Notes

- The production build outputs static files to the `dist/` directory
- Can be served by any static file server (Nginx, Apache, Vercel, Netlify, etc.)
- Ensure the `VITE_BACKEND_URL` environment variable points to your production API server
- Configure your web server to redirect all routes to `index.html` for client-side routing support

---

## License

This project is private and not licensed for public distribution.

---

> **JobHunter** — Built with ❤️ using React, TypeScript, and Ant Design
