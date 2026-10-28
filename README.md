# After School Program System

A powerful and comprehensive school management system tailored for after-school programs. This system streamlines student tracking, assignment automation, attendance management, fee collection, and detailed analytics for parents and administrators.

## 🚀 Features

### 1. Authentication & Accounts
- JWT-based login / logout.
- Public registration for **Super Admin**, **Center Admin** and **Parent** accounts.
- View own profile, update profile (name, phone, address, profile photo) and change password.
- Activate / deactivate any user account — inactive users are blocked at login.
- Role-based access control via `role` middleware (`super_admin`, `center_admin`, `teacher`, `student`, `parent`).

### 2. Center Management
- Create, list, update and delete centers (name, address, city, phone, active flag, assigned center admin).
- View a single center and its statistics.
- List and delete center admins.

### 3. Teacher Management
- Create, list, view, update and delete teachers (with user account and profile photo).
- Assign / unassign students to a teacher.
- View the students assigned to a teacher.
- Teacher dashboard (assigned students, pending submissions, recent submissions).

### 4. Student Management
- Create students with a login account; **enrollment number is auto-generated** (`S-YYM101`, `S-YYM102`, …).
- Store date of birth, grade, enrollment date, subjects, current level, monthly fee, parent and teacher.
- List, view, update and delete students.
- Per-student views: assignments, attendance, fees, progress and full report.
- Student dashboard and "my assignments" list.

### 5. Subjects & Levels
- Subjects: create, update, activate/deactivate, list active subjects, list all subjects.
- Levels: create, update, delete and list.

### 6. Worksheet Library
- Upload PDF worksheets (max 10 MB) with subject, level, worksheet number, description, total marks and time limit.
- Filter worksheets by subject and level.
- Update, delete, view and download worksheets.

### 7. Assignments
- Bulk-assign a worksheet to multiple students with a due date and notes.
- List assignments (filter by student / status), view, update (due date, notes, status) and cancel.
- Status flow: `assigned` → `submitted` → `graded` (or `returned`).

### 8. Submissions & Grading
- Students upload their completed work (PDF / JPG / PNG, max 10 MB) with time taken.
- List all submissions, pending (ungraded) submissions, and submissions per assignment.
- View and download a submission file.
- Grade a submission with score (0–100), error count and feedback; re-grade later if needed.
- **Student progress is updated automatically on grading** — worksheets completed, average score and average time per subject/level.

### 9. Attendance
- Bulk mark attendance for a date (`present`, `absent`, `late`) with notes.
- Edit a single attendance record.
- View today's attendance and attendance history.
- Monthly attendance summary by status.

