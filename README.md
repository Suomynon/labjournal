# Here are your Instructions
# 🚀 **Running the Lab Journal on Your MacBook**

Here's a complete guide to set up and run the electronic lab journal system on your MacBook:

## 📋 **Prerequisites**

### **1. Install Required Software:**

```bash
# Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Python 3.9+
brew install python@3.11

# Install Node.js and npm
brew install node

# Install MongoDB
brew tap mongodb/brew
brew install mongodb-community

# Install Git (if not already installed)
brew install git
```

---

## 📁 **Project Setup**

### **1. Create Project Directory:**

```bash
# Create and navigate to project directory
mkdir lab-journal
cd lab-journal

# Create the directory structure
mkdir -p backend frontend
```

### **2. Set Up Backend (FastAPI):**

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Create requirements.txt file
cat > requirements.txt << EOF
fastapi==0.110.1
uvicorn==0.25.0
motor==3.3.1
pymongo==4.5.0
pydantic>=2.6.4
email-validator>=2.2.0
pyjwt>=2.10.1
passlib>=1.7.4
bcrypt>=4.0.1
python-dotenv>=1.0.1
python-multipart>=0.0.9
cryptography>=42.0.8
python-jose>=3.3.0
EOF

# Install Python dependencies
pip install -r requirements.txt
```

### **3. Create Backend Environment File:**

```bash
# Create .env file in backend directory
cat > .env << EOF
MONGO_URL=mongodb://localhost:27017
DB_NAME=lab_journal
JWT_SECRET=lab-journal-secret-key-change-in-production-2025
EOF
```

### **4. Set Up Frontend (React):**

```bash
# Navigate back to project root and go to frontend
cd ../frontend

# Create React app
npx create-react-app . --template typescript
# Choose "y" when prompted about creating in existing directory

# Install additional dependencies
npm install axios

# Install Tailwind CSS
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# Configure Tailwind (update tailwind.config.js)
cat > tailwind.config.js << EOF
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
EOF

# Create frontend environment file
cat > .env << EOF
REACT_APP_BACKEND_URL=http://localhost:8001
EOF
```

---

## 💾 **Add the Application Code**

### **1. Backend Code:**

```bash
# In backend directory, create server.py
cd ../backend
```

Copy the complete `server.py` code I built earlier into this file, or create it with your preferred text editor.

### **2. Frontend Code:**

```bash
# In frontend/src directory
cd ../frontend/src
```

Replace the contents of `App.js` and `App.css` with the code I built earlier.

Update `src/index.css` to include Tailwind:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## 🗄️ **Database Setup**

### **1. Start MongoDB:**

```bash
# Start MongoDB service
brew services start mongodb/brew/mongodb-community

# Verify MongoDB is running
brew services list | grep mongodb
```

### **2. Create Database (Optional - will be created automatically):**

```bash
# Connect to MongoDB shell (optional, for verification)
mongosh

# In MongoDB shell:
use lab_journal
show collections
exit
```

---

## 🏃‍♂️ **Running the Application**

### **1. Start the Backend:**

```bash
# Open a new terminal and navigate to backend directory
cd /path/to/your/lab-journal/backend

# Activate virtual environment
source venv/bin/activate

# Start the FastAPI server
uvicorn server:app --host 0.0.0.0 --port 8001 --reload
```

You should see:
```
INFO:     Uvicorn running on http://0.0.0.0:8001 (Press CTRL+C to quit)
INFO:     Started reloader process
INFO:     Started server process
INFO:     Waiting for application startup.
INFO:     Application startup complete.
```

### **2. Start the Frontend:**

```bash
# Open another terminal and navigate to frontend directory
cd /path/to/your/lab-journal/frontend

# Start the React development server
npm start
```

The frontend should automatically open in your browser at `http://localhost:3000`.

---

## 🔑 **Initial Setup & Login**

### **1. Default Admin Account:**

The system automatically creates an admin account:
- **Email:** `admin@lab.com`
- **Password:** `admin123`

### **2. First Login:**

1. Go to `http://localhost:3000`
2. Login with the admin credentials
3. You'll see the dashboard with your role as "admin"

### **3. Verify Everything Works:**

- **Dashboard:** Should show statistics (initially empty)
- **Chemical Inventory:** You can add chemicals
- **Experiments:** You can create experiments
- **Admin Panel:** Full access to user/role management and activity logs

---

## 🛠️ **Development Workflow**

### **Daily Development:**

```bash
# Terminal 1: Backend
cd lab-journal/backend
source venv/bin/activate
uvicorn server:app --host 0.0.0.0 --port 8001 --reload

# Terminal 2: Frontend  
cd lab-journal/frontend
npm start

# Terminal 3: MongoDB (if needed)
mongosh
```

### **Stopping Services:**

```bash
# Stop FastAPI: Ctrl+C in backend terminal
# Stop React: Ctrl+C in frontend terminal
# Stop MongoDB: 
brew services stop mongodb/brew/mongodb-community
```

---

## 🔧 **Troubleshooting**

### **Common Issues:**

**1. MongoDB Connection Error:**
```bash
# Check if MongoDB is running
brew services list | grep mongodb

# Restart MongoDB if needed
brew services restart mongodb/brew/mongodb-community
```

**2. Port Already in Use:**
```bash
# Kill process on port 8001 (backend)
lsof -ti:8001 | xargs kill -9

# Kill process on port 3000 (frontend)
lsof -ti:3000 | xargs kill -9
```

**3. Python Dependencies:**
```bash
# Reinstall dependencies
cd backend
source venv/bin/activate
pip install --upgrade -r requirements.txt
```

**4. Node Dependencies:**
```bash
# Clear npm cache and reinstall
cd frontend
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

---

## 📱 **Accessing the Application**

### **URLs:**
- **Frontend:** `http://localhost:3000`
- **Backend API:** `http://localhost:8001`
- **API Documentation:** `http://localhost:8001/docs`

### **Features to Test:**
1. **Login** with admin credentials
2. **Add chemicals** to inventory
3. **Create experiments** linking chemicals
4. **Manage users** in Admin Panel
5. **Create custom roles** with specific permissions
6. **View activity logs** to see all actions

---

## 🚀 **Production Deployment (Optional)**

For production deployment, you would need to:

1. **Set up a production database** (MongoDB Atlas)
2. **Configure environment variables** for production
3. **Build the React app** (`npm run build`)
4. **Deploy to a cloud service** (AWS, DigitalOcean, etc.)
5. **Set up HTTPS** and proper domain
6. **Configure production security** settings

---

## ✅ **Verification Checklist**

- [ ] MongoDB is running
- [ ] Backend starts without errors
- [ ] Frontend loads in browser
- [ ] Can login with admin credentials
- [ ] Dashboard shows statistics
- [ ] Can create chemicals and experiments
- [ ] Admin panel is accessible
- [ ] Activity logs are recording actions

**You now have a fully functional electronic lab journal running locally on your MacBook!** 🎉
