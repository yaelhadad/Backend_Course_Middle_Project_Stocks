# 📈 StockInfo - Stock Management Platform

Django web application for managing stock information with real-time data and AI insights.

## ⚙️ Running the Application

This project is designed to run seamlessly in different environments: locally for development and on cloud platforms (like AWS) for production. The key to this flexibility lies in **Environment Variables**. These variables allow you to configure the application's behavior (e.g., connecting to a local database vs. AWS RDS, or serving media files locally vs. from AWS S3) without changing the core code.

### How Environment Variables Work:

*   **Local Development (`.env` file):** For running the application on your local machine, you'll use a `.env` file in the project's root. This file stores configuration specific to your development setup, such as using a local SQLite database (`USE_RDS=False`) and local media files (`USE_S3=False`). This keeps your sensitive production credentials safe and out of your version control.
*   **Production Deployment (System Environment Variables):** When deploying to a live server or cloud environment, you'll set these variables directly in the system's environment. This means the application will connect to services like AWS RDS for a PostgreSQL database (`USE_RDS=True`) and AWS S3 for media storage (`USE_S3=True`). This approach is crucial for security, scalability, and flexibility in a production setting.

By managing these variables, you can ensure the application adapts its behavior to the specific environment it's running in, using the same codebase.

## 🌟 Features

- **📊 Stock Management**: Browse and view detailed stock information
- **🔐 User Authentication**: Signup, login, logout system
- **👥 User Reviews**: Rate and review stocks (authenticated users only)
- **🤖 Advanced AI Features**: Company summaries, news analysis, market insights, price predictions (login required)
- **📈 Real-time Data**: Live stock prices via Alpha Vantage API
- **🎯 Admin Panel**: Full control over stocks and reviews

## 🛠️ Tech Stack

- **Backend**: Django 5.2.5, SQLite3
- **Frontend**: Bootstrap 5, HTML5, CSS3
- **APIs**: Google Gemini (AI), Alpha Vantage (stock data)עםא
- **Authentication**: Django built-in system

## 🚀 Installation & Setup

### Prerequisites
- Python 3.8+ installed
- pip package manager
- Git (optional)

### Step 1: Clone/Download Project
```bash
# If using Git:
git clone <repository-url>
cd Final_Project

# Or download ZIP and extract
```

### Step 2: Create Virtual Environment (Recommended)
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Environment Variables Setup
Create a `.env` file in the project root:

```env
# General Django settings
SECRET_KEY=your_insecure_local_secret_key # For local development only, DO NOT use in production!
DEBUG=True
ALLOWED_HOSTS=127.0.0.1,localhost

# Database settings (for local SQLite)
USE_RDS=False # Set to True in production for PostgreSQL/RDS

# Media storage settings (for local files)
USE_S3=False # Set to True in production for AWS S3

# API Keys
GEMINI_API_KEY=your_gemini_api_key_here
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_api_key_here
NEWS_API_KEY=your_news_api_key_here

# Example for RDS/S3 in production (DO NOT include actual production secrets here locally)
# RDS_DB_USER=your_rds_user
# RDS_DB_PASSWORD=your_rds_password
# RDS_DB_HOST=your_rds_endpoint
# AWS_ACCESS_KEY_ID=your_aws_access_key
# AWS_SECRET_ACCESS_KEY=your_aws_secret_key
# AWS_STORAGE_BUCKET_NAME=your_s3_bucket_name
```

**Important:** The `.env` file is for **local development only** and should **NEVER** be committed to version control (e.g., Git). Make sure it's added to your `.gitignore` file.

**Get API Keys:**
- **Gemini AI**: https://makersuite.google.com/app/apikey
- **Alpha Vantage**: https://www.alphavantage.co/support/#api-key
- **NewsAPI**: https://newsapi.org/register (Free: 1000 requests/day)

### Step 5: Database Setup
```bash
# Apply migrations
python manage.py migrate

# Create superuser (admin)
python manage.py createsuperuser

# Load initial stock data (optional)
python manage.py shell
>>> exec(open('stocks/manage_stocks_update_db.py').read())
>>> exit()
```

### Step 6: Run Development Server
```bash
python manage.py runserver
```

