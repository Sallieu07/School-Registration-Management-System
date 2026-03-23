# 🛡️ School Registration Management System

A fully functional, role-based **School Registration Management System** built with pure **HTML, CSS, and JavaScript** — no frameworks, no backend required. Open `index.html` in any modern browser and it works instantly.

---

## 🔗 Repository

```
https://github.com/Sallieu07/School-Registration-Management-System.git
```

Clone the repository:

```bash
git clone https://github.com/Sallieu07/School-Registration-Management-System.git
cd School-Registration-Management-System
```

---

## 📁 Project Structure

```
School-Registration-Management-System/
│
├── index.html        # Main HTML — all views, modals, and page structure
├── styles.css        # All styling — layout, components, animations, themes
├── app.js            # All logic — auth, routing, CRUD, role-based access
└── README.md         # Project documentation
```

> ⚠️ Keep all three files (`index.html`, `styles.css`, `app.js`) in the **same folder**. The HTML references the CSS and JS by relative path.

---

## 🚀 Getting Started

No installation, no build step, no server needed.

1. Clone or download the repository
2. Open `index.html` in your browser
3. Log in with any of the demo credentials below

```bash
# Quick open on macOS
open index.html

# Quick open on Linux
xdg-open index.html

# Quick open on Windows
start index.html
```

---

## 🔐 Demo Credentials

| Role            | Username   | Password      |
|-----------------|------------|---------------|
| Administrator   | `admin`    | `admin123`    |
| Academic Staff  | `staff`    | `staff123`    |
| Lecturer        | `lecturer` | `lecturer123` |
| Student         | `student`  | `student123`  |

---

## 👥 Role-Based Access Control

Each role sees a customised interface with specific permissions:

| Feature                  | Admin | Staff | Lecturer  | Student      |
|--------------------------|:-----:|:-----:|:---------:|:------------:|
| Dashboard                | ✅    | ✅    | ✅        | ✅           |
| My Academic Profile      | ❌    | ❌    | ❌        | ✅           |
| Student Management       | ✅ Edit | ✅ Edit | 👁 View | ❌           |
| Course Management        | ✅ Edit | ✅ Edit | 👁 View | ❌           |
| Attendance & Results     | ✅    | ✅    | ✅        | ❌           |
| User Roles & Access      | ✅    | ❌    | ❌        | ❌           |
| Settings                 | ✅    | ✅    | ✅        | ✅           |

---

## 📸 Features Overview

### 🔐 Login Page
- Clean, responsive login card
- Role-specific authentication
- Demo credentials displayed on screen
- Error feedback for wrong credentials

### 📊 Dashboard
- Live stat cards: Total Students, Active Courses, Average Attendance, Average GPA
- Recent Students panel with GPA and attendance per student
- Upcoming Classes panel with schedule and credits
- **Student-exclusive:** "My Academic Profile" section showing personal GPA, Attendance Rate, and Enrolled Courses

### 🧑‍🎓 Student Management *(Admin & Staff)*
- Full student records table (ID, Name, Age, Grade, GPA, Attendance, Status)
- Live search by name or student ID
- Add new student via modal form
- Edit existing student records
- Delete with confirmation dialog
- Auto-generated Student IDs (STU001, STU002…)

### 📚 Course Management *(Admin & Staff full, Lecturer view-only)*
- Course cards showing: name, code, department, credits, subjects, instructor, enrollment, schedule
- Add / Edit / Delete courses
- View Details button per course

### 📅 Attendance & Results *(Admin, Staff & Lecturer)*
- Course selector dropdown
- **Attendance tab:** Mark students Present/Absent with radio buttons, save by date
- **Results tab:** Enter numeric scores (0–100), auto-calculates letter grade (A–F)
- Pre-seeded sample attendance and results data

### 👔 User Roles & Access *(Admin only)*
- Summary cards per role with user counts
- Full users table with role badges and status
- Add / Edit / Delete users
- Role assignment (Administrator, Academic Staff, Lecturer, Student)

### ⚙️ Settings *(All roles)*
- Profile Information form (username, email, phone, role)
- Change Password with validation
- Notification toggles (Email, SMS, Push)
- System Info panel (version, last updated, database status)

---

## 🎨 Design System

