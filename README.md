# AgriCycle – AI-Powered Harvest, Fodder & Agricultural Residue Marketplace

> **“One Harvest. Multiple Markets. Better Income. Less Waste.”**

AgriCycle is an enterprise-grade full-stack digital agricultural marketplace that connects **Farmers**, **Livestock Owners / Citizens**, **Industrial Companies**, and **Transport Logistics Providers**, governed by a secure **Super Admin**.

The platform is designed around the core paradigm of **ONE HARVEST → MULTIPLE MARKETS**: when a farmer completes a harvest (e.g. Rice Paddy), instead of selling only the grain and burning or discarding the remaining biomass, they can generate multiple verified sellable streams from the same harvest—such as food grain to millers, nutrient-rich straw bales to dairy/livestock owners, and rice husk to industrial biofuel or packaging plants.

---

## 🚀 Key Features

1. **One Harvest → Multiple Sellable Streams**
   - Farmers log a single crop harvest with variety and quantity.
   - Instantly branch the harvest into multiple marketplace listings (Grain, Fodder Straw, Residue Husk, Bagasse, Stalks).
   - Every downstream listing maintains a persistent parent relationship with its origin harvest record.

2. **Digital Lot ID & QR Code Provenance Traceability**
   - Every approved marketplace listing receives an immutable **Digital Lot ID** (e.g. `AGC-RICE-TG-2026-000145`).
   - Automatically generates a visual QR code matrix on HTML5 canvas representing harvest lineage, village origin, crop variety, and moisture/quality inspection data without exposing private personal phone numbers.

3. **Geospatial Marketplace & Leaflet Map Integration**
   - Interactive search and filter engine by keyword, category, district, price band, and quantity.
   - Dual-mode viewing: responsive Bootstrap card grid or interactive Leaflet + OpenStreetMap displaying nearby farm-gate supplies.

4. **Dedicated Livestock & Dairy Feed Portal**
   - Specialized search filtered by animal type (Milch Cows, Buffaloes, Goats, Sheep).
   - **Emergency Fodder Broadcast**: Livestock owners facing dry-season feed shortages can broadcast urgent alerts to local farmers for direct supply.

5. **Industrial Demand Board & Reverse Marketplace**
   - Bio-energy, paper, biochar, and compost manufacturers post bulk procurement demands (RFQs).
   - Individual farmers or rural aggregator clusters can submit supply proposals (`/requirements/{id}/offers`).

6. **Order Lifecycle & Transparent Counter-Offer Negotiation**
   - Complete multi-stage order workflow: `PENDING` → `CONFIRMED` → `READY_FOR_PICKUP` → `IN_TRANSIT` → `DELIVERED` → `COMPLETED`.
   - Buyers and farmers can exchange counter-offers before formalizing contract terms.

7. **Rural Logistics & Transporter Job Matching**
   - Registered transporters (tractors, mini trucks, commercial haulers) receive available delivery job dispatches based on pickup and drop points.
   - Real-time status update controls (`DISPATCHED`, `IN_TRANSIT`, `DELIVERED`) with transparent haulage earnings.

8. **AI Engine Suite**
   - **AI Multi-Factor Matching**: Calculates compatibility scores between farmer listings and buyer demands across material, volume, proximity, and price.
   - **AI Best-Use Classifier**: Algorithmic suggestions for optimal downstream commercial reuse.
   - **AI Fair-Band Price Estimator**: Suggests minimum and maximum market price bands.
   - **AI Demand Trend Appetite Index**: Regional market appetite ratings.
   - **Harvest Recovery Value Calculator**: Live simulation calculating additional income boost (+15% to +30%) from by-product monetization.
   - **Environmental & Carbon Impact Engine**: Quantifies metric tons of residue diverted, stubble burning prevented, and CO2 emissions mitigated.

