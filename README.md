# 📊 Bill of Material & Bill of Quantity Generator

A modern web-based solution for solution engineers at **Datoms IoT** to create, manage, and export **Bill of Materials (BOM)** and **Bill of Quantities (BOQ)**.

![License](https://img.shields.io/badge/license-MIT-blue)
![Node](https://img.shields.io/badge/node-18%2B-green)
![React](https://img.shields.io/badge/react-19-blue)
![TypeScript](https://img.shields.io/badge/typescript-5-blue)

## ✨ Features

### 📋 Bill of Quantity (BOQ) Calculator
- ✅ Item name, description, and quantity management
- ✅ Unit and unit rate configuration
- ✅ Automatic GST/tax calculations (customizable percentage)
- ✅ Line item and grand totals
- ✅ Professional formatting and templates
- ✅ Real-time calculations

### 📦 Bill of Material (BOM) Calculator
- ✅ Component listing with quantities
- ✅ Cost per unit and supplier tracking
- ✅ Automatic cost calculations
- ✅ Assembly/sub-assembly grouping
- ✅ Component categorization
- ✅ Multi-level hierarchy support

### 💾 Data Management
- ✅ Multi-project support with dashboard
- ✅ Database persistence (PostgreSQL)
- ✅ Import/Export to Excel, CSV, PDF, JSON
- ✅ Project versioning and history
- ✅ Automatic saving and recovery

### 🔐 User Features
- ✅ Secure authentication (Email/Password)
- ✅ Project ownership and access control
- ✅ Responsive design for all devices
- ✅ Intuitive UI for non-technical users
- ✅ Real-time calculations and updates
- ✅ Datoms IoT branding

### 🎨 Professional Design
- ✅ Modern, clean interface
- ✅ Dark/Light mode support
- ✅ Responsive layout (mobile, tablet, desktop)
- ✅ Accessibility compliant (WCAG)
- ✅ Professional color scheme

## 🛠 Tech Stack

### Frontend
| Tool | Purpose |
|------|---------|
| **React 19** | UI Framework |
| **Next.js 15** | Full-stack framework with SSR |
| **TypeScript** | Type safety |
| **Shadcn/ui** | UI component library |
| **Tailwind CSS** | Styling and responsive design |
| **React Hook Form** | Form management |
| **Zod** | Schema validation |
| **Zustand** | State management |
| **TanStack Table** | Data tables |
| **ExcelJS** | Excel export |
| **jsPDF** | PDF export |
| **papaparse** | CSV handling |

### Backend
| Tool | Purpose |
|------|---------|
| **Node.js 18+** | Runtime |
| **Express.js** | Web framework |
| **TypeScript** | Type safety |
| **PostgreSQL** | Database |
| **Prisma** | ORM |
| **JWT** | Authentication |
| **bcrypt** | Password hashing |
| **Zod** | Input validation |
| **Cors** | Cross-origin requests |
| **Rate Limiter** | API protection |

### DevOps & Deployment
| Tool | Purpose |
|------|---------|
| **Docker** | Containerization |
| **Vercel** | Frontend hosting |
| **Railway/Heroku** | Backend hosting |
| **PostgreSQL** | Managed database |

## 📁 Project Structure

```
BOM-BOQ/
├── frontend/                          # React + Next.js application
│   ├── app/
│   │   ├── layout.tsx                # Root layout
│   │   ├── page.tsx                  # Home page
│   │   ├── (auth)/                   # Auth routes
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   └── forgot-password/
│   │   ├── dashboard/                # Dashboard
│   │   ├── projects/                 # Project management
│   │   │   ├── page.tsx
│   │   │   ├── [id]/
│   │   │   └── create/
│   │   ├── boq/                      # BOQ routes
│   │   │   ├── page.tsx
│   │   │   ├── [projectId]/
│   │   │   └── create/
│   │   ├── bom/                      # BOM routes
│   │   │   ├── page.tsx
│   │   │   ├── [projectId]/
│   │   │   └── create/
│   │   ├── settings/
│   │   └── api/                      # API routes
│   ├── components/
│   │   ├── ui/                       # Shadcn components
│   │   ├── forms/
│   │   ├── tables/
│   │   ├── layout/
│   │   ├── boq/
│   │   ├── bom/
│   │   └── shared/
│   ├── lib/
│   │   ├── api.ts
│   │   ├── auth.ts
│   │   ├── utils.ts
│   │   └── constants.ts
│   ├── hooks/
│   ├── types/
│   ├── styles/
│   ├── public/                       # Static assets
│   │   ├── images/
│   │   └── icons/
│   ├── .env.example
│   ├── next.config.js
│   ├── tsconfig.json
│   ├── package.json
│   └── tailwind.config.ts
│
├── backend/                          # Node.js + Express API
│   ├── src/
│   │   ├── index.ts                 # Server entry point
│   │   ├── config.ts                # Configuration
│   │   ├── routes/
│   │   │   ├── auth.ts
│   │   │   ├── projects.ts
│   │   │   ├── boq.ts
│   │   │   ├── bom.ts
│   │   │   └── index.ts
│   │   ├── controllers/
│   │   │   ├── authController.ts
│   │   │   ├── projectController.ts
│   │   │   ├── boqController.ts
│   │   │   └── bomController.ts
│   │   ├── services/
│   │   │   ├── authService.ts
│   │   │   ├── projectService.ts
│   │   │   ├── boqService.ts
│   │   │   ├── bomService.ts
│   │   │   └── exportService.ts
│   │   ├── middleware/
│   │   │   ├── auth.ts
│   │   │   ├── errorHandler.ts
│   │   │   ├── validation.ts
│   │   │   └── cors.ts
│   │   ├── types/
│   │   │   └── index.ts
│   │   ├── utils/
│   │   │   ├── db.ts
│   │   │   └── validators.ts
│   │   └── constants/
│   │       └── index.ts
│   ├── prisma/
│   │   ├── schema.prisma
│   │   └── migrations/
│   ├── .env.example
│   ├── package.json
│   ├── tsconfig.json
│   └── Dockerfile
│
├── docs/
│   ├── API.md                        # API documentation
│   ├── SETUP.md                      # Setup guide
│   ├── DATABASE.md                   # Database schema
│   ├── FEATURES.md                   # Feature details
│   └── DEPLOYMENT.md                 # Deployment guide
│
├── .gitignore
├── .env.example
├── docker-compose.yml
├── LICENSE
└── README.md
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ ([Download](https://nodejs.org/))
- PostgreSQL 12+ ([Download](https://www.postgresql.org/))
- Git ([Download](https://git-scm.com/))

### 1. Clone Repository
```bash
git clone https://github.com/ashishanand969/BOM-BOQ.git
cd BOM-BOQ
```

### 2. Frontend Setup
```bash
cd frontend
npm install
cp .env.example .env.local

# Update .env.local with your backend API URL
# NEXT_PUBLIC_API_URL=http://localhost:5000

npm run dev
```

**Frontend runs on:** http://localhost:3000

### 3. Backend Setup
```bash
cd ../backend
npm install
cp .env.example .env

# Update .env with database credentials
# DATABASE_URL=postgresql://user:password@localhost:5432/bom_boq
# JWT_SECRET=your_secret_key
# NODE_ENV=development

# Run migrations
npx prisma migrate dev

# Start server
npm run dev
```

**Backend API runs on:** http://localhost:5000

### 4. Access Application
- **Frontend:** https://localhost:3000
- **API Docs:** https://localhost:5000/api/docs
- **Database:** PostgreSQL on localhost:5432

## 📚 API Documentation

### Authentication
```
POST   /api/auth/register          Register new user
POST   /api/auth/login             Login user
POST   /api/auth/logout            Logout user
POST   /api/auth/refresh           Refresh token
GET    /api/auth/me                Get current user
```

### Projects
```
GET    /api/projects               List user projects
POST   /api/projects               Create new project
GET    /api/projects/:id           Get project details
PUT    /api/projects/:id           Update project
DELETE /api/projects/:id           Delete project
```

### BOQ Management
```
GET    /api/projects/:projectId/boq                Get all BOQ items
POST   /api/projects/:projectId/boq                Create BOQ item
PUT    /api/projects/:projectId/boq/:itemId        Update BOQ item
DELETE /api/projects/:projectId/boq/:itemId        Delete BOQ item
POST   /api/projects/:projectId/boq/export         Export BOQ
```

### BOM Management
```
GET    /api/projects/:projectId/bom                Get all BOM items
POST   /api/projects/:projectId/bom                Create BOM item
PUT    /api/projects/:projectId/bom/:itemId        Update BOM item
DELETE /api/projects/:projectId/bom/:itemId        Delete BOM item
POST   /api/projects/:projectId/bom/export         Export BOM
```

## 💾 Database Schema

### Users Table
```sql
id (UUID Primary Key)
email (String, Unique)
password (String, Hashed)
name (String)
avatar (String)
createdAt (Timestamp)
updatedAt (Timestamp)
```

### Projects Table
```sql
id (UUID Primary Key)
userId (UUID Foreign Key)
name (String)
description (Text)
createdAt (Timestamp)
updatedAt (Timestamp)
```

### BOQ Items Table
```sql
id (UUID Primary Key)
projectId (UUID Foreign Key)
itemName (String)
description (Text)
quantity (Decimal)
unit (String)
unitRate (Decimal)
gstPercent (Decimal)
total (Decimal - Calculated)
createdAt (Timestamp)
updatedAt (Timestamp)
```

### BOM Items Table
```sql
id (UUID Primary Key)
projectId (UUID Foreign Key)
componentName (String)
quantity (Decimal)
costPerUnit (Decimal)
supplier (String)
category (String)
parentItemId (UUID - for hierarchy)
total (Decimal - Calculated)
createdAt (Timestamp)
updatedAt (Timestamp)
```

## 📤 Export Formats

The application supports exporting BOQ and BOM data in multiple formats:

- ✅ **Excel (.xlsx)** - Formatted spreadsheets with calculations
- ✅ **PDF (.pdf)** - Professional documents with company branding
- ✅ **CSV (.csv)** - Import-friendly format
- ✅ **JSON (.json)** - For data integration

## 🔐 Security Features

- 🔒 JWT-based authentication
- 🔑 Password hashing with bcrypt
- 🛡️ CORS protection
- ✓ Input validation and sanitization
- ⏱️ Rate limiting on API endpoints
- 🔐 SQL injection prevention (via Prisma ORM)
- 🚫 XSS protection
- 🔄 CSRF tokens for state-changing operations

## 🎨 Branding

The application includes:
- Datoms IoT logo and branding
- Professional color scheme
- Responsive design optimized for all devices
- Customizable templates
- Professional document exports

## 📱 Responsive Design

- ✅ Mobile devices (320px+)
- ✅ Tablets (768px+)
- ✅ Desktops (1024px+)
- ✅ Large screens (1440px+)

## 🧪 Testing

```bash
# Frontend tests
cd frontend
npm run test

# Backend tests
cd backend
npm run test

# Coverage report
npm run test:coverage
```

## 📦 Build & Deploy

### Frontend (Vercel)
```bash
cd frontend
npm run build
vercel deploy
```

### Backend (Railway/Heroku)
```bash
cd backend
npm run build
# Deploy using Railway/Heroku CLI
```

## 📖 Documentation

- [API Documentation](./docs/API.md) - Detailed API endpoints and examples
- [Setup Guide](./docs/SETUP.md) - Detailed installation instructions
- [Database Schema](./docs/DATABASE.md) - Database structure and relationships
- [Features Guide](./docs/FEATURES.md) - Feature documentation and usage
- [Deployment Guide](./docs/DEPLOYMENT.md) - Production deployment steps

## 🤝 Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Ashish Anand** - Initial development and architecture
- Datoms IoT Team

## 💬 Support

For issues, questions, or suggestions:
- 📝 [Create an Issue](https://github.com/ashishanand969/BOM-BOQ/issues)
- 💌 [Email Support](mailto:support@datoms.io)
- 📞 [Contact Us](https://www.datoms.io/contact)

## 🙏 Acknowledgments

- Built with modern technologies for production-ready applications
- Inspired by best practices in enterprise software development
- Designed with user experience as a priority

---

**Built with ❤️ for Datoms IoT Solution Engineers**

*Last Updated: May 30, 2026*
