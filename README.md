# 🚀 Teen Expense Tracker

A modern, beginner-friendly, production-quality financial tracking web application built specifically for teenagers and young adults. Designed to help teenagers record pocket money and expenses, manage category budgets, work toward saving goals, analyze spending habits with interactive charts, and receive friendly, educational smart financial suggestions.

---

## 🌟 Key Features

### 1. 🔐 User Authentication & Security
- **Secure Registration & Login** using `bcryptjs` password hashing with salt rounds.
- **JWT Authentication** tokens with session management and protected routes.
- **Strict User Isolation**: All backend queries derive `user_id` strictly from verified JWT tokens—users can never access or modify another user's records.
- **Sensitive Key Protection**: Supabase service keys and JWT secrets reside exclusively in backend environment variables.

### 2. 📊 Dynamic Dashboard
- Instant view of:
  - **Total Balance** (Total Received − Total Spent)
  - **Total Money Spent** (Lifetime & Current Month)
  - **Total Money Received** (Pocket money, allowances, gifts)
  - **Logged Expenses Count**
  - **Largest Single Expense** with category and date
  - **Most-Used Spending Category**
  - **Recent Transactions Feed** combining income and expenses
  - **Active Budget Alerts Banner** (highlighting categories nearing or exceeding limits)
  - **Smart Suggestions Widget**

### 3. 💸 Add Expense & Smart Categorization
- Input fields: Amount, Title, Category, Expense Date, Payment Method (Cash, UPI, Card, Net Banking), and Optional Notes.
- **Teen Category Grid**: Food 🍕, Shopping 🛍️, Entertainment 🎬, Transport 🚌, Education 📚, Gaming 🎮, Subscriptions 📱, Friends 🤝, Other 💡.
- **Real-Time Budget Guardrail**: Warns the user *before* submitting if the expense will approach or exceed their monthly category budget.
- Comprehensive form validation preventing negative values, empty fields, or invalid dates.

### 4. 📋 Expense List & History
- Complete transaction log with:
  - Real-time text search (searches title and notes)
  - Category filtering
  - Date range filtering (From Date to To Date)
  - Multi-attribute sorting (Date Newest/Oldest, Amount High-to-Low/Low-to-High)
  - Category badges and payment method tags
  - Inline **Edit Expense Modal**
  - Safe **Delete Confirmation Dialog**

### 5. 💰 Income & Money Received Tracking
- Track money received separately from spending.
- Specific teen sources: Pocket money, Allowance, Gift, Part-time income, Scholarship, Other.
- Total income metrics and full CRUD capabilities.

### 6. 📈 Graphical Analytics (Powered by Recharts)
- **Category-Wise Spending (Pie / Doughnut Chart)**: Visual slice breakdown with custom currency tooltips.
- **Monthly Spending (Bar Chart)**: 6-month historical spending comparison.
- **Spending Trend Velocity**: Automatically calculates whether current month spending is increasing or decreasing compared to last month.
- **Income vs. Expense Comparison**: Side-by-side cash flow bar chart.
- **Payment Method Distribution**: Visual breakdown of Cash vs. UPI vs. Card usage.

### 7. 💡 Smart Spending Suggestions
- Educational, supportive, and non-judgmental rule-based financial tips.
- Flags spending concentrations (e.g. *"Food took up 35% of your expenses"*).
- Celebrates disciplined months (e.g. *"Spending is down 15% from last month—fantastic discipline!"*).
- Suggests putting surplus cash toward wishlist saving goals.
- Clear educational disclaimer clarifying suggestions are for financial literacy, not professional financial advice.

### 8. 🎯 Monthly Category Budgets
- Set monthly limits for categories like Food, Shopping, Entertainment, etc.
- Interactive progress bars showing:
  - 🟢 **Safe** (< 80% used)
  - 🟡 **Warning** (80% - 100% used): *"You're getting close to your Food budget."*
  - 🔴 **Exceeded** (> 100% used): *"You have exceeded your Food budget by ₹200."*
- Month-by-month historical budget selector.

