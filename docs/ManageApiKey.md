# API Keys

## ¿Por qué necesito usar claves de API?

Las claves de API identifican al proyecto (la aplicación o el sitio) que realiza la llamada a la API. Ayudan a Identificar a la aplicación o proyecto que hace uso del API y se generan para el proyecto que realiza la llamada.  Su uso puede restringirse a un entorno específico o una aplicación específica.

Dado que identifican al proyecto que las usa, las claves de API permiten que la información se asocie con ese proyecto y que se rechace llamadas de otros proyectos que no tienen acceso o que no se habilitaron para el uso de la API o de la operación (método) en la API.

El cliente de Aspen define la interfaz IAppIdentity e implementa las clases EnvironmentIdentity, RegistryIdentity, AppConfigIdentity, HardCodeIdentity y SecureIdentity para tal fin. Si ninguna de estas clases satisface sus necesidades, podría hacer su propia implementación de la interfaz IAppIdentity y reemplazar el componente en tiempo de ejecución.

<div class="admonition tip">
   <p class="first admonition-title">Tip</p>
   <p class="last">Por defecto, el cliente de Aspen utiliza la clase <a href="../EnvironmentIdentity">EnvironmentIdentity</a> para obtener el valor de las credenciales de conexión.</p>
   <p class="last">Puede utilizar cualquiera de las clases que se mencionan a continuación para definir los valores que utilizará el cliente de Aspen.</p>
</div>

## [IAppIdentity](IAppIdentity.md)

- Define la información de identidad de una aplicación para autenticar las solicitudes al servicio Aspen.

## [EnvironmentIdentity](EnvironmentIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de variables de ambiente del sistema.

## [RegistryIdentity](RegistryIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de la configuración en el registro de Windows.

## [AppConfigIdentity](AppConfigIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de la entradas de configuración en la sección appSettings de un archivo de configuración XML.

## [HardCodeIdentity](HardCodeIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de los valores proporcionados en el constructor de la clase. NO SE RECOMIENDA EL USO DE ESTA CLASE. Se provee solo con fines de pruebas de concepto.

## [SecureIdentity](SecureIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de un archivo de texto cifrado.

## Obtener una instancia del servicio

Para obtener una instancia de la clase que representa la conexión con el servicio Aspen, basta con invocar el método GetClient(). El cliente de Aspen se encargará de solicitar un token de autenticación con las credenciales proporcionadas y lo almacenará en una Cache interna para su uso posterior.

```c#
var client = AutonomousApp.Initialize()
   .WithDefaults()
   .Authenticate()
   .GetClient();
```

A través de la variable `client` podrá acceder a los módulos del servicio Aspen como veremos más adelante.

![IntelliSense](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/IntelliSense.png?raw=true)

## ¿Cómo puedo acceder al token de autenticación?

Para evitar que en cada llamada al servicio de Aspen deba entregar su **ApiKey** y **ApiSecret**, se usa un token de autenticación, que no es más que una cadena de texto larga y cifrada que se entrega en respuesta de la autenticación del servicio Aspen. Esta cadena contiene el token que podrá utilizar para futuros accesos y así certificar que su proyecto/aplicación está autenticado contra el servicio Aspen.

De forma predeterminada, el cliente de Aspen almacena en memoria el token de autenticación emitido para el proyecto/aplicación y así reutilizarlo con las siguientes operaciones mientras este vigente.

Cuando se crea una instancia del cliente utilizando la sintaxis anterior, el cliente se encargará de agregar las cabeceras de autenticación requeridas, agregar la información solicitada por el servicio (como el Nonce y el Epoch), serializar la solicitud en formato JSON/JWT, procesar la respuesta y almacenar el token de autenticación en cache. Si necesita acceder al token generado, puede utilizar la propiedad `AuthToken` de la variable `client` que tiene tres importante propiedades.

| Propiedad | Descripción |
| :-:|---|
| **ExpiresAt** | Fecha y hora en que expira el token de auteniticación. |
| **IssueAt** | Fecha y hora en que se emitió el token de auteniticación. |
| **Token** | Cadena que representa el token de autenticación. |

![AuthToken](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/AuthToken.png?raw=true)

## Usar el cliente ignorando el token de autentiación en cache

Al ignorar los valores del token de autenticación almacenado en memoria, el cliente de Aspen solicitará nuevos tokens de autenticación por cada operación que requiera su proyecto/aplicación, pero esto debe ser un factor de rendimiento para poner en consideración. El método `AuthenticateNoCache` es el que debe utilizar si toma la decisión de ignorar el token de autenticación en cache \(**no recomendado**\).

```c#
var client = AutonomousApp.Initialize()
   .WithDefaults()
   .AuthenticateNoCache()
   .GetClient();
```
