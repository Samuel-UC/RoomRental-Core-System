StayManager-MVC: Room Rental Management System
📌 Overview
StayManager-MVC is a robust web application designed to streamline the administration of room rentals. Built on the ASP.NET Core MVC framework, the system automates the lifecycle of a reservation—from client data entry and automatic cost calculation based on room types to persistent storage and record management (CRUD).

The project focuses on high data integrity, utilizing Entity Framework Core for ORM (Object-Relational Mapping) and a modular architecture that separates business logic, data models, and user views.

🚀 Key Features
Dynamic Cost Calculation: Automatically computes the total stay price based on room category (Standard, Suite, Deluxe) and duration.

Full CRUD Operations: Comprehensive interface to Create, Read, Update, and Delete rental records.

Data Validation: Server-side and client-side validation for required fields, dates, and numeric inputs.

Responsive Dashboard: A clean, modern table-based view for monitoring all active and past rentals.

Database Persistence: Full integration with SQL Server to ensure data persistence and security.

🛠️ Technical Stack
Backend: C# with ASP.NET Core 8.0 (MVC Pattern).

ORM: Entity Framework Core (Code First / DB First approach).

Database: Microsoft SQL Server.

Frontend: Razor Pages, HTML5, CSS3, and Bootstrap for responsive design.

🧠 Database Schema & Logic
The system is centered around a RoomRental entity. Key attributes include:

Guest Name: String (Required).

Room Type: Categorized selection (Standard: $X/day, Suite: $Y/day, etc.).

Stay Duration: Integer (Days).

Total Cost: Calculated field (Rate * Days).

Data Model Snippet (C#)
C#
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
💻 Implementation Details
Business Logic: Automatic Pricing
The application implements a specialized logic within the Controller to handle pricing tiers. This ensures that the user only needs to input the room type and days, while the system handles the financial accuracy.

C#
// Logic snippet inside the Controller
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
View Components (Razor)
The UI uses strongly-typed views to bind data models to HTML forms, ensuring that validation messages are displayed in real-time if a field is omitted.

📂 Project Structure
Plaintext
StayManager-MVC/
├── Controllers/
│   └── RentalController.cs    # Handles CRUD logic and pricing calculations
├── Models/
│   └── RoomRental.cs          # Data structure and validation rules
├── Data/
│   └── ApplicationDbContext.cs # Database context and EF configuration
├── Views/
│   ├── Rental/
│   │   ├── Index.cshtml       # Main records dashboard
│   │   ├── Create.cshtml      # New registration form
│   │   └── Edit.cshtml        # Record modification interface
│   └── Shared/
├── wwwroot/                   # Static files (CSS, JS, Images)
└── Program.cs                 # Application startup and Dependency Injection
🔧 Installation & Setup
Clone the repository:

Bash
git clone https://github.com/your-username/staymanager-mvc.git
Database Configuration: Update the ConnectionStrings in appsettings.json to point to your SQL Server instance.

Apply Migrations:

Bash
dotnet ef database update
Run the application:

Bash
dotnet run
🎓 Learning Outcomes
This project demonstrates proficiency in:

MVC Pattern: Separation of concerns for scalable web development.

Entity Framework Core: Managing relational data through C# objects.

Form Validation: Implementing robust error handling for user inputs.

Backend Logic: Handling conditional calculations and data processing.

📄 License
This project is licensed under the MIT License.

Note: This documentation was generated based on the technical implementation of the Room Rental Management project.