9. **Enterprise Security & Role-Based Access Control (RBAC)**
   - Strict defense-in-depth: stateless JWT authentication, BCrypt password hashing (strength 12), fine-grained method security (`@PreAuthorize`), XSS protection, and SQL injection prevention via JPA parameterization.
   - Admin account is protected with bootstrap-only creation (cannot be chosen during registration).
   - Comprehensive, immutable `AuditLog` records every administrative, security, and moderation action.

---

## 🛠️ Technology Stack

- **Backend**: Java 25 LTS, Spring Boot 3.5.16
- **Persistence**: Spring Data JPA, Hibernate, MySQL 8.x
- **Security**: Spring Security 6.x, JJWT (0.12.6), BCrypt
- **API Documentation**: Springdoc OpenAPI 2.8.17 (Swagger UI)
- **Database**: Relational MySQL (`agricycle_db`) with indexed foreign keys and strict constraints
- **Frontend**: HTML5, CSS3, JavaScript (Fetch API, ES6 Modules), Bootstrap 5.3, Bootstrap Icons, Leaflet Maps
- **Build Tool**: Apache Maven 3.9+

---

## 🔐 Pre-Seeded Demo Test Accounts

The platform includes a built-in `DataInitializer` that seeds realistic Telangana & Andhra Pradesh agricultural demo data. You can log in instantly using the **⚡ Quick Demo 1-Click Login** buttons on `/login.html`:

| Role | Name | Email | Password | Primary Functions |
|---|---|---|---|---|
| **Farmer** | Ramesh Patel | `ramesh.farmer@agricycle.com` | `Farmer@123` | Add harvests, create outputs, manage listings, view orders & earnings |
| **Livestock Owner** | Suresh Dairy | `suresh.dairy@agricycle.com` | `Livestock@123` | Search fodder by animal, post urgent shortage alerts, rate sellers |
| **Company Buyer** | GreenTech Biomass | `procure@greentechbiomass.com` | `Company@123` | Post bulk industrial demands, review supply proposals, place POs |
| **Transporter** | Raju Logistics | `raju.transport@agricycle.com` | `Transporter@123` | Accept delivery jobs, update transit statuses, manage fleet |
| **Super Admin** | System Admin | `admin@agricycle.com` | `Admin@AgriCycle2026!` | User suspension, listing approvals, category controls, audit trail |

---

## 📦 Project Structure

```
AgriCycle/
├── backend/
│   └── src/
│       ├── main/
│       │   ├── java/com/agricycle/
│       │   │   ├── config/             # SecurityConfig, WebConfig, OpenApiConfig, DataInitializer
│       │   │   ├── controller/         # REST Controllers for all 18 modules
│       │   │   ├── dto/                # Request/Response DTOs with Bean Validation
│       │   │   ├── entity/             # 21 JPA entities and enums
│       │   │   ├── exception/          # GlobalExceptionHandler and custom exceptions
│       │   │   ├── repository/         # Spring Data JPA repositories with query methods
│       │   │   ├── security/           # JwtUtils, JwtFilter, UserDetailsServiceImpl
│       │   │   └── service/            # Core business logic services
│       │   └── resources/
│       │       ├── application.properties
│       │       └── schema.sql, data.sql
│       └── test/java/com/agricycle/    # Unit & Integration Tests (AiServiceTest, SecurityAndRbacTest)
├── database/
│   ├── schema.sql                      # Complete MySQL DDL table schema
│   └── data.sql                        # Comprehensive DML seed dataset
├── frontend/
│   ├── css/
│   │   └── style.css                   # Custom responsive styling and theme tokens
│   ├── js/
│   │   ├── app.js                      # Core API fetcher, JWT storage, toasts, i18n, QR generator
│   │   ├── marketplace.js              # Marketplace filtering & Leaflet OpenStreetMap logic
│   │   └── dashboard.js                # Multi-role controller for all 5 dashboard panels
│   ├── index.html                      # Homepage & Live AI Harvest Recovery Calculator
│   ├── marketplace.html                # Central Marketplace with Grid & Geospatial Map
│   ├── product-detail.html             # Product provenance, Lot ID, QR canvas, and order form
│   ├── find-fodder.html                # Dedicated fodder portal for livestock & emergency alerts
│   ├── requirements.html               # Industrial Demand Board & Reverse Marketplace
│   ├── login.html                      # JWT Sign-in with 1-Click Demo Quick Fill buttons
│   ├── register.html                   # Role-based onboarding with dynamic fields
│   ├── dashboard-farmer.html           # Farmer Control Center
│   ├── dashboard-livestock.html        # Livestock & Dairy Management Panel
│   ├── dashboard-company.html          # Corporate Procurement Center
│   ├── dashboard-transporter.html      # Transporter Logistics & Job Manager
│   ├── dashboard-admin.html            # Super Admin Governance Center
│   ├── impact.html                     # Carbon Mitigation & Economic Impact stats
│   ├── how-it-works.html               # Persona-based workflow guides
│   ├── about.html                      # Mission, Vision & UN SDG alignment
│   ├── faq.html                        # Frequently Asked Questions
│   └── contact.html                    # Agricultural Operations Helpline & Regional Center
├── pom.xml                             # Maven build configuration
└── README.md
```

