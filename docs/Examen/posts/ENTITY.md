---
date: 2024-06-23
title: "Entity Framework"
---


 
 
 
## Instalar paquetes Nugget
 

 Primero de todo antes de comenzar, instalamos los siguientes [paquetes Nugget](../Recordatorios.md):

- Microsoft.EntityFrameworkCore 
- Microsoft.EntityFrameworkCore.Design
- Microsoft.EntityFrameworkCore.SqlServer
- Microsoft.EntityFrameworkCore.Tools
----- 

## Cadena de conexión

<div> A continuación, tenemos que declarar la cadena de conexión de nuestra base de datos. </div>
Nos dirigimos al archivo  `App.Settings` en la raiz de nuestro proyecto.
 
 > Agregamos la siguiente cadena:
```json
"ConnectionStrings": {
  "MiConexion": "Data Source=DesktopMJK2;Initial Catalog=Tienda5;User ID=sa;Password=1234;TrustServerCertificate=True;Encrypt=True;Trusted_Connection=True;MultipleActiveResultSets=true"
}
```

<br>
Ten cuidado al copiar la cadena, no te olvides de la coma después del AllowedHost
!!! warning
    
    ![Nuggets](../../images/lacoma.PNG)

### Explicación cadena de conexión

!!! info
    Esta cadena es para SQL server, si pide MySql es diferente, pulsa aquí

- Data Source -> Nombre de nuestra instancia del servidor de base de datos
- Initial Catalog -> El nombre de la base de datos que queramos gestionar
- User -> Tu usuario, si lo tienes por defecto es `sa`
- Password -> La contraseña del usuario, si lo tienes por defecto es `sa` (Si no funciona prueba con 1234)

------

## Crear modelo de datos







 
	
 
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