### 10. Fee Management
- Bulk-generate monthly fees for all active students of a center (amount taken from each student's `monthly_fee`, duplicates skipped).
- List fees with filters (student, month, status), view all fees of a center, view a single fee.
- Update a fee record and mark it as paid (payment method, transaction ID, paid date).
- Mark unpaid fees past their due date as `overdue`; list unpaid/overdue fees.
- Fee collection summary report.

### 11. Parent Portal
- Parent dashboard with an overview of all their children.
- View children's reports, attendance, assignments and fees.

### 12. Reports & Analytics
- Role-based dashboard KPIs for every role.
- Super Admin dashboard and full-system report (centers, students, revenue, attendance and submission rates, center-wise distribution).
- Center performance report and detailed 360° center report (financial, academic, operational).
- Teacher performance report.
- Student detailed report.
- Fee collection report (monthly revenue trend).
- Attendance report.
- Level progression report.

---

## 👥 What Each User Can Do

### 🛡️ Super Admin
- Everything in the system across **all centers**.
- Create, update, delete and view centers and their stats; list and delete center admins.
- Activate / deactivate any user; list parents.
- Manage subjects (create, update, toggle status) and levels (create, update, delete).
- Manage teachers and students, and assign / unassign students to teachers.
- Manage worksheets (upload, update, delete, download).
- Create, update and cancel assignments; grade and re-grade submissions.
- Mark and edit attendance; view today's attendance, history and monthly summary.
- Generate fees, update fees, mark fees paid / overdue, view all fee records and reports.
- View the Super Admin dashboard, full-system report and all other reports.

### 🏫 Center Admin
- View their own center and its statistics.
- Activate / deactivate users; list parents.
- Create, update, delete and list teachers; assign / unassign students to teachers.
- Create, update, delete and list students; view student assignments, attendance, fees, progress and reports.
- View subjects and levels.
- Upload, update, delete and download worksheets.
- View and cancel assignments; view submissions and pending submissions.
- Mark and edit attendance; view today's attendance, history and monthly summary.
- Generate monthly fees, update fees, mark fees paid / overdue, and view fee records and reports (limited to their center).
- View dashboard KPIs, center performance, detailed center, teacher performance, fee collection, attendance and level progression reports.

### 👩‍🏫 Teacher
- View the teacher dashboard and their assigned students.
- List and update students; view student details, assignments, attendance, progress and reports.
- View subjects and levels.
- Upload, update and download worksheets.
- Bulk-assign worksheets, update and cancel assignments.
- View all / pending submissions, download submitted files, grade and re-grade work.
- Mark and edit attendance; view today's attendance and attendance history.
- View their dashboard KPIs (students, pending grades, average score).

### 🎓 Student
- Log in and manage their own profile and password.
- View the student dashboard and "my assignments".
- View assignments and download worksheets.
- Submit completed work (file upload).
- View their own submissions and download them.
- View their progress and reports.
- View their dashboard KPIs (pending assignments, current level, last score).

### 👨‍👩‍👧 Parent
- Register, log in and manage their own profile and password.
- View the parent dashboard covering all their children.
- View each child's details, reports, progress, assignments, submissions, attendance and fees.
- View the teacher assigned to their child.
- View their own children's fee records (cannot edit fees).
- View their dashboard KPIs (number of children, pending fees, average progress).

## 🛠️ Technology Stack

- **Framework**: Laravel 11.x
- **Security**: JWT Authentication (JSON Web Token)
- **Database**: MySQL 8.x
- **Storage**: Local/Cloud Disk for worksheets and submissions

## 🔧 Installation & Setup

1. **Clone the Repo**:

    ```bash
    git clone [repository-url]
    cd After_school_program_system
    ```

2. **Install Dependencies**:

    ```bash
    composer install
    npm install && npm run build
    ```

3. **Environment Setup**:

    ```bash
    cp .env.example .env
    # Update DB_DATABASE, DB_USERNAME, DB_PASSWORD
    # Generate Application Key
    php artisan key:generate
    # Generate JWT Secret
    php artisan jwt:secret
    ```

4. **Database Migration**:

    ```bash
    php artisan migrate --seed
    ```

5. **Run Server**:
    ```bash
    php artisan serve
    ```

---

## 📖 API Documentation

### Base URL

`http://localhost:8000/api`

### 🔒 Authorization

Most endpoints require a **Bearer Token**. Include it in your headers:
`Authorization: Bearer {your_token}`

---

Role abbreviations: **SA** = Super Admin, **CA** = Center Admin, **T** = Teacher, **S** = Student, **P** = Parent.

### 1. Authentication & Users

| Endpoint                    | Method | Description                                  | Roles  |
| :-------------------------- | :----- | :------------------------------------------- | :----- |
| `/register`                 | POST   | Register (super_admin, center_admin, parent) | Public |
| `/login`                    | POST   | Login and receive JWT token                  | Public |
| `/logout`                   | POST   | Invalidate current token                     | All    |
| `/profile`                  | GET    | View current user profile                    | All    |
| `/update-profile`           | POST   | Update name, phone, address, image           | All    |
| `/change-password`          | POST   | Update account password                      | All    |
| `/super-admin/dashboard`    | GET    | Super Admin dashboard                        | SA     |
| `/center-admins`            | GET    | List center admins                           | SA     |
| `/center-admins/{id}`       | DELETE | Delete a center admin                        | SA     |
| `/parents`                  | GET    | List parents                                 | SA, CA |
| `/users/{id}/toggle-status` | PATCH  | Activate / deactivate a user                 | SA, CA |

### 2. Centers

| Endpoint             | Method         | Description            | Roles  |
| :------------------- | :------------- | :--------------------- | :----- |
| `/center`            | GET \| POST    | List / create centers  | SA     |
| `/center/{id}`       | PUT \| DELETE  | Update / delete center | SA     |
| `/center/{id}`       | GET            | View center            | SA, CA |
| `/center/stats/{id}` | GET            | Center statistics      | SA, CA |

### 3. Teachers

| Endpoint                     | Method        | Description                    | Roles        |
| :--------------------------- | :------------ | :----------------------------- | :----------- |
| `/teacher/dashboard`         | GET           | Teacher dashboard              | SA, CA, T    |
| `/teacher`                   | GET \| POST   | List / create teachers         | SA, CA       |
| `/teacher/{id}`              | PUT \| DELETE | Update / delete teacher        | SA, CA       |
| `/teacher/{id}`              | GET           | View teacher                   | SA, CA, T, P |
| `/teacher/{id}/students`     | GET           | Students assigned to a teacher | SA, CA, T, P |
| `/teacher/assign-students`   | POST          | Assign students to a teacher   | SA, CA       |
| `/teacher/unassign-students` | POST          | Unassign students              | SA, CA       |

### 4. Students

| Endpoint                    | Method | Description                          | Roles        |
| :-------------------------- | :----- | :----------------------------------- | :----------- |
| `/student`                  | POST   | Create student (auto enrollment no.) | SA, CA       |
| `/student/{id}`             | DELETE | Delete student                       | SA, CA       |
| `/student`                  | GET    | List students                        | SA, CA, T    |
| `/student/{id}`             | PUT    | Update student                       | SA, CA, T    |
| `/student/{id}`             | GET    | View student                         | SA, CA, T, P |
| `/student/{id}/assignments` | GET    | Student's assignments                | SA, CA, T, P |
| `/student/{id}/attendance`  | GET    | Student's attendance                 | SA, CA, T, P |
| `/student/{id}/fees`        | GET    | Student's fees                       | SA, CA, P    |
| `/student/{id}/progress`    | GET    | Level progress and metrics           | All          |
| `/student/{id}/reports`     | GET    | Full academic / attendance report    | All          |
| `/student/dashboard`        | GET    | Student dashboard                    | S            |
| `/student/my-assignments`   | GET    | Logged-in student's assignments      | S            |

### 5. Parent Portal

| Endpoint                       | Method | Description            | Roles |
| :----------------------------- | :----- | :--------------------- | :---- |
| `/parent/dashboard`            | GET    | Parent dashboard       | P     |
| `/parent/children-reports`     | GET    | Children's reports     | P     |
| `/parent/children-attendance`  | GET    | Children's attendance  | P     |
| `/parent/children-assignments` | GET    | Children's assignments | P     |
| `/parent/children-fees`        | GET    | Children's fees        | P     |

### 6. Subjects & Levels

| Endpoint                      | Method        | Description           | Roles     |
| :---------------------------- | :------------ | :-------------------- | :-------- |
| `/subject`                    | GET           | List active subjects  | All       |
| `/subject/all`                | GET           | List all subjects     | SA, CA, T |
| `/subject/{id}`               | GET           | View subject          | SA, CA, T |
| `/subject`                    | POST          | Create subject        | SA        |
| `/subject/{id}`               | PUT           | Update subject        | SA        |
| `/subject/{id}/toggle-status` | PATCH         | Activate / deactivate | SA        |
| `/level`                      | GET           | List levels           | All       |
| `/level`                      | POST          | Create level          | SA        |
| `/level/{id}`                 | PUT \| DELETE | Update / delete level | SA        |

### 7. Worksheets

| Endpoint                   | Method      | Description                                  | Roles     |
| :------------------------- | :---------- | :------------------------------------------- | :-------- |
| `/worksheet`               | GET \| POST | List (filter by subject/level) / upload PDF  | SA, CA, T |
| `/worksheet/{id}`          | PUT         | Update worksheet                             | SA, CA, T |
| `/worksheet/{id}`          | DELETE      | Delete worksheet                             | SA, CA    |
| `/worksheet/{id}`          | GET         | View worksheet                               | All       |
| `/worksheet/{id}/download` | GET         | Download worksheet PDF                       | All       |

### 8. Assignments

| Endpoint           | Method | Description                      | Roles        |
| :----------------- | :----- | :------------------------------- | :----------- |
| `/assignment`      | GET    | List assignments                 | SA, CA, T, S |
| `/assignment/{id}` | GET    | View assignment                  | SA, CA, T, S |
| `/assignment`      | POST   | Bulk assign worksheet            | SA, T        |
| `/assignment/{id}` | PUT    | Update due date / notes / status | SA, T        |
| `/assignment/{id}` | DELETE | Cancel assignment                | SA, CA, T    |

### 9. Submissions

| Endpoint                                | Method | Description                     | Roles        |
| :-------------------------------------- | :----- | :------------------------------ | :----------- |
| `/submission`                           | POST   | Submit work (file upload)       | S, SA, CA, T |
| `/submission`                           | GET    | List all submissions            | SA, CA, T    |
| `/submission/pending`                   | GET    | Ungraded submissions            | SA, CA, T    |
| `/submission/{id}/grade`                | PATCH  | Grade (score, errors, feedback) | SA, T        |
| `/submission/{id}/update-grade`         | PUT    | Re-grade a submission           | SA, T        |
| `/submission/assignment/{assignmentId}` | GET    | Submission for an assignment    | All          |
| `/submission/{id}`                      | GET    | View submission                 | All          |
| `/submission/{id}/download`             | GET    | Download submitted file         | All          |

### 10. Attendance

| Endpoint              | Method | Description               | Roles        |
| :-------------------- | :----- | :------------------------ | :----------- |
| `/attendance/bulk`    | POST   | Bulk mark attendance      | SA, CA, T    |
| `/attendance/{id}`    | PUT    | Edit attendance record    | SA, CA, T    |
| `/attendance/today`   | GET    | Today's attendance        | SA, CA, T    |
| `/attendance`         | GET    | Attendance history        | SA, CA, T, P |
| `/attendance/summary` | GET    | Monthly summary by status | SA, CA       |

### 11. Fees

| Endpoint                   | Method | Description                                  | Roles     |
| :------------------------- | :----- | :------------------------------------------- | :-------- |
| `/fees`                    | GET    | List fees (filter student_id, month, status) | SA, CA, P |
| `/fees/{id}`               | GET    | View fee record                              | SA, CA, P |
| `/fees/center/{center_id}` | GET    | All fee records of a center                  | SA, CA    |
| `/fees/generate`           | POST   | Bulk generate monthly fees                   | SA, CA    |
| `/fees/{id}`               | PUT    | Update fee record                            | SA, CA    |
| `/fees/{id}/pay`           | PUT    | Mark as paid (method, txn ID, date)          | SA, CA    |
| `/fees/mark-overdue`       | POST   | Mark past-due unpaid fees as overdue         | SA, CA    |
| `/fees/unpaid-overdue`     | GET    | List unpaid / overdue fees                   | SA, CA    |
| `/fees/report`             | GET    | Fee collection summary                       | SA, CA    |

### 12. Reports & Analytics

| Endpoint                         | Method | Description                          | Roles  |
| :------------------------------- | :----- | :----------------------------------- | :----- |
| `/dashboard/kpis`                | GET    | Role-based dashboard KPIs            | All    |
| `/reports/center-performance`    | GET    | Center performance                   | SA, CA |
| `/reports/center-detailed/{id}`  | GET    | 360° center report                   | SA, CA |
| `/reports/teacher-performance`   | GET    | Teacher performance                  | SA, CA |
| `/reports/student-detailed/{id}` | GET    | Detailed student report              | SA, CA |
| `/reports/fee-collection`        | GET    | Monthly revenue trend                | SA, CA |
| `/reports/attendance`            | GET    | Attendance distribution              | SA, CA |
| `/reports/level-progression`     | GET    | Students and average score per level | SA, CA |
| `/reports/full-system`           | GET    | Full system report                   | SA     |

---

## 📁 System Architecture

- **Controllers**: Located in `app/Http/Controllers/Api`
- **Models**: Located in `app/Models`
- **Database**: Migrations in `database/migrations`
- **Traits**: Shared logic for responses in `app/Traits/ApiResponse.php`
