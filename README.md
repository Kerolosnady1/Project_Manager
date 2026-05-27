```markdown
# Project-To-Project (P2P) Launcher & Sign Language Dictionary

An Event-Driven Windows Forms desktop application developed in C# targeting **.NET 10**. This project serves a dual-purpose system: acting as a centralized application hub/launcher for external executables, and housing an embedded functional Sign Language Dictionary that dynamically translates text inputs into animated sign language GIFs.

---

## 🚀 Key Features

* **Application Launcher Hub:** Register custom external executable (`.exe`) files into a persistent database via an integrated `OpenFileDialog` interface and execute them straight from the dashboard.
* **Sign Language Dictionary:** An embedded dictionary module that takes text input queries, maps them to known words, and asynchronously renders visual sign representations via animated GIFs into a `PictureBox`.
* **Self-Healing Database Initialization:** Powered by **SQL Server LocalDB**, the system automatically generates, configures, and attaches its physical database files (`EventProjectDB.mdf`) inside the user's `MyDocuments` folder on cold start—requiring zero external server setup or script runs.
* **Pre-Flight Diagnostic Core:** Built-in validation suite engine executable directly via a runtime CLI flag to test database Create and Read (CR) capabilities on new host environments.

---

## 🛠️ Architecture & Technology Stack

* **Framework:** .NET 10 (Windows Forms)
* **Language:** C# 14
* **Database Engine:** Microsoft SQL Server LocalDB (`MSSQLLocalDB`)
* **Data Access Layer:** Low-overhead raw ADO.NET using the modern `Microsoft.Data.SqlClient` data provider with parameterized query bindings.

---

## 📊 Relational Database Design

The local instance initializes two tables configured automatically by `DatabaseHelper.cs`:

### 1. `Projects` Table
Maintains data regarding external executable bindings registered into the central launchpad dashboard.

| Column Name | Data Type | Key / Constraints | Description |
| :--- | :--- | :--- | :--- |
| **Id** | `INT` | Primary Key, Identity | Unique system identifier for the executable record. |
| **Name** | `NVARCHAR(100)`| Not Null | Friendly display label for the application grid. |
| **ExePath** | `NVARCHAR(MAX)`| Not Null | Absolute local physical filepath to the targeted executable binary. |

### 2. `Signs` Table
Acts as the text-to-graphics translation repository mapping text keywords to local animation visual components.

| Column Name | Data Type | Key / Constraints | Description |
| :--- | :--- | :--- | :--- |
| **Id** | `INT` | Primary Key, Identity | Unique reference key for the dictionary index entity. |
| **Answer** | `NVARCHAR(100)`| Not Null, Indexed | The core target keyword phrase entry mapped to user search input. |
| **GifPath** | `NVARCHAR(MAX)`| Not Null | The relative portable file directory string pointing to the corresponding sign language GIF. |

---

## 📂 Structural Directory & File Breakdown

* **`Program.cs`** The main entrance boundary of the application. Handles programmatic application bootstrap rules, calls the initial data storage validations, and filters runtime arguments. If `--test` is caught via the application argument stack, it routes processing straight to the console tester and bypasses the graphical environment.
* **`DatabaseHelper.cs`** Houses database initialization, master target routing configuration bindings, and exposes core dataset transaction pipelines such as `GetAllWords()` and targeted lookups via `GetGif()`.
* **`DatabaseTester.cs`** An isolated, decoupled automated self-diagnostic tool. Generates mock entries, performs transaction verification, and prints database stability indicators to confirm deployment health.
* **`Form1.cs` (Launcher View)** The graphical dashboard interface providing dynamic list rendering of external executable paths, native file dialog triggers, and structural navigation links to inner application layers.
* **`Form5.cs` (Dictionary View)** The operational dictionary workspace binding user lookups, rendering indexed elements, dynamically loading picture components into a custom view window, and managing storage index deletions.

---

## 💻 Getting Started & Execution

### Prerequisites
* Windows OS (Required for WinForms execution layer)
* [.NET 10 SDK](https://dotnet.microsoft.com/download) installed
* [SQL Server Express LocalDB](https://learn.microsoft.com/en-us/sql/database-engine/configure-windows/sql-server-express-localdb) instance running locally on the machine

### Installation & Run Steps
1. Clone this repository locally to your directory:
   ```bash
   git clone [https://github.com/YourUsername/P2P-Launcher-SignLanguage.git](https://github.com/YourUsername/P2P-Launcher-SignLanguage.git)
   cd P2P-Launcher-SignLanguage
Restore internal packages and dependencies:

Bash
dotnet restore
Run the primary desktop app directly via the dotnet engine pipeline:

Bash
dotnet run
Executing Pre-Flight System Self-Tests
To run the decoupled database engine checks directly inside your automated continuous environment workflow or terminal shell without compiling full desktop views:

Bash
dotnet run -- --test
👥 Development Team
This project was developed for the Event-Driven Programming Course under the academic guidance of our instruction team.

Student Contributors
Philopateer Waheed — ID: 42410086

Shimaa Salah — ID: 42410338

Noran Ahmed — ID: 42410001

Yousef Mohamed — ID: 42410515

Kerolos Nady — ID: 42410542

Shrouk Khalaf — ID: 42410575

Instruction Team
Dr. Ahmed Seif — Course Professor

Eng. Ahmed Karem — Teaching Assistant

Eng. Ahmed Hamdy — Teaching Assistant

Academic Year: 2025 / 2026
