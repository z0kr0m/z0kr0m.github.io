---
date: 2024-06-23
title: "Entity Framework"
---


 
 
 
## INSTALAR PAQUETES NUGGET
 

 Primero de todo antes de comenzar, instalamos los siguientes [paquetes Nugget](../Recordatorios.md):

- Microsoft.EntityFrameworkCore 
- Microsoft.EntityFrameworkCore.Design
- Microsoft.EntityFrameworkCore.SqlServer
- Microsoft.EntityFrameworkCore.Tools



  
 
 
App.Settings
 
"ConnectionStrings": {
  "MiConexion": "Data Source=TU-MAMA-ES-LESB;Initial Catalog=Tienda5;User ID=sa;Password=1234;TrustServerCertificate=True;Encrypt=True;Trusted_Connection=True;MultipleActiveResultSets=true"
}
 
 
	
 
En Models
 
 
todos los modelos
 
despues
 
Crear clase  inherited DbContext
 
 
    public Contexto(DbContextOptions<Contexto> options) : base(options)
    {
    }
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
    }
 
    public DbSet<Producto> misProductos { get; set; } // Nombre de la tabla
}
 
 
 
programcs
 
builder.Services.AddDbContext<Contexto>(
options =>
{
 
options.UseSqlServer(builder.Configuration.GetConnectionString("MiConexion"));
});
 
 
Add-Migration "aa"
 
Update-Database
 
 
 
controller model  with EntityTemplate
 
 
private readonly TiendaDbContext _context;
public Productos(TiendaDbContext _context )
{
           this._context = _context;
}  


## Prueba
