# MLM Binary Tree Application

A complete Multilevel Marketing (MLM) system with Binary Tree structure built with Node.js and file-based JSON storage.

## 🌟 Features

- **Binary Tree Structure**: Each member can have one left and one right downline member
- **Intelligent Spill Logic**: Automatically places new members in the next available slot when a position is filled
- **Member Registration**: Join under a sponsor with position selection (Left/Right)
- **Authentication System**: Secure login with bcrypt password hashing
- **Dashboard**: View team statistics and member counts
- **Profile Management**: View personal details and account information
- **Downline Tracking**: Monitor left and right team members with detailed information
- **Real-time Counters**: Track total left and right team counts

## 🏗️ Project Structure

```
Multilevel/
├── database/
│   ├── db.js              # File-based JSON database operations
│   └── data/              # Auto-generated data storage
│       ├── members.json   # Members database
│       └── counter.json   # Member ID counter
├── models/
│   └── Member.js          # Member model with business logic
├── routes/
│   ├── auth.js            # Authentication routes
│   └── member.js          # Member dashboard routes
├── views/
│   ├── login.ejs          # Login page
│   ├── register.ejs       # Registration form
│   ├── dashboard.ejs      # Member dashboard
│   ├── profile.ejs        # Profile view
│   └── downline.ejs       # Downline team view
├── server.js              # Main application server
├── package.json           # Dependencies
└── README.md              # This file
```

## 📋 Requirements

- Node.js (v14 or higher)
- npm (Node Package Manager)

## 🚀 Installation

1. **Install Dependencies**
```powershell
npm install
```

2. **Create Root Member** (First member in the system)
```powershell
node createRootMember.js
```

This will create the first member with:
- **Member Code**: MEM1001
- **Email**: admin@mlm.com
- **Password**: admin123

3. **Start the Application**
```powershell
npm start
```

4. **Open in Browser**
```
http://localhost:3000
```

## 📖 How to Use

### 1. Login
- Navigate to `http://localhost:3000`
- Use the root member credentials:
  - Email: `admin@mlm.com`
  - Password: `admin123`

### 2. Register New Members
- Click "Register Now" or access `/register`
- Fill in the member details:
  - Name, Email, Mobile
  - **Sponsor Code**: Enter the code of your sponsor (e.g., MEM1001)
  - **Position**: Choose Left or Right
  - Password
- If the selected position is already filled, the system will automatically place the member in the next available slot using **spill logic**

### 3. View Dashboard
- See total team counts
- View left and right team statistics
- Access quick actions

### 4. Check Profile
- View personal information
- See sponsor details
- Check team counts

### 5. View Downline
- See all members in your left team
- See all members in your right team
- View detailed member information

## 🔄 Binary Tree & Spill Logic

### How it Works

1. **Each member can have**:
   - One LEFT child
   - One RIGHT child

2. **Spill Logic**:
   - If you select LEFT position and sponsor's left is already filled
   - System traverses down the left branch
   - Finds the first available left slot recursively
   - Places the new member there
   - Same applies for RIGHT position

3. **Count Updates**:
   - When a new member joins, counts are updated recursively upward
   - Each member's `leftCount` and `rightCount` reflect their total downline

### Example

```
        MEM1001 (Root)
       /              \
  MEM1002 (L)      MEM1003 (R)
    /    \            /    \
MEM1004  MEM1005  MEM1006  MEM1007
```

If you join under MEM1001 with LEFT position:
- If MEM1002 exists, system checks MEM1002's left
- If MEM1004 exists, system checks MEM1004's left
- Places you in the first empty left slot

## 🛠️ API Routes

### Authentication
- `GET /` - Home (redirects to login or dashboard)
- `GET /login` - Login page
- `POST /login` - Login submission
- `GET /register` - Registration page
- `POST /register` - Registration submission
- `GET /logout` - Logout

### Member Dashboard
- `GET /member/dashboard` - Member dashboard
- `GET /member/profile` - Profile view
- `GET /member/downline` - Downline team view

## 💾 Data Storage

The application uses a file-based JSON storage system:

- **members.json**: Stores all member data
- **counter.json**: Tracks the last member ID for generating unique codes
- No external database required - perfect for development and testing

## 🔒 Security Features

- Password hashing with bcrypt
- Session-based authentication
- Protected routes with authentication middleware
- Input validation and error handling

## 🎨 Features Highlights

✅ **Member Joining Form** with sponsor validation  
✅ **Position Selection** (Left/Right)  
✅ **Automatic Spill Logic** for filled positions  
✅ **Recursive Tree Traversal**  
✅ **Real-time Count Updates**  
✅ **Secure Login System**  
✅ **Profile Management**  
✅ **Downline Visualization**  
✅ **Responsive Design**  

## 📝 Notes

- First member (root) has no sponsor
- Member codes are auto-generated (MEM1001, MEM1002, etc.)
- All passwords are hashed and securely stored
- Data persists between application restarts
- The system handles unlimited depth in the binary tree

## 🐛 Troubleshooting

**Port already in use:**
```powershell
# Change PORT in server.js or set environment variable
$env:PORT=3001; npm start
```

**Cannot find module:**
```powershell
npm install
```

**Database not found:**
- The database files are auto-created on first run
- Run `node createRootMember.js` to initialize

## 📄 License

ISC

## 👨‍💻 Support

For issues or questions, please check the code comments or create an issue in the repository.

---

**Happy Network Building! 🌟**
