<!-- ████████████████████████████████████████████████ -->
<!--   Save banner.svg and this file in same repo   -->
<!--   Then upload both to your GitHub profile repo -->
<!-- ████████████████████████████████████████████████ -->

<div align="center">

![banner](./ems_banner.svg)

</div>

---

<div align="center">

```
╔══════════════════════════════════════════════════════════════╗
║          EMPLOYEE MANAGEMENT SYSTEM  [ C Language ]         ║
║    Admin Access  ·  Employee Portal  ·  Persistent Storage  ║
╚══════════════════════════════════════════════════════════════╝
```

</div>

---

## 📌 About

A terminal-based **Employee Management System** written in pure **C**, featuring dual-role access (Admin & Employee), binary file persistence, dynamic memory management, and a complete leave workflow — all without any external libraries.

> Built as a hands-on demonstration of C fundamentals: `structs`, `malloc/realloc`, `fread/fwrite`, `pointers`, and modular function design.

---

## ⚙️ Features

### 🔐 Admin Panel
| Feature | Description |
|--------|-------------|
| ➕ Add Employee | Auto-generates default password (`name+id`) |
| ✏️ Update Employee | Name, salary, leave quota, or password reset |
| 🗑️ Delete Employee | Soft-delete (marks `isActive = 0`) |
| 🔍 Search Employee | Lookup by Employee ID |
| 📋 View All | Lists all currently active employees |
| ✅ Manage Leaves | Approve or reject pending leave requests |
| 🔑 Change Password | Secure old → new → confirm flow |

### 👤 Employee Portal
| Feature | Description |
|--------|-------------|
| 👁️ View Details | Salary, leaves taken, leave balance |
| 📝 Request Leave | Submit leave days for admin approval |
| 📊 Check Status | View Pending / Approved / Rejected result |
| 🔒 Change Password | Self-service password update |

---

## 🏗️ Architecture

```
main()
 ├── adminMenu()
 │    ├── addEmployee()       → ensureCapacity() + dynamic array append
 │    ├── updateEmployee()    → in-place struct field update
 │    ├── deleteEmployee()    → soft-delete (isActive flag)
 │    ├── searchEmployee()    → findActiveEmployeeIndex()
 │    ├── viewAllEmployees()  → linear scan with isActive filter
 │    ├── manageLeaveRequests() → leaveRequestStatus state machine
 │    └── changeAdminPassword()
 │
 └── employeeLogin()
      └── employeeMenu()
           ├── requestLeave()       → sets leaveRequestStatus = 1 (Pending)
           ├── checkLeaveStatus()   → reads + resets status after viewing
           └── changeEmployeePassword()

Persistence Layer
 ├── loadEmployees()  / saveEmployees()   → employees.dat  (binary)
 └── loadAdminPassword() / saveAdminPassword() → admin.dat (binary)
```

---

## 📂 Project Structure

```
.
├── ems.c            ← Full source (single-file)
├── employees.dat    ← Auto-created at runtime (binary)
├── admin.dat        ← Auto-created at runtime (binary)
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- GCC or any ANSI C99 compiler
- Linux / macOS / Windows (WSL or MinGW)

### Build & Run

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/employee-management-system-c.git
cd employee-management-system-c

# Compile
gcc ems.c -o ems

# Run
./ems
```

### Default Credentials

| Role | Username | Password |
|------|----------|----------|
| Admin | `admin` | `admin123` |
| Employee | `<Employee ID>` | `<name><id>` (auto-generated) |

> Example: Employee "Vijay" with ID 101 → default password is `Vijay101`

---

## 💾 Data Persistence

All data is stored in **binary files** using `fread` / `fwrite`:

```c
// Save
fwrite(&empCount, sizeof(int), 1, fp);
fwrite(employees, sizeof(Employee), empCount, fp);

// Load
fread(&count, sizeof(int), 1, fp);
fread(employees, sizeof(Employee), count, fp);
```

The dynamic array doubles in capacity via `realloc` when full — a simple but effective growable buffer.

---

## 🔄 Leave Request State Machine

```
Employee submits request
        │
        ▼
  [1] PENDING  ──── Admin approves ──▶  [2] APPROVED
        │                                     │
        └──── Admin rejects  ──▶  [3] REJECTED
                                              │
                             Employee checks status ──▶ [0] RESET
```

---

## 🛡️ Security Notes

- Passwords stored as plain text in binary files *(for educational purposes)*
- Input validation on all `scanf` calls with `clearInputBuffer()`
- Soft-delete pattern prevents accidental data loss
- Admin password change requires old password verification + confirm step

---

## 🧰 Tech Stack

![C](https://img.shields.io/badge/Language-C-00599C?style=flat-square&logo=c&logoColor=white)
![GCC](https://img.shields.io/badge/Compiler-GCC-A42E2B?style=flat-square&logo=gnu&logoColor=white)
![Linux](https://img.shields.io/badge/Platform-Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Terminal](https://img.shields.io/badge/Interface-Terminal-000000?style=flat-square&logo=gnometerminal&logoColor=white)

---

## 👨‍💻 Author

**Vijay Kumar**
B.E. — Electrical & Electronics Engineering | PVKK Institute of Technology
Embedded Systems Intern @ Cranes Varsity Pvt. Ltd. *(Best Intern Award 🏆)*

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/YOUR_USERNAME)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/YOUR_LINKEDIN)

---

<div align="center">

*"Writing C is like building with bare hands — no abstractions, just raw control."*

</div>