| Property       | Value                               |
|----------------|-------------------------------------|
| Primary Color  | `#0d9e8a` (Teal)                   |
| Display Font   | Sora (Google Fonts)                 |
| Body Font      | DM Sans (Google Fonts)              |
| Border Radius  | `12px` (cards), `8px` (inputs)     |
| Sidebar Width  | `260px`                             |
| Header Height  | `70px`                              |

---

## 🗂️ Data Architecture

All data is stored in a central `store` object in `app.js`. In production this would be replaced with API calls to a backend.

```
store
├── credentials       — demo login map { username: { password, role, name, email } }
├── currentUser       — active session object
├── students[]        — student records
├── courses[]         — course records
├── users[]           — system user accounts
├── attendance{}      — { courseId: { date: { studentId: 'Present'|'Absent' } } }
├── results{}         — { courseId: { studentId: { score, grade } } }
└── pendingDelete     — callback stored until user confirms deletion
```

---

## 🧩 Key Functions Reference

### Authentication
| Function | Description |
|----------|-------------|
| `doLogin()` | Validates credentials, sets session, builds sidebar, navigates to dashboard |
| `doLogout()` | Clears session, returns to login page |

### Navigation
| Function | Description |
|----------|-------------|
| `navigate(view)` | Switches active page, updates topbar, renders content |
| `buildSidebar(role)` | Injects role-specific nav links into sidebar |
| `applyRoleRestrictions(role)` | Shows/hides action buttons based on role |

### CRUD Operations
| Function | Description |
|----------|-------------|
| `saveStudent()` | Add or update a student record |
| `saveCourse()` | Add or update a course |
| `saveUser()` | Add or update a system user |
| `deleteRecord(type, id)` | Shows confirm modal then deletes record |
| `saveAttendance()` | Saves attendance for selected course & date |
| `saveResults()` | Saves exam results for selected course |

### Utilities
| Function | Description |
|----------|-------------|
| `showToast(msg, type)` | Shows a brief success/error notification |
| `initials(name)` | Returns two-letter initials from a name |
| `avatarColor(str)` | Returns a consistent colour for a name |
| `scoreToGrade(score)` | Converts numeric score to letter grade A–F |
| `autoGrade(input)` | Auto-fills grade letter when score is typed |

---

## 🔧 Customisation

### Adding a new student
Edit `store.students` in `app.js`:
```js
{ id: 'STU007', name: 'Your Name', age: 21, grade: 'Year 3', gpa: 3.4, attendance: 90, status: 'Active' }
```

### Adding a new course
Edit `store.courses` in `app.js`:
```js
{ id: 'NEW101', name: 'Course Name', dept: 'Department', credits: 3, instructor: 'Dr. Name', enrolled: 30, schedule: 'Mon, Wed - 10:00 AM', subjects: ['Subject 1', 'Subject 2'] }
```

### Changing the colour theme
Edit the CSS variables in `styles.css`:
```css
:root {
  --primary:      #0d9e8a;   /* main brand colour */
  --primary-dark: #0a7d6e;   /* hover state */
  --primary-light:#e6f7f5;   /* backgrounds */
}
```

### Linking a different student to the student login
Change the `studentAccountId` in `app.js`:
```js
studentAccountId: 'STU001',  // now the student login maps to Emma Johnson
```

---

## 📋 Grade Scale

| Score     | Grade |
|-----------|-------|
| 90 – 100  | A     |
| 80 – 89   | B     |
| 70 – 79   | C     |
| 60 – 69   | D     |
| 0  – 59   | F     |

---

## 🌐 Browser Support

| Browser          | Status  |
|------------------|---------|
| Chrome 90+       | ✅ Full |
| Firefox 88+      | ✅ Full |
| Edge 90+         | ✅ Full |
| Safari 14+       | ✅ Full |
| Opera 76+        | ✅ Full |

---

## 📌 Notes

- All data resets on page refresh (no localStorage — data lives in memory)
- The system is client-side only — safe to open directly from the file system
- To persist data, connect `store` to a REST API or localStorage in `app.js`
- Google Fonts are loaded via CDN — an internet connection is required for typography

---

## 👤 Author

**Sallieu**
- GitHub: [@Sallieu07](https://github.com/Sallieu07)
- Repository: [School-Registration-Management-System](https://github.com/Sallieu07/School-Registration-Management-System.git)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

*Built with ❤️ using HTML, CSS, and JavaScript — no frameworks required.*