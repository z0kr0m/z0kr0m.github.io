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

<figure markdown="span">
![conexion](../../images/ClaseConexion.png)

 <figcaption>Un vistazo de cómo quedaría la clase conexión</figcaption>
</figure>

------


## Clases Modelo

Vamos a por las clases del modelo, (son las 3 tablas que has creado en tu base de datos).

!!!note
    Siempre empezamos por las que no tienen ninguna foreign key, en este caso es `Profesor`

    ```csharp
        public class Profesor
    {
        public int Id { get; set; }
        public string Nombre { get; set; }
    }
    
    ```

A continuación, seguiremos por la que tenga la foreign key de `Profesor`, en este caso, `Curso`

```csharp
 public class Curso
 {
     public int Id { get; set; }
     public string nombre_c { get; set; }
     public int nombre_d { get; set; }
     public int id_profesor { get; set; }
     [ForeignKey(nameof(id_profesor))]
     public Profesor profesor { get; set; }

 }
```

Recordamos que los `Id` si se llaman `Id`, `NombreId` no hace falta poner `[key]` encima suya.

### Foreign keys

Para declarar una [foreign key](/Definiciones/#foreign-key) lo primero que tenemos que hacer es crear un campo que sea del tipo al que va a referenciar, en este caso es un id, por lo tanto tipo `int`.

```csharp
  public int id_profesor { get; set; }
```

Ahora tenemos que declarar un objeto del tipo de la tabla de la que queremos crear una relación.

```csharp
  public Profesor profesor { get; set; }
```

Por úiltimo, especificamos el campo de foreign key (tiene que ser encima del objeto).

```csharp
  [ForeignKey(nameof(id_profesor))]
  public Profesor profesor { get; set; }
```
Si te das cuenta al hacer el `nameof()` estamos especificando el `int` que hemos creado arriba, estamos básicamente diciendo: Quiero formar una relación con la tabla `Profesor` por eso creo un objeto, y dentro de `Profesor` quiero hacer referencia a su clave primaria (id) porque se identifica unívocamente.

![profesor](../../images/SIN_ENTITY/cursoModelo.PNG)

<div> </div>

Por último, la clase `Alumno`

```csharp
  public class Alumno
  {
      public int Id { get; set; }
      public string Nombre { get; set; }

      public string apellido1 { get; set; }

      public string apellido2 { get; set; }

      public string dni {  get; set; } 

      public string direccion {  get; set; }

      public DateOnly fecha_n {  get; set; }

      public string telefono { get; set; }

  }

```

-----


## Controladores


