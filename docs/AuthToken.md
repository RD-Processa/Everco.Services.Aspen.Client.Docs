# Token de autenticación

Para evitar que en cada llamada al servicio de ASPEN se deba entregar su **ApiKey** y **ApiSecret** se usa un token de autenticación, que no es más que una cadena de texto larga y encriptada que se entrega en respuesta de la autenticación del servicio de ASPEN. Esta cadena contiene el token que usará para futuros accesos y así certificar que su proyecto/aplicación está autenticado para usar recursos del servicio.

De forma predeterminada, el cliente de ASPEN almacena en memoria el token de autenticación emitido para el proyecto/aplicación y así reutilizarlo con las siguientes operaciones mientras este vigente.

### Usar el cliente con token almacenado en caché

Para inicializar un cliente de ASPEN que conserve en memoria la información del token de autenticación emitido, basta con usar la funcionalidad: `Authenticate()`. Una vez inicializado el cliente, puede verificar los datos del token emitido para su proyecto/aplicación con la propiedad: `AuthToken`

```c#
var client = AutonomousApp.Initialize()
	.RoutingTo("YourUrl")
	.WithIdentity("YourApiKey", "YourApiSecret")
	.Authenticate()
	.GetClient();

Console.WriteLine("Token de Autenticación => {0}", client.AuthToken.Token);
Console.WriteLine("Fecha de emisión => {0}", client.AuthToken.IssueAt);
Console.WriteLine("Fecha de expiración => {0}", client.AuthToken.ExpiresAt);
```

### Usar el cliente ignorando los valores almacenados en caché

Al ignorar los valores del token de autenticación almacenado en memoria, el cliente de ASPEN solicitará nuevos tokens de autenticación por cada operación del API de ASPEN que requiera su proyecto/aplicación; esto puede ser un factor de rendimiento que deba considerar.

Antes de inicializar un cliente de ASPEN use la funcionalidad: `AuthenticateNoCache()`

```c#
var client = AutonomousApp.Initialize()
	.RoutingTo("YourUrl")
	.WithIdentity("YourApiKey", "YourApiSecret")
	.AuthenticateNoCache()
	.GetClient();
``` 

## Vigencia

Luego de realizar de la autenticación usando su **ApiKey** y **ApiSecret**, ASPEN devuelve al cliente un token de autenticación que incluye los datos de emisión y vigencia o fecha de expiración. El cliente de ASPEN se asegura de comprobar el estado del token (si está almacenado en memoria) en cualquiera de las funcionalidades implementadas.
