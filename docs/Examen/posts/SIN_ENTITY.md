---
date: 2024-06-24
title: "Sin Entity Framework"
---

!!! note
    En este projecto vamos a usar SQL server, en el caso de que nos pidan MySql mira [aquí](/Examen/Recordatorios/#conexion-mysql)


## Instalar paquetes NuGet
Al no usar Entity Framework vamos a necesitar menos paquetes [NuGet](../Recordatorios.md)
<div> </div>
- System.Data.SqlClient

## Crear clase conexión

En la clase `Models` creamos una clase en este caso la vamos a llamar `Conexion`

```csharp
  public class Conexion
  {
      private string cadenaConexion;
      private SqlConnection conexion;
  }
```

Lo primero es asignar los atributos necesarios, una string con la cadena de conexión y un objeto `SqlConnection`



```csharp
 public Conexion()
 {

     conexion = new SqlConnection();

     conexion.ConnectionString = "Data Source=T24W16\\MSSQLSERVER2;Initial Catalog=Tienda;User ID=sa;Password=sa;TrustServerCertificate=True;Encrypt=True;Trusted_Connection=True";

     conexion.Open(); 

 }
```
Ahora cremos el constructor donde instanciamos el objeto `SqlConnection`, le pasamos la conexión y abrimos la conexión para que esté activa durante todo el tiempo de vida de la aplicación.

-----

### Sintaxis cadena conexión

!!! info
    Esta cadena es para SQL server, si pide MySql es diferente, pulsa [aquí](/Examen/Recordatorios/#conexion-mysql)

- Data Source -> Nombre de nuestra instancia del servidor de base de datos
- Initial Catalog -> El nombre de la base de datos que queramos gestionar
- User -> Tu usuario, si lo tienes por defecto es `sa`
- Password -> La contraseña del usuario, si lo tienes por defecto es `sa` (Si no funciona prueba con 1234)

<div> </div>

-----

### Métodos clase conexión

Por último, agregamos un método que returne la conexión, (vamos a usarlo más adelante para hacer las peticiones).

```csharp
 public SqlConnection returnarConexion()
 {
     return conexion;
 }
```

![conexion](../../images/ClaseConexion.png)