### 9. 🎧 Wishlist & Saving Goals
- Track goals such as *New Headphones*, *Gaming Console*, *Sneakers*, *College Fund*.
- Progress bar displaying saved amount, target amount, and progress percentage.
- **Interactive Pocket Money Deposit**: Allows depositing money directly into the goal with one-click presets (+₹100, +₹250, +₹500, +₹1,000, or custom).
- 🏆 **Celebration Badge** when 100% of the goal is achieved!

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, Vite 6, React Router DOM 6, Recharts, Lucide React, Modern CSS3 |
| **Backend** | Node.js, Express.js 4, REST API, bcryptjs, jsonwebtoken, cors, dotenv |
| **Database** | Supabase PostgreSQL with `@supabase/supabase-js` (with zero-setup local persistent fallback) |
| **Design** | Clean modern typography (Plus Jakarta Sans & Outfit), Glassmorphism, Responsive CSS Grid/Flexbox |

---

## 📂 Project Structure

```text
teen-expense-tracker/
│
├── frontend/                          # React + Vite Frontend Application
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── common/
│   │   │   │   ├── Card.jsx
│   │   │   │   ├── ConfirmDialog.jsx  # Reusable delete confirmation
│   │   │   │   ├── EmptyState.jsx     # Teen-friendly empty states
│   │   │   │   ├── LoadingSpinner.jsx # Spinners & loading overlays
│   │   │   │   └── Modal.jsx          # Accessible dialog overlay
│   │   │   └── layout/
│   │   │       ├── Layout.jsx         # App shell layout
│   │   │       ├── Navbar.jsx         # Sticky header with quick actions
│   │   │       ├── ProtectedRoute.jsx # Route authentication guard
│   │   │       └── Sidebar.jsx        # Responsive navigation sidebar
│   │   ├── context/
│   │   │   └── AuthContext.jsx        # Global session & currency state
│   │   ├── pages/
│   │   │   ├── AddExpense.jsx         # Dedicated expense creation form
│   │   │   ├── Analytics.jsx          # Recharts analytics & trend page
│   │   │   ├── Budget.jsx             # Category budget management
│   │   │   ├── Dashboard.jsx          # Master dashboard
│   │   │   ├── Expenses.jsx           # Filterable expense list & modals
│   │   │   ├── Income.jsx             # Income tracker & modal CRUD
│   │   │   ├── Login.jsx              # Sign-in page with demo button
│   │   │   ├── Profile.jsx            # User settings & password change
│   │   │   ├── Register.jsx           # Sign-up page
│   │   │   └── Savings.jsx            # Wishlist saving goals & deposits
│   │   ├── services/
│   │   │   └── api.js                 # Centralized API fetch client with JWT
│   │   ├── App.jsx                    # React Router configuration
│   │   ├── index.css                  # Master CSS design system & tokens
│   │   └── main.jsx                   # React root entry
│   ├── .env.example
│   ├── .env
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
│
└── backend/                           # Node.js + Express REST API
    ├── database.sql                   # Supabase PostgreSQL schema & RLS
    ├── tests/
    │   └── api.test.js                # Automated backend test suite
    ├── src/
    │   ├── config/
    │   │   ├── db.js                  # Supabase client + local dev engine
    │   │   └── env.js                 # Environment variable validation
    │   ├── controllers/
    │   │   ├── analyticsController.js
    │   │   ├── authController.js
    │   │   ├── budgetController.js
    │   │   ├── dashboardController.js
    │   │   ├── expenseController.js
    │   │   ├── incomeController.js
    │   │   ├── savingsController.js
    │   │   └── suggestionsController.js
    │   ├── middleware/
    │   │   ├── authMiddleware.js      # JWT token validation
    │   │   ├── errorMiddleware.js     # Centralized error handler
    │   │   └── validateMiddleware.js  # Request schema validation
    │   ├── routes/
    │   │   ├── analyticsRoutes.js
    │   │   ├── authRoutes.js
    │   │   ├── budgetRoutes.js
    │   │   ├── dashboardRoutes.js
    │   │   ├── expenseRoutes.js
    │   │   ├── incomeRoutes.js
    │   │   ├── savingsRoutes.js
    │   │   └── suggestionsRoutes.js
    │   ├── services/
    │   │   ├── analyticsService.js
    │   │   ├── authService.js
    │   │   ├── budgetService.js
    │   │   ├── dashboardService.js
    │   │   ├── expenseService.js
    │   │   ├── incomeService.js
    │   │   ├── savingsService.js
    │   │   └── suggestionsService.js
    │   └── server.js                  # Express application setup
    ├── .env.example
    ├── .env
    └── package.json
```

