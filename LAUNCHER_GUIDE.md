# 🍔 Food Shop - Multi-Service Launcher

## Quick Start (One Command to Rule Them All!)

Launch the entire application with one command:

### Windows (PowerShell)
```powershell
.\start.ps1
```

### Windows (Batch)
```cmd
start.bat
```

### Linux / macOS
```bash
chmod +x start.sh
./start.sh
```

## What Gets Started?

The launcher automatically starts **3 services** on different ports:

| Service | URL | Port | Purpose |
|---------|-----|------|---------|
| **Frontend (UI)** | http://localhost:3000/index.html | 3000 | Order interface |
| **API Backend** | http://localhost:8001 | 8001 | REST API endpoints |
| **Database** | ./food_shop.db | - | SQLite database |

## Service Details

### 1. **Frontend Server** (Port 3000)
- Serves the HTML/CSS/JavaScript interface
- Static HTTP server using Python's built-in module
- Browse menu, add items to cart, place orders

**Access:** `http://localhost:3000/index.html`

### 2. **API Server** (Port 8001)
- FastAPI with auto-reload for development
- Handles all business logic
- CORS enabled for cross-origin requests
- Interactive API documentation available

**Access:** `http://localhost:8001/docs`

### 3. **Database** (SQLite)
- Automatically created on first run
- Seeded with 12 sample food items
- Located at: `./food_shop.db`

## How the Communication Works

```
User Browser (localhost:3000)
         ↓
   Frontend Server
         ↓
  Makes HTTP requests
         ↓
   API Server (localhost:8001)
         ↓
   Processes & queries
         ↓
   SQLite Database
```

## What Happens on Startup

1. ✅ Virtual environment activated
2. ✅ Database initialized (tables created)
3. ✅ Sample foods seeded (if needed)
4. ✅ Frontend server started on port 3000
5. ✅ API server started on port 8001 with auto-reload
6. ✅ All services ready to use

## Stopping The Application

Simply press **`Ctrl+C`** in the terminal. All services will gracefully shut down.

## Complete API Endpoints

### Foods
```
GET  /api/v1/foods              - List all foods
GET  /api/v1/foods/{id}         - Get food by ID
POST /api/v1/foods              - Create new food
PUT  /api/v1/foods/{id}         - Update food
DELETE /api/v1/foods/{id}       - Delete food
```

### Orders
```
POST /api/v1/orders                    - Create order
GET  /api/v1/orders                    - List all orders
GET  /api/v1/orders/{id}               - Get order by ID
PUT  /api/v1/orders/{id}               - Update order
PATCH /api/v1/orders/{id}/confirm      - Confirm order
PATCH /api/v1/orders/{id}/deliver      - Mark delivered
```

### Payments
```
POST /api/v1/payments                       - Create payment
GET  /api/v1/payments                       - List all payments
GET  /api/v1/payments/{id}                  - Get payment
POST /api/v1/payments/{id}/confirm          - Confirm payment
```

## Sample Data

The database comes pre-loaded with **12 delicious food items**:

- 🍔 Classic Hamburger - $8.99
- 🥗 Caesar Salad - $9.99
- 🍕 Pepperoni Pizza - $12.99
- 🍝 Margherita Pizza - $11.99
- 🍗 Grilled Chicken Burger - $10.99
- 🌯 Vegetarian Wrap - $8.99
- 🥙 Greek Salad - $9.99
- 🍗 Crispy Chicken Wings - $7.99
- 🥖 Garlic Bread - $3.99
- 🍟 French Fries - $3.49
- 🍰 Chocolate Cake - $4.99
- 🎂 Cheesecake - $5.99

## Troubleshooting

### Port Already In Use
If a port is already in use, modify `run.py`:
```python
FRONTEND_PORT = 3000  # Change to 3001, 3002, etc.
API_PORT = 8001       # Change to 8002, 8003, etc.
```

Then update the API_BASE in `index.html` to match the new API port.

### Virtual Environment Issues
If the virtual environment doesn't activate:
```powershell
# Windows PowerShell
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# Then run
python run.py
```

### Database Reset
Delete the database file and restart:
```bash
rm food_shop.db      # Linux/Mac
del food_shop.db     # Windows
# Then run the launcher again
```

### CORS Errors
Already handled! The API is configured with CORS enabled for all origins.

## Development Mode Features

The launcher includes:
- ✅ **Fast Reload** - API auto-reloads on code changes
- ✅ **Easy Debugging** - Watch server logs in real-time
- ✅ **Sample Data** - Pre-populated with realistic food items
- ✅ **API Documentation** - Interactive Swagger UI at /docs
- ✅ **Multiple Services** - All running independently

## Architecture Overview

```
food_shop/
├── index.html            # Frontend UI
├── main.py               # FastAPI app
├── run.py                # Multi-service launcher
├── start.ps1             # PowerShell launcher
├── start.bat             # Batch launcher
├── start.sh              # Bash launcher
├── seed_foods.py         # Database seeder
├── requirements.txt      # Python dependencies
└── app/
    ├── routes/          # API endpoints
    ├── models/          # Database models
    ├── schemas/         # Request/response schemas
    ├── services/        # Business logic
    ├── repositories/    # Data access
    └── core/           # Config & database
```

## Usage Workflow

1. **Open the launcher** based on your OS (start.ps1, start.bat, or start.sh)
2. **Wait** for all services to start (you'll see "All Services Started Successfully!")
3. **Open** http://localhost:3000/index.html in your browser
4. **Browse** the menu and place an order
5. **Press Ctrl+C** when done to stop all services

## Environment Variables

The launcher handles everything automatically. No configuration needed!

But if you want to customize:
```python
# Edit run.py
FRONTEND_PORT = 3000   # Change port
API_PORT = 8001        # Change port
BACKEND_HOST = "127.0.0.1"  # Change host
```

## Advanced: Running Services Individually

### Start only the API:
```bash
python -m uvicorn main:app --reload --host 127.0.0.1 --port 8001
```

### Start only the Frontend:
```bash
python -m http.server 3000 --bind 127.0.0.1
```

### Seed database separately:
```bash
python seed_foods.py
```

---

## 📚 Related Files

- [FRONTEND_README.md](FRONTEND_README.md) - Frontend detailed guide
- [README.md](README.md) - Project overview
- [requirements.txt](requirements.txt) - Python dependencies

**Happy serving! 🍔✨**
