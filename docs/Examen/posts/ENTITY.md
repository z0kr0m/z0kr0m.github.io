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

