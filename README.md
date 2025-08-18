# 📈 StockInfo - Stock Management Platform

Django web application for managing stock information with real-time data and AI insights.

## 🌟 Features

- **📊 Stock Management**: Browse and view detailed stock information
- **🔐 User Authentication**: Signup, login, logout system
- **👥 User Reviews**: Rate and review stocks (authenticated users only)
- **🤖 Advanced AI Features**: Company summaries and news analysis with investment insights (login required)
- **📈 Real-time Data**: Live stock prices via Alpha Vantage API
- **🎯 Admin Panel**: Full control over stocks and reviews

## 🛠️ Tech Stack

- **Backend**: Django 5.2.5, SQLite3
- **Frontend**: Bootstrap 5, HTML5, CSS3
- **APIs**: Google Gemini (AI analysis), Alpha Vantage (stock data + news)
- **Authentication**: Django built-in system
- **Dependencies**: See `requirements.txt` for full list

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
GEMINI_API_KEY=your_gemini_api_key_here
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_api_key_here
```

**Get API Keys:**
- **Gemini AI**: https://makersuite.google.com/app/apikey (Free tier available)
- **Alpha Vantage**: https://www.alphavantage.co/support/#api-key (Free: 25 requests/day)

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

**Two Powerful AI Analysis Tools** (Login Required):

1. **📝 Company Summary** - AI explains what the company does in simple terms
2. **📰 Latest News + AI Analysis** - Recent financial news with intelligent investment insights

**Powered by:**
- **Google Gemini AI** for intelligent analysis and content generation
- **Alpha Vantage API** for live market data AND financial news

**How it works:**
- **AI Summary**: Uses company description to generate simple explanations
- **News Analysis**: Fetches 3 latest news articles, then AI analyzes them for investment insights
- **Fallback system**: Always provides useful content even when APIs are down
- **Smart caching**: Updates stock prices every 60 minutes to save API calls

**Features:**
- Single sentence AI summaries (fast and concise)
- Real-time financial news from Alpha Vantage
- Fallback links to Yahoo Finance & MarketWatch
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
- Check `.env` file exists in project root with both required keys
- Verify API keys are valid and active
- Ensure no extra spaces in `.env` file
- **Note**: Only GEMINI_API_KEY and ALPHA_VANTAGE_API_KEY are required
- News feature uses Alpha Vantage (same API key as stock data)

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

