# Co-op Support Application (CSA)

A Java desktop application designed to help manage the university co-op process in one place. The **Co-op Support Application (CSA)** provides role-based portals for students, co-op coordinators, and workplace supervisors to handle applications, track decisions, submit work-term documents, and review missing submissions.

Built as a **CPS 406 course project** using Java Swing for the interface and SQLite for local data storage.

## Features

### Student portal
- Apply for co-op by creating a student account with a name, nine-digit student ID, email, and password.
- Sign in to check application status and read notes from the co-op coordinator.
- View provisional and final application decisions.
- Upload or replace a PDF work-term report after receiving **Final Accepted** status.
- Record a work term and deadline when submitting a report.

### Coordinator dashboard
- View student applications in a table with their current status, notes, and submission date.
- See total and pending application counts.
- Provisionally accept or reject applications, then issue a final decision for provisionally accepted students.
- Add notes when updating an application decision.
- Review whether final-accepted students have submitted their work-term reports and supervisor evaluations.
- Display a reminder summary for missing submissions. **Reminder emails are not actually sent**; this is a simulated in-app confirmation.

### Supervisor portal
- Create a supervisor account and sign in.
- Submit an evaluation for a final-accepted student using an online form with a 1–5 rating and comments.
- Alternatively, upload a completed evaluation as a PDF.
- Associate each evaluation with a student ID and work term.

## Tech Stack

| Technology | Purpose |
| --- | --- |
| Java (JDK 21+) | Application logic |
| Java Swing / AWT | Desktop graphical user interface |
| SQLite | Local relational database |
| JDBC (Xerial SQLite JDBC driver) | Database connectivity |
| Bash / Windows Batch | Build and launch scripts |

## Getting Started

### Prerequisites

1. Install **JDK 21 or newer** and ensure `java` and `javac` are available from your terminal.
2. Download the **SQLite JDBC** `.jar` file from the [Xerial SQLite JDBC releases](https://github.com/xerial/sqlite-jdbc/releases).
3. In the project root, create a `lib` folder if it does not already exist. Place the downloaded driver inside and rename it to **`sqlite-jdbc.jar`**.

Your project should include the following file before running:

```text
lib/
└── sqlite-jdbc.jar
```

> The JDBC driver is not included in the source archive and is excluded from Git using `.gitignore`.

### Run on Windows

Open Command Prompt or PowerShell in the project folder and run:

```bat
run.bat
```

### Run on macOS or Linux

Open a terminal in the project folder and run:

```bash
chmod +x run.sh
./run.sh
```

The scripts compile the Java source files into `out/` and launch `csa.App`.

### Demo coordinator login

A coordinator account is added automatically the first time the database is initialized:

```text
Email:    coordinator@tmu.ca
Password: admin123
```

This login is provided **for local demonstration only**. You can create student accounts from **Apply for Co-op** and supervisor accounts from **Create Supervisor Account** on the sign-in screen.

## How It Works

1. **Apply:** A student creates an account and submits an application. The initial status is `Pending Provisional Review`.
2. **Review:** The coordinator reviews the application and chooses a provisional decision. Only a `Provisional Accepted` application can proceed to a final decision.
3. **Track:** The student signs in to view the updated status and any coordinator notes.
4. **Submit:** Once `Final Accepted`, the student can upload a PDF work-term report and a supervisor can submit an evaluation.
5. **Monitor:** The coordinator checks the **Missing Submissions** tab to identify outstanding reports or evaluations.

## Project Structure

```text
CPS406proj-main/
├── src/
│   └── csa/
│       ├── App.java                 # Main window and screen navigation
│       ├── db/
│       │   └── Database.java        # SQLite setup and queries
│       ├── model/
│       │   └── User.java            # Signed-in user data model
│       └── ui/
│           ├── LoginScreen.java
│           ├── ApplyScreen.java
│           ├── StudentScreen.java
│           ├── CoordinatorScreen.java
│           ├── SupervisorScreen.java
│           └── Helpers.java
├── lib/
│   └── sqlite-jdbc.jar              # Download separately (not tracked)
├── run.bat                          # Windows launcher
├── run.sh                           # macOS / Linux launcher
├── .gitignore
└── README.md
```

At runtime, the application also creates:

- `csa.db`, the local SQLite database containing user accounts, applications, reports, and evaluations.
- `uploads/`, which stores copies of submitted PDF reports and PDF evaluations.
- `out/`, which contains compiled Java classes.

These generated files and directories are ignored by Git.

## Current Limitations

This is a **course prototype**, not a production co-op management system.

- Data is stored locally rather than on a shared server.
- Passwords are currently stored as plain text, and the demo coordinator password is hard-coded. Production use would require secure password hashing and stronger account controls.
- The reminder feature shows an in-app message but does not send emails or notifications.
- PDF uploads are stored locally, and the application does not include cloud storage or an administrative file viewer.
- The interface uses a basic desktop layout rather than a web or mobile client.

## Project Context

Developed as a team project for **CPS 406 (Software Engineering)** at Toronto Metropolitan University.
