# Nifty Dashboard Test Suite

Comprehensive QA test suite for a live Nifty options trading analytics dashboard deployed at `nifty.jeytrade.in`.

## System Under Test

A Flask-based analytics dashboard that tracks two parallel Nifty options paper-trading systems (3-minute and 5-minute Heikin Ashi strategies). The dashboard provides:
- Real-time trade monitoring with auto-refresh
- Daily PnL tracking with Indian-locale formatting
- Historical analytics (equity curves, drawdown, hourly heatmaps)
- REST API endpoints for programmatic access
- Password-protected access via HTTP Basic Auth

**Tech stack:** Python/Flask backend, Chart.js frontend, nginx reverse proxy, systemd services, deployed on Azure VM (Ubuntu 24.04)

## Testing Approach

### UI Automation (Selenium WebDriver + Java)
- Page Object Model (POM) design pattern
- Login flow validation (valid/invalid credentials)
- Dashboard tab navigation (Today ↔ History, 3m ↔ 5m switching)
- Manual refresh button functionality
- Auto-refresh countdown verification
- Chart rendering validation
- Trade table sorting
- Mobile responsive layout testing

### API Testing (REST Assured)
- `/api/3m/stats` and `/api/5m/stats` — JSON schema validation
- `/api/3m/health` and `/api/5m/health` — service health checks
- `/callback` — Zerodha OAuth callback flow
- Authentication enforcement (401 without credentials, 200 with valid auth)
- Response time SLA validation
- Edge cases: malformed parameters, missing fields, expired sessions

### Bug Reports
- [SRI Integrity Block](bug-reports/001-chartjs-sri-integrity.md) — Chart.js blocked by browser due to invalid SRI hash
- [Callback 404](bug-reports/002-callback-404-root-domain.md) — OAuth redirect hitting wrong domain

## Tech Stack (Test Suite)

| Component | Technology |
|-----------|-----------|
| Language | Java 11+ |
| UI Automation | Selenium WebDriver 4.x |
| API Testing | REST Assured |
| Test Framework | TestNG |
| Build Tool | Maven |
| Design Pattern | Page Object Model (POM) |
| CI/CD | GitHub Actions |
| Reporting | ExtentReports / TestNG HTML |

## Project Structure (Planned)
src/
├── main/java/
│   └── pages/           # Page Object classes
│       ├── LoginPage.java
│       ├── TodayDashboardPage.java
│       ├── HistoryDashboardPage.java
│       └── CallbackPage.java
├── test/java/
│   ├── ui/              # Selenium UI tests
│   ├── api/             # REST Assured API tests
│   └── base/            # Test base classes, config
├── test/resources/
│   └── testng.xml       # Test suite configuration
bug-reports/
├── 001-chartjs-sri-integrity.md
└── 002-callback-404-root-domain.md
## Status

🚧 **In Progress** — Building test framework and writing initial test cases.

## About the Author

Career transitioner with 15+ years in US Retirement Services (401k/DC plan operations) at Fidelity Investments. Currently building QA automation skills through hands-on projects. This test suite demonstrates practical testing against a real, live production system I built and deployed.

- 📍 Chennai, India

## License

MIT
