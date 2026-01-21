# StayManager-MVC: Room Rental Management System

[![Framework: .NET Core 8.0](https://img.shields.io/badge/Framework-.NET%20Core%208.0-blue.svg)](https://dotnet.microsoft.com/en-us/download)
[![Architecture: MVC](https://img.shields.io/badge/Architecture-MVC-green.svg)](https://dotnet.microsoft.com/en-us/apps/aspnet/mvc)
[![Database: SQL Server](https://img.shields.io/badge/Database-SQL%20Server-red.svg)](https://www.microsoft.com/en-us/sql-server/)
[![ORM: Entity Framework Core](https://img.shields.io/badge/ORM-EF%20Core-orange.svg)](https://learn.microsoft.com/en-us/ef/core/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Overview
**StayManager-MVC** is a robust web application designed to streamline the administration of room rentals. Built on the **ASP.NET Core MVC** framework, the system automates the complete lifecycle of a reservation—from client data entry and automatic cost calculation based on room types to persistent storage and full record management (CRUD).

The project emphasizes high data integrity and follows a modular architecture, ensuring a clean separation between business logic, data models, and user interfaces.

---

## 🚀 Key Features
* **Dynamic Cost Calculation:** Real-time computation of stay prices based on room category (Standard, Suite, Deluxe) and duration.
* **Full CRUD Lifecycle:** Comprehensive interface to Create, Read, Update, and Delete rental records with ease.
* **Smart Data Validation:** Multi-layer validation (Client & Server-side) for data types, required fields, and logical date ranges.
* **Responsive Dashboard:** A modern, mobile-friendly table-based view for monitoring active and past rentals.
* **Enterprise-Ready Persistence:** Full integration with **SQL Server** through **Entity Framework Core** for secure data management.

---

## 🛠️ Technical Stack
* **Backend:** C# with ASP.NET Core 8.0 (MVC Architectural Pattern).
* **ORM:** Entity Framework Core (Code First & DB First compatibility).
* **Database:** Microsoft SQL Server.
* **Frontend:** Razor Pages, HTML5, CSS3, and Bootstrap for responsive layouts.

---

## 🧠 Database Schema & Logic
The system is centered around the `RoomRental` entity, designed for optimal data normalization:

| Attribute | Data Type | Constraint |
| :--- | :--- | :--- |
| **Guest Name** | String | Required |
| **Room Type** | String | Category Selection |
| **Stay Duration** | Integer | Range (1-365) |
| **Total Cost** | Decimal | Calculated Field |

### Data Model Implementation
```csharp
public class RoomRental
{
    [Key]
    public int Id { get; set; }

    [Required(ErrorMessage = "Guest name is mandatory")]
    [Display(Name = "Guest Name")]
    public string GuestName { get; set; }

    [Required]
    [Display(Name = "Room Type")]
    public string RoomType { get; set; }

    [Range(1, 365, ErrorMessage = "Stay must be between 1 and 365 days")]
    public int Days { get; set; }

    [DataType(DataType.Currency)]
    public decimal TotalAmount { get; set; }
}
💻 Implementation Highlights
Business Logic: Automated Pricing Engine
A centralized logic within the Controller manages pricing tiers, ensuring accuracy and reducing manual input errors.

C#
// Business logic for cost calculation
public decimal CalculateTotal(string type, int days)
{
    decimal rate = type switch
    {
        "Standard" => 50.00m,
        "Suite" => 120.00m,
        "Deluxe" => 200.00m,
        _ => 0.00m
    };
    return rate * days;
}
UX Design (Razor & Bootstrap)
The UI utilizes strongly-typed views to bind models directly to the HTML, providing instant feedback via validation summaries and dynamic layouts.

📂 Project Structure
Plaintext
StayManager-MVC/
├── Controllers/
│   └── RentalController.cs    # Orchestrates CRUD & Business Logic
├── Models/
│   └── RoomRental.cs          # Entity definitions & validation rules
├── Data/
│   └── ApplicationDbContext.cs # EF Core Context & DB Configuration
├── Views/
│   ├── Rental/
│   │   ├── Index.cshtml       # Main Records Dashboard
│   │   ├── Create.cshtml      # New Registration Interface
│   │   └── Edit.cshtml        # Record Update Module
│   └── Shared/                # Layouts & Partials
├── wwwroot/                   # Static Assets (CSS, JS, Libs)
└── Program.cs                 # App Startup & Dependency Injection
🔧 Installation & Setup
Clone the repository:

Bash
git clone [https://github.com/your-username/staymanager-mvc.git](https://github.com/your-username/staymanager-mvc.git)
Database Configuration: Modify the ConnectionStrings in appsettings.json to match your local SQL Server instance.

Apply Database Migrations:

Bash
dotnet ef database update
Launch Application:

Bash
dotnet run
🎓 Learning Outcomes
This project serves as a showcase of proficiency in:

Professional MVC Architecture: Scalable separation of concerns.

ORM Mastery: Managing relational data seamlessly with EF Core.

Backend Development: Implementing conditional logic and financial calculations.

Secure UI/UX: Designing forms with robust validation and error handling.

📄 License
This project is licensed under the MIT License.
