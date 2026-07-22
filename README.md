# TaskFlow — Task Management System (MERN)

A task management app converted from a full-stack Employee Management System. Admins assign and manage tasks; employees track and update progress on tasks assigned to them.

## What changed from the original EMS

- **Removed:** Attendance (clock in/out), Leave applications, Payslips/payroll fields, and their related pages, models, controllers, and background jobs.
- **Added:** A `Task` model (title, description, assignee, priority, status, due date, category) with full CRUD, a `/tasks` page with filtering and status updates, task-focused dashboards for both roles, and background email notifications for new task assignments + a daily overdue-task reminder.
- **Kept as-is:** Authentication (Admin/Employee roles), Employee directory (minus salary fields), profile & settings pages, and the overall UI shell (sidebar, layout, login flow).

## Roles

- **Admin** — creates tasks, assigns them to employees, edits/deletes tasks, filters by status/priority/assignee, sees team-wide stats.
- **Employee** — sees only tasks assigned to them, updates status (To Do → In Progress → Completed / Blocked), sees personal stats and upcoming due dates.

## Running it

### Server
```bash
cd server
npm install
# fill in server/.env (Mongo URI, JWT secret, admin email, SMTP creds, Inngest keys)
npm run seed     # creates the first admin user
npm run server   # starts on http://localhost:4000
```

### Client
```bash
cd client
npm install
# set VITE_BASE_URL in client/.env if your server isn't on localhost:4000
npm run dev      # starts on http://localhost:5173
```

Log in at `/login`, choose the Admin or Employee portal, and use the admin account created by `npm run seed` to get started (default password `admin123` — change it after first login).

## Key API routes

| Method | Route | Who | Purpose |
|---|---|---|---|
| POST | `/api/tasks` | Admin | Create & assign a task |
| GET | `/api/tasks` | Admin/Employee | List tasks (admin: all + filters; employee: own only) |
| PUT | `/api/tasks/:id` | Admin | Edit task details |
| PATCH | `/api/tasks/:id/status` | Admin/Employee | Update task status |
| DELETE | `/api/tasks/:id` | Admin | Delete a task |
| GET | `/api/dashboard` | Admin/Employee | Task-based dashboard stats |
