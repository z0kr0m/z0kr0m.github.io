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

El siguiente paso es crear los modelos, recordamos que un modelo es una representación de una tabla.
<br>

 ![modelo](../../images/modelo.PNG) 

Creamos una clase por tabla en la carpeta Models

###  Ejemplo modelo

```csharp
 public class Producto
 {
     public int Id { get; set; }
     public string? Nombre { get; set; }

     [Column(TypeName = "decimal(4, 2)")]
     public decimal Precio { get; set; }
     public int CategoriaId { get; set; }
     [ForeignKey(nameof(CategoriaId))]
     public Categoria categoria { get; set; } = null!;

 }
```
Cada propiedad con public y su respectivo tipo de dato (Recuerda: Si en la base de datos es varchar, aquí lo ponemos como string).
<br>

!!! note
    Las primary key se identifica con: `Id`, `NombreId` o especificando `[key]` arriba en el caso de que tengamos un nombre diferente.
    <br>

- `[Column(TypeName = "decimal(4, 2)")]` Es para especificar de cuantas cifras es el numero (4) y cuantos números después de la coma tiene: 1000,45 sería un ejemplo con esta configuración.

- `[ForeignKey(nameof(CategoriaId))]` Identifica a una foreign key, primero creamos un campo, en este caso de tipo int, después, creamos un objeto del modelo que estamos haciendo referencia.

```csharp
// Primero la propiedad para almacenar la foreign key
 public int CategoriaId { get; set; }
 // Aquí especificamos que es una foreign key y dentro del parentesis le pasamos la propiedad de arriba
 [ForeignKey(nameof(CategoriaId))]
 // La siguiente propiedad es un objeto del modelo (la otra tabla)
 public Categoria categoria { get; set; } = null!;
```
<br>
De esta manera crearíamos todos los modelos, cambiando tipos de datos y nombres, (No todos los modelos tienen foreign keys).

------

## Crear clase DbContext

Ahora nos toca crear una clase DbContext que va a actuar como puente entre la base de datos y nuestra aplicación.
Para ello, en la carpeta `Models` creamos una nueva clase, en este caso la voy a llamar `Contexto`, pero puede tener otro nombre.
Mi recomendación es que no lo cambies, para que no haya luego lios con nombres.

```csharp
public class Contexto : DbContext
{
    public Contexto(DbContextOptions<Contexto> options) : base(options)
    {
    }
   
    public DbSet<Producto> misProductos { get; set; }
    public DbSet<Categoria> misCategorias { get; set; }
}
```

<div> Si le has llamado de otra forma a la clase, reemplaza Contexto por el nombre que le hayas asignado. </div>
No te olvides de agregar `: Dbconext` después del nombre de la clase.

Los `DbSet<>` nos van a servir para mapear las tablas de la base de datos, por cada modelo que crees, tienes que agregar un `DbSet`, en este ejemplo tenemos solo dos, producto y catergoría, puedes fijarte [aquí](/Examen/2024/06/23/entity-framework/#crear-modelo-de-datos) 

----

Una vez tenemos la clase `Contexto` configurada, tenemos que editar el fichero `program.cs`

```c#
builder.Services.AddDbContext<Contexto>(
 options =>
 {
     options.UseSqlServer(builder.Configuration.GetConnectionString("MiConexion"));
 });
```
CUIDADO DONDE SITUAMOS EL CÓDIGO DE ARRIBA

!!! warning
    ![program](../../images/program.png)
    
Tenemos que asegurarnos de que está por encima del `builder.Build`


Teniendo los modelos, la clase contexto y la cadena de conexión tenemos dos opciones: 

- No tenemos la base de datos creada, (Nos piden que lo hagamos mediante migraciones).
- Ya tenemos la base de datos creada, (Hemos hecho el script manual). -> Saltar directamente [aquí](/Examen/2024/06/23/entity-framework/#crud-con-entity-framework)

------

## Migraciones

El primer paso para hacer una migración es abrir una terminal -> Herramientas -> Nuget Manager -> Consola

![boton](../../images/nuggetTerminal.png)

Dentro de la ternminal ejecutamos el siguiente comando:

```csharp
Add-Migration "nombre"
```



-----



## CRUD con Entity Framework

----- 

```csharp
[Key]
[DatabaseGenerated(DatabaseGeneratedOption.Identity)]  // Auto increment
public int Id { get; set; }
```







