# StayManager-MVC: Sistema de Gestión de Alquiler de Habitaciones

[![Framework: .NET Core 8.0](https://img.shields.io/badge/Framework-.NET%20Core%208.0-blue.svg)](https://dotnet.microsoft.com/es-es/download)
[![Arquitectura: MVC](https://img.shields.io/badge/Arquitectura-MVC-green.svg)](https://dotnet.microsoft.com/es-es/apps/aspnet/mvc)
[![Base de Datos: SQL Server](https://img.shields.io/badge/Base_de_Datos-SQL%20Server-red.svg)](https://www.microsoft.com/es-es/sql-server/)
[![ORM: Entity Framework Core](https://img.shields.io/badge/ORM-EF%20Core-orange.svg)](https://learn.microsoft.com/es-es/ef/core/)
[![Licencia: MIT](https://img.shields.io/badge/Licencia-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📌 Descripción General
**StayManager-MVC** es una aplicación web robusta diseñada para optimizar la administración de alquileres de habitaciones. Desarrollado bajo el framework **ASP.NET Core MVC**, el sistema automatiza el ciclo de vida completo de una reserva: desde el ingreso de datos del cliente y el cálculo automático de costos según el tipo de habitación, hasta el almacenamiento persistente y la gestión integral de registros (CRUD).

El proyecto destaca por su alta integridad de datos y sigue una arquitectura modular, asegurando una separación clara entre la lógica de negocio, los modelos de datos y las interfaces de usuario.

---

## 🚀 Características Clave
* **Cálculo Dinámico de Costos:** Computación en tiempo real de los precios de estancia basados en la categoría de habitación (Estándar, Suite, Deluxe) y la duración.
* **Ciclo CRUD Completo:** Interfaz intuitiva para Crear, Leer, Actualizar y Eliminar registros de alquiler sin complicaciones.
* **Validación Inteligente de Datos:** Validación multicapa (Lado Cliente y Servidor) para tipos de datos, campos obligatorios y rangos lógicos de fechas.
* **Dashboard Responsivo:** Vista moderna basada en tablas, compatible con dispositivos móviles, para el monitoreo de alquileres actuales e históricos.
* **Persistencia de Clase Empresarial:** Integración total con **SQL Server** a través de **Entity Framework Core** para una gestión segura de la información.

---

## 🛠️ Stack Tecnológico
* **Backend:** C# con ASP.NET Core 8.0 (Patrón Arquitectónico MVC).
* **ORM:** Entity Framework Core (Compatibilidad con Code First y DB First).
* **Base de Datos:** Microsoft SQL Server.
* **Frontend:** Razor Pages, HTML5, CSS3 y Bootstrap para diseños responsivos.

---

## 🧠 Esquema y Lógica de Base de Datos
El sistema se centraliza en la entidad `RoomRental`, diseñada para una normalización de datos óptima:

| Atributo | Tipo de Dato | Restricción |
| :--- | :--- | :--- |
| **Nombre Huésped** | String | Requerido |
| **Tipo Habitación** | String | Selección por Categoría |
| **Duración** | Entero | Rango (1-365 días) |
| **Costo Total** | Decimal | Campo Calculado |

### Implementación del Modelo de Datos
```csharp
public class RoomRental
{
    [Key]
    public int Id { get; set; }

    [Required(ErrorMessage = "El nombre del huésped es obligatorio")]
    [Display(Name = "Nombre del Huésped")]
    public string GuestName { get; set; }

    [Required]
    [Display(Name = "Tipo de Habitación")]
    public string RoomType { get; set; }

    [Range(1, 365, ErrorMessage = "La estancia debe ser entre 1 y 365 días")]
    public int Days { get; set; }

    [DataType(DataType.Currency)]
    public decimal TotalAmount { get; set; }
}
💻 Aspectos Destacados de Implementación
Lógica de Negocio: Motor de Precios Automatizado
Una lógica centralizada en el Controlador gestiona los niveles de precios, asegurando precisión y reduciendo errores de entrada manual.

C#
// Lógica de negocio para el cálculo de costos
public decimal CalculateTotal(string tipo, int dias)
{
    decimal tarifa = tipo switch
    {
        "Standard" => 50.00m,
        "Suite" => 120.00m,
        "Deluxe" => 200.00m,
        _ => 0.00m
    };
    return tarifa * dias;
}
Diseño de Experiencia de Usuario (Razor & Bootstrap)
La interfaz utiliza vistas fuertemente tipadas para vincular los modelos directamente con el HTML, proporcionando retroalimentación instantánea mediante resúmenes de validación y diseños dinámicos.

📂 Estructura del Proyecto
Plaintext
StayManager-MVC/
├── Controllers/
│   └── RentalController.cs    # Orquestador de CRUD y Lógica de Negocio
├── Models/
│   └── RoomRental.cs          # Definiciones de entidad y reglas de validación
├── Data/
│   └── ApplicationDbContext.cs # Contexto de EF Core y configuración de BD
├── Views/
│   ├── Rental/
│   │   ├── Index.cshtml       # Panel de Control de Registros
│   │   ├── Create.cshtml      # Interfaz de Nuevo Registro
│   │   └── Edit.cshtml        # Módulo de Actualización de Datos
│   └── Shared/                # Diseños Globales y Parciales
├── wwwroot/                   # Recursos Estáticos (CSS, JS, Libs)
└── Program.cs                 # Inicio de App e Inyección de Dependencias
🔧 Instalación y Configuración
Clonar el repositorio:

Bash
git clone [https://github.com/tu-usuario/staymanager-mvc.git](https://github.com/tu-usuario/staymanager-mvc.git)
Configuración de Base de Datos: Modifica la cadena ConnectionStrings en appsettings.json para que coincida con tu instancia local de SQL Server.

Aplicar Migraciones de Base de Datos:

Bash
dotnet ef database update
Iniciar Aplicación:

Bash
dotnet run
🎓 Resultados del Aprendizaje
Este proyecto demuestra competencia en:

Arquitectura Profesional MVC: Separación de responsabilidades escalable.

Maestría en ORM: Gestión de datos relacionales sin interrupciones con EF Core.

Desarrollo Backend: Implementación de lógica condicional y cálculos financieros.

UI/UX Segura: Diseño de formularios con validación robusta y manejo de errores.

📄 Licencia
Este proyecto está bajo la Licencia MIT.