Visit: http://127.0.0.1:8000/

## ☁️ Running in Production

For production deployments (e.g., on an AWS EC2 instance, Docker, or other cloud platforms), environment variables should be set directly in the deployment environment rather than using a `.env` file. This ensures security and proper configuration for services like AWS RDS and S3.

Here's an example of environment variables you would set in your production environment:

```bash
# General Django settings for production
export SECRET_KEY="your_strong_production_secret_key" # GENERATE A STRONG, UNIQUE KEY!
export DEBUG=False
export ALLOWED_HOSTS="yourdomain.com,www.yourdomain.com"

# Database settings for AWS RDS (PostgreSQL)
export USE_RDS=True
export RDS_DB_USER="your_rds_username"
export RDS_DB_PASSWORD="your_rds_password"
export RDS_DB_HOST="your_rds_endpoint"
export RDS_DB_PORT="5432"

# Media storage settings for AWS S3
export USE_S3=True
export AWS_ACCESS_KEY_ID="your_aws_access_key_id"
export AWS_SECRET_ACCESS_KEY="your_aws_secret_access_key"
export AWS_STORAGE_BUCKET_NAME="your_s3_bucket_name"
export AWS_REGION="us-east-1" # Or your desired AWS region

# API Keys
export GEMINI_API_KEY="your_production_gemini_api_key"
export ALPHA_VANTAGE_API_KEY="your_production_alpha_vantage_api_key"
export NEWS_API_KEY="your_production_news_api_key"
```

**Why this is optimal for Production:**

*   **Security:** Keeps sensitive credentials out of your codebase and allows them to be managed securely by your deployment platform.
*   **Flexibility:** Allows the same codebase to be deployed across different environments with unique configurations.
*   **Scalability:** Integrates well with containerization (Docker) and orchestration (Kubernetes) systems.

## 🎯 Usage

**Regular Users:**
- Browse stocks and view details
- Login for AI insights and reviews
- Rate and comment on stocks

**Administrators:**
- Manage stocks via `/admin/`
- Monitor user reviews
- Add/edit stock information

## 🤖 Advanced AI Features

**Four Powerful AI Analysis Tools** (Login Required):

1. **📝 Company Summary** - What the company does in simple terms
2. **📰 News Analysis** - Recent news + AI investment insights
3. **📊 Market Analysis** - Industry position, growth potential, investment recommendation
4. **🔮 Price Prediction** - Technical analysis & future outlook

**Powered by:**
- **Google Gemini AI** for intelligent analysis
- **NewsAPI** for real-time financial news
- **Alpha Vantage** for live market data

**Features:**
- Multi-language support (Hebrew/English)
- Real-time news aggregation
- Professional investment insights
- Educational disclaimers for responsible investing

## 🔐 Security

- Django built-in password hashing
- CSRF protection
- Authentication-gated premium features
- Admin-only stock management

## 🔧 Troubleshooting

### Common Issues:

**1. ModuleNotFoundError**
```bash
# Make sure virtual environment is activated
venv\Scripts\activate  # Windows
# Then reinstall requirements
pip install -r requirements.txt
```

**2. API Key Errors**
- Check `.env` file exists in project root
- Verify API keys are valid and active
- Ensure no extra spaces in `.env` file

**3. Database Errors**
```bash
# Reset database (WARNING: deletes all data)
rm db.sqlite3
python manage.py migrate
python manage.py createsuperuser
```

**4. Static Files Not Loading**
```bash
python manage.py collectstatic
```

## 📂 Project Structure
```
Final_Project/
├── db.sqlite3              # Database file
├── manage.py               # Django management script
├── requirements.txt        # Python dependencies
├── .env                   # Environment variables (create this)
├── media/logos/           # Stock company logos
├── stockinfo/             # Main Django project
│   ├── settings.py        # Django settings
│   ├── urls.py           # Main URL routing
│   └── ...
└── stocks/                # Stocks app
    ├── models.py          # Database models
    ├── views.py           # View logic
    ├── urls.py           # App URL routing
    ├── templates/         # HTML templates
    ├── static/           # CSS/JS files
    └── ...
```