---

## ⚡ Setup & Execution Instructions

### 1. Prerequisites
- **Java Development Kit**: JDK 25 installed.
- **Apache Maven**: Maven 3.9+ configured in PATH.
- **MySQL 8.0**: Running locally on port `3306`.
  - Default database credentials: username `root`, password `1234`.
  - Database name: `agricycle_db` (Spring Boot creates it automatically if it does not exist).

### 2. Configure Database (Optional)
If your local MySQL credentials differ, adjust `backend/src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/agricycle_db?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC
spring.datasource.username=YOUR_MYSQL_USERNAME
spring.datasource.password=YOUR_MYSQL_PASSWORD
```

### 3. Run the Test Suite
Verify that all unit and integration tests execute cleanly:
```powershell
mvn test "-Dnet.bytebuddy.experimental=true"
```

### 4. Start the Application
Launch the Spring Boot server directly via Maven:
```powershell
mvn spring-boot:run
```
The application will boot on **port 8080**. `DataInitializer` will automatically seed the initial users, categories, harvests, listings, requirements, and orders.

### 5. Access the Platform
- **AgriCycle Web Portal**: [http://localhost:8080/](http://localhost:8080/)
- **Marketplace**: [http://localhost:8080/marketplace.html](http://localhost:8080/marketplace.html)
- **Fodder Finder**: [http://localhost:8080/find-fodder.html](http://localhost:8080/find-fodder.html)
- **Industry Demands**: [http://localhost:8080/requirements.html](http://localhost:8080/requirements.html)
- **Login Portal**: [http://localhost:8080/login.html](http://localhost:8080/login.html)
- **Swagger / OpenAPI Documentation**: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)

---

## 🔒 Security Best Practices Implemented

1. **Strict Separation of Privilege**: Regular user registration strictly blocks `ROLE_ADMIN`. Any attempt to register as an administrator throws a `BadRequestException` and writes a security violation record to `AuditLog`.
2. **Stateless Session Management**: Backed by cryptographically signed JWT tokens with expiration handling.
3. **Data Sanitization & Ownership Enforcement**: Users can only update or cancel their own listings and orders. Controllers delegate strictly to transactional service layers that validate entity ownership.
4. **Privacy-Preserving Provenance**: Digital Lot IDs and QR code labels do not display personal telephone numbers or private financial credentials.
5. **Defense Against Common Attacks**:
   - **SQL Injection**: Eliminated through Spring Data JPA typed queries and JPQL parameters.
   - **XSS**: Strict output encoding on frontend components and input bean validation.
   - **CSRF**: Stateless token architecture immune to browser credential reuse.

---

## 📄 License & Attribution
Developed for AgriCycle Agricultural Circular Economy Platform. Built exclusively using Java Full Stack 