---

## ⚙️ Installation & Quick Start

### Prerequisites
- **Node.js** (v18.0 or newer recommended)
- **npm** (v9.0 or newer)

---

### Step 1: Install Backend Dependencies
```bash
cd backend
npm install
```

### Step 2: Install Frontend Dependencies
```bash
cd ../frontend
npm install
```

---

## 🏃 Running the Application

### 1. Start the Backend Server (Port 5000)
```bash
cd backend
npm run dev
```
Output:
```text
=================================================
🚀 Teen Expense Tracker Backend Server Running!
📡 URL: http://localhost:5000
💾 Database: Supabase PostgreSQL (or Local Persistence Engine)
🔒 Security: bcrypt hashing + JWT authentication
=================================================
```

### 2. Start the Frontend Application (Port 5173)
In a separate terminal window:
```bash
cd frontend
npm run dev
```
Open **[http://localhost:5173](http://localhost:5173)** in your browser.

---

## 🧪 Running Automated Tests

A complete automated API test suite is included that validates authentication, bcrypt hashing, expense CRUD, income tracking, category budgets, saving goal deposits, user isolation, and security.

Run the test suite from the `backend/` directory:
```bash
cd backend
npm test
```
Result:
```text
🧪 Starting Teen Expense Tracker Backend API Test Suite...
  ✅ PASS: GET /api/health returns healthy
  ✅ PASS: POST /api/auth/register creates user and issues JWT
  ✅ PASS: POST /api/auth/login succeeds with valid credentials
  ✅ PASS: POST /api/auth/login rejects incorrect password
  ✅ PASS: GET /api/expenses without token returns 401 Unauthorized
  ✅ PASS: POST /api/income records income
  ✅ PASS: POST /api/expenses records expense
  ✅ PASS: POST /api/expenses records second expense
  ✅ PASS: POST /api/expenses rejects negative amount
  ✅ PASS: POST /api/budgets sets budget limit
  ✅ PASS: GET /api/budgets calculates spent & remaining correctly
  ✅ PASS: POST /api/savings creates goal and calculates percentage
  ✅ PASS: POST /api/savings/:id/deposit updates progress correctly
  ✅ PASS: GET /api/dashboard returns correct financial overview
  ✅ PASS: GET /api/suggestions generates educational suggestions
  ✅ PASS: Security: User 2 cannot see User 1 expenses
  ✅ PASS: Security: User 2 cannot delete User 1 expense
🎉 TEST SUMMARY: 17 passed, 0 failed
```

---

## 🗄️ Supabase PostgreSQL Setup

The project is built to work directly with **Supabase PostgreSQL**.

### 1. Create a Supabase Project
1. Log in to your [Supabase Dashboard](https://supabase.com).
2. Click **New Project** and configure your database password and region.

### 2. Run Database Schema
1. Open the **SQL Editor** in your Supabase dashboard.
2. Open the file [`backend/database.sql`](file:///c:/Users/Shreya%20Chourasia/OneDrive/Desktop/shreyansh/backend/database.sql).
3. Copy and paste the entire script into the SQL Editor and click **Run**.
4. This creates all tables (`users`, `expenses`, `income`, `budgets`, `saving_goals`), indexes, foreign keys, and Row Level Security policies.

### 3. Configure Backend Environment
1. In your Supabase dashboard, navigate to **Project Settings** ➔ **API**.
2. Copy your **Project URL**, **Anon Key**, and **service_role Key**.
3. Open [`backend/.env`](file:///c:/Users/Shreya%20Chourasia/OneDrive/Desktop/shreyansh/backend/.env) and populate:
```env
PORT=5000
NODE_ENV=development
JWT_SECRET=your_jwt_secret_key_here

SUPABASE_URL=https://your-project-id.supabase.co
SUPABASE_ANON_KEY=your_anon_key_here
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key_here
```
4. Restart the backend with `npm run dev`. The server will log:
```text
✅ Connected to live Supabase PostgreSQL database at: https://your-project-id.supabase.co
```

> **Zero-Setup Local Dev Engine:** If `SUPABASE_URL` is omitted or left empty, the application automatically runs on a local JSON persistence layer with identical queries and pre-seeded demo data, allowing you to test every feature instantly offline.

---

## 🔑 Demo Account Credentials

For immediate exploration, a pre-seeded account is available:
- **Email:** `demo.teen@example.com`
- **Password:** `teenpassword123`
- *Alternatively, click the "Autofill demo credentials" button on the Login page.*

---

## 📡 REST API Reference

All protected endpoints require an `Authorization: Bearer <jwt_token>` header.

### Authentication Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/register` | Register new teen user (name, email, password, age, currency) |
| `POST` | `/api/auth/login` | Login with email and password, returns JWT token |
| `POST` | `/api/auth/logout` | Client logout acknowledgement |
| `GET` | `/api/auth/me` | Get authenticated user profile |
| `PUT` | `/api/auth/profile` | Update profile information or change password |

### Dashboard Endpoint
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/dashboard` | Get aggregated financial summary, recent activity, and alerts |

### Expenses Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/expenses` | Get expenses (filters: `search`, `category`, `dateFrom`, `dateTo`, `sortBy`, `order`) |
| `POST` | `/api/expenses` | Add new expense (amount, title, category, payment_method, date, note) |
| `GET` | `/api/expenses/:id` | Get specific expense by ID |
| `PUT` | `/api/expenses/:id` | Update expense by ID |
| `DELETE` | `/api/expenses/:id` | Delete expense by ID |

### Income Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/income` | Get all income entries |
| `POST` | `/api/income` | Record income (source, amount, income_date, note) |
| `GET` | `/api/income/:id` | Get specific income record |
| `PUT` | `/api/income/:id` | Update income record |
| `DELETE` | `/api/income/:id` | Delete income record |

### Budget Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/budgets?month=YYYY-MM` | Get category budgets with real-time calculated spending & status |
| `POST` | `/api/budgets` | Create or update category budget |
| `PUT` | `/api/budgets/:id` | Update existing budget |
| `DELETE` | `/api/budgets/:id` | Delete category budget |

### Saving Goals Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/savings` | Get all saving goals with progress percentages |
| `POST` | `/api/savings` | Create saving goal (name, target_amount, saved_amount, target_date, icon) |
| `GET` | `/api/savings/:id` | Get specific goal details |
| `PUT` | `/api/savings/:id` | Update saving goal |
| `POST` | `/api/savings/:id/deposit` | Add pocket money deposit to goal |
| `DELETE` | `/api/savings/:id` | Delete saving goal |

### Analytics & Smart Suggestions
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/analytics` | Category breakdown, monthly history, trend velocity, payment methods |
| `GET` | `/api/suggestions` | Rule-based supportive, educational financial recommendations |

---

## 🔒 Security Best Practices Implemented

- **Password Hashing:** Passwords hashed with `bcryptjs` using 10 salt rounds. Plaintext passwords are never stored or logged.
- **JWT Authorization:** Session tokens verified on every protected request.
- **Tenant Isolation:** Users can never access, edit, or delete another user's records. `user_id` is always derived on the server from the verified JWT token and never trusted from client request bodies.
- **Input Validation:** Positive numeric checks, category whitelisting, valid date checks, and age boundaries (10–25).
- **Error Sanitization:** Internal stack traces are hidden from API client responses.
- **Environment Separation:** API keys and database secrets are isolated in environment variables.

---

## 📄 License
This project is open-source and available under the MIT License.
