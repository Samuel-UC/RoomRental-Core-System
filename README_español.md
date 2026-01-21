StayManager-MVC: Sistema de Gestión de Alquiler de Habitaciones
📌 Descripción General
StayManager-MVC es una aplicación web robusta diseñada para optimizar la administración de alquileres de habitaciones. Desarrollado bajo el framework ASP.NET Core MVC, el sistema automatiza el ciclo de vida de una reserva: desde el ingreso de datos del cliente y el cálculo automático de costos según el tipo de habitación, hasta el almacenamiento persistente y la gestión de registros (CRUD).

El proyecto se centra en la integridad de los datos, utilizando Entity Framework Core como ORM (Object-Relational Mapping) y una arquitectura modular que separa claramente la lógica de negocio, los modelos de datos y las vistas de usuario.

🚀 Características Clave
Cálculo Dinámico de Costos: Computa automáticamente el precio total de la estancia basándose en la categoría de la habitación (Estándar, Suite, Deluxe) y la duración.

Operaciones CRUD Completas: Interfaz integral para Crear, Leer, Actualizar y Eliminar registros de alquiler.

Validación de Datos: Validaciones tanto en el lado del servidor como del cliente para campos obligatorios, formatos de fecha y entradas numéricas.

Dashboard Responsivo: Vista basada en tablas modernas y limpias para el monitoreo de alquileres activos e históricos.

Persistencia de Datos: Integración total con SQL Server para garantizar la seguridad y permanencia de la información.

🛠️ Stack Tecnológico
Backend: C# con ASP.NET Core 8.0 (Patrón MVC).

ORM: Entity Framework Core (Enfoque Code First / DB First).

Base de Datos: Microsoft SQL Server.

Frontend: Razor Pages, HTML5, CSS3 y Bootstrap para un diseño responsivo.

🧠 Lógica y Esquema de Base de Datos
El sistema se centraliza en la entidad RoomRental (Alquiler de Habitación). Los atributos clave incluyen:

Nombre del Huésped: String (Requerido).

Tipo de Habitación: Selección categorizada (Estándar, Suite, Deluxe).

Duración: Entero (Días).

Costo Total: Campo calculado (Tarifa * Días).

Fragmento del Modelo de Datos (C#)
C#
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
💻 Detalles de Implementación
Lógica de Negocio: Tarifas Automáticas
La aplicación implementa una lógica especializada dentro del Controlador para gestionar los niveles de precios. Esto asegura que el usuario solo necesite ingresar el tipo de habitación y los días, mientras el sistema garantiza la precisión financiera.

C#
// Fragmento de lógica dentro del Controlador
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
Componentes de Vista (Razor)
La interfaz utiliza vistas fuertemente tipadas (strongly-typed views) para vincular los modelos de datos con los formularios HTML, asegurando que los mensajes de validación se muestren en tiempo real.

📂 Estructura del Proyecto
Plaintext
StayManager-MVC/
├── Controllers/
│   └── RentalController.cs    # Maneja la lógica CRUD y cálculos de precios
├── Models/
│   └── RoomRental.cs          # Estructura de datos y reglas de validación
├── Data/
│   └── ApplicationDbContext.cs # Contexto de BD y configuración de EF
├── Views/
│   ├── Rental/
│   │   ├── Index.cshtml       # Panel principal de registros
│   │   ├── Create.cshtml      # Formulario de nuevo registro
│   │   └── Edit.cshtml        # Interfaz de modificación
│   └── Shared/
├── wwwroot/                   # Archivos estáticos (CSS, JS, Imágenes)
└── Program.cs                 # Configuración de inicio e Inyección de Dependencias
🔧 Instalación y Configuración
Clonar el repositorio:

Bash
git clone https://github.com/tu-usuario/staymanager-mvc.git
Configuración de la Base de Datos: Actualizar la cadena de conexión (ConnectionStrings) en el archivo appsettings.json con los datos de tu instancia de SQL Server.

Aplicar Migraciones:

Bash
dotnet ef database update
Ejecutar la aplicación:

Bash
dotnet run
🎓 Resultados del Aprendizaje
Este proyecto demuestra competencia en:

Patrón MVC: Separación de responsabilidades para un desarrollo web escalable.

Entity Framework Core: Gestión de datos relacionales mediante objetos C#.

Validación de Formularios: Implementación de manejo de errores robusto para entradas de usuario.

Lógica de Backend: Procesamiento de cálculos condicionales y flujos de datos.

📄 Licencia
Este proyecto está bajo la Licencia MIT.