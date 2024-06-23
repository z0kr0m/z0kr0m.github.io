# RECORDATORIOS

## Plantilla
  <div>Los projectos que vamos a crear son usando la plantilla MVC (Con C#) </div>

   ![Image title](/images/Capture.PNG)


## Paquetes NuGet
<div> Para instalar paquetes NuGet... </div>

 ![Nuggets](../images/nugget.png)


## Conexión MySql

 Cadena de conexión en MySql
 ```csharp
   private string "server=localhost;database=empleados;user=root;password=1234";
 ```

 Si quieres hacer una clase simplemente:

 ```csharp
 public class conexionDB
    {
        private  string stringDB = "server=localhost;database=empleados;user=root;password=1234";
        private MySqlConnection conexion;
        public conexionDB()
        {
            
            conexion = new MySqlConnection(stringDB);
        }

        public void AbrirConexion()
        {
            try
            {
                conexion.Open();
                Console.WriteLine("Conexión establecida");
            } catch (Exception e)
            {
                Console.WriteLine("La conexión ha fallado");
                Console.WriteLine(e.Message);
            }
            {
                
            }

        }

        public void CerrarConexion()
        {
            try
            {
                conexion.Close();
            }
            catch (Exception e) 
            {
                Console.WriteLine("La conexión ha fallado");
                Console.WriteLine(e.Message);
            }
        }

        public MySqlConnection returnarConexion()
        {
            return conexion;
        }

    }
 ```