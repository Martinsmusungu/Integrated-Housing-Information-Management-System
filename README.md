# Integrated Housing Information Management System

## Overview

The Integrated Housing Information Management System (IHIMS) is designed to streamline and enhance the management of housing information across 47 counties and headquarters. This platform enables efficient management of occupancy, change requests, approvals, and data analytics with role-based access control and geospatial visualization.

## Project Vision

A centralized, multi-tenant web application that allows:
- **County Level**: Submit occupancy changes and housing unit information
- **HQ Level**: Review, approve/reject submissions with detailed comments
- **All Levels**: View analytics, reports, and geospatial data of housing assets

## Key Features

### 1. Housing Unit Management
- Track house number, personal number, date of occupation/vacation
- Monitor rent amounts and occupancy status
- Record remarks for occupancy changes
- County-level data entry and updates

### 2. Occupancy Change Requests
- Submit occupancy changes with justification
- Track submission status (pending, approved, rejected)
- HQ-level approval/rejection with comments
- Audit trail of all changes

### 3. Role-Based Access Control
- **County Officers**: View and submit housing data and change requests
- **County Admin**: Approve county-level submissions before HQ review
- **HQ Officers**: Review and process submissions
- **HQ Admin**: System administration and analytics

### 4. Analytics & Reporting
- Dashboard showing submission metrics
- Approved vs. rejected occupancy changes
- County-level performance indicators
- Trend analysis over time

### 5. Geospatial Features
- Map visualization of housing units by county
- Land resources and assets location mapping
- Integration with Survey123 or open-source data collection tools (ODK)
- Real-time updates from field surveys

## System Architecture

### Technology Stack
- **Frontend**: React.js/Vue.js with Leaflet or Mapbox for mapping
- **Backend**: Python (Django/FastAPI) or Node.js (Express)
- **Database**: PostgreSQL with PostGIS extension for geospatial features
- **Mobile Data Collection**: Survey123 or ODK (Open Data Kit)
- **Deployment**: Docker, Kubernetes (optional)

### Architecture Components

```
┌─────────────────────────────────────────────────────────────┐
│                      CLIENT LAYER                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │ County Web   │  │ HQ Web       │  │ Mobile App   │       │
│  │ Application  │  │ Dashboard    │  │ (Data Entry) │       │
│  └──────────────┘  └──────────────┘  └──────────────┘       │
└──────────────────────┬──────────────────────────────────────┘
                       │
          ┌────────────┴────────────┐
          │   REST/GraphQL API      │
          │   API Gateway           │
          └────────────┬────────────┘
                       │
┌──────────────────────┴──────────────────────────────────────┐
│                    APPLICATION LAYER                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ Auth Module  │  │ Housing Unit │  │ Change       │      │
│  │              │  │ Management   │  │ Request      │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ Geospatial   │  │ Analytics &  │  │ Approval     │      │
│  │ Module       │  │ Reports      │  │ Workflow     │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└──────────────────────┬──────────────────────────────────────┘
                       │
┌──────────────────────┴──────────────────────────────────────┐
│                    DATA LAYER                               │
│  ┌────────────────────────────────────────────────────┐    │
│  │  PostgreSQL Database (with PostGIS)                │    │
│  │  - Users & Roles                                   │    │
│  │  - Housing Units                                   │    │
│  │  - Occupancy Changes                               │    │
│  │  - Geospatial Data                                 │    │
│  │  - Audit Logs                                      │    │
│  └────────────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────────────┘
```

### Database Schema Overview

**Users Table**
- user_id, username, email, password_hash, role, county_id

**Counties Table**
- county_id, county_name, region, contact_info

**Housing Units Table**
- unit_id, house_number, personal_number, county_id, date_occupied, date_vacated, rent_amount, status, remarks, geom (PostGIS geometry)

**Occupancy Changes Table**
- change_id, unit_id, submitted_by, submission_date, change_type, new_occupant, justification, status, submitted_to_hq_date

**Approvals Table**
- approval_id, change_id, approved_by, approval_date, status (approved/rejected), comments, remarks

**Audit Logs Table**
- log_id, user_id, action, table_name, timestamp, details

## Installation & Setup

### Prerequisites
- Node.js (v16+) / Python (3.8+)
- PostgreSQL (12+) with PostGIS
- Git

### Backend Setup
```bash
# Clone repository
git clone https://github.com/Martinsmusungu/Integrated-Housing-Information-Management-System.git
cd Integrated-Housing-Information-Management-System

# Backend (Python/Django)
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

### Frontend Setup
```bash
# Frontend (React/Vue)
cd frontend
npm install
npm start
```

### Environment Configuration
Create a `.env` file in backend and frontend directories with appropriate values for:
- DATABASE_URL
- SECRET_KEY
- API_BASE_URL
- MAP_API_KEY (Mapbox or similar)

## Development Workflow

1. Create feature branches from `main`
2. Follow the issue templates for bug reports and feature requests
3. Create pull requests with detailed descriptions
4. Code reviews required before merge
5. Automated tests must pass

## Contributing

Please read CONTRIBUTING.md for guidelines on:
- Code style
- Commit messages
- Pull request process
- Testing requirements

## Project Roadmap

### Phase 1: Core Housing Unit Management
- Housing unit CRUD operations
- County-level data entry
- Basic user authentication

### Phase 2: Occupancy Change Workflow
- Change request submission
- HQ approval/rejection mechanism
- Comments and feedback system

### Phase 3: Analytics & Reporting
- Dashboard development
- Report generation
- Performance metrics

### Phase 4: Geospatial Features
- Map integration
- Survey123/ODK integration
- Real-time data updates

### Phase 5: Advanced Features
- Mobile application
- Advanced analytics
- System optimization

## License

[Specify your license here]

## Contact & Support

For questions or support, please contact: [contact information]

## Repository Structure

```
.
├── README.md
├── CONTRIBUTING.md
├── docs/
│   ├── ARCHITECTURE.md
│   ├── API_DOCUMENTATION.md
│   ├── DATABASE_SCHEMA.md
│   └── DEPLOYMENT.md
├── backend/
│   ├── app/
│   ├── tests/
│   ├── requirements.txt
│   └── config.py
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── .env.example
├── .github/
│   ├── workflows/
│   └── ISSUE_TEMPLATE/
└── docker-compose.yml
```