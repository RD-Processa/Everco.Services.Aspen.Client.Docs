# Descripción general del cliente de Aspen

El cliente de Aspen es una librería que facilita la conexión con el servicio [Aspen](https://processa-aspen.readthedocs.io/) de Evertec Colombia.

Su motivación principal es permitir  a los desarrolladores crear una aplicación con unas pocas líneas de código a través del uso de una librería lista para los ambientes producción, facilitando la depuración y simplificando el acceso al servicio.

## Conceptos clave

### ¿Por qué querría usar el cliente de Aspen?

El cliente de Aspen es una librería  que facilita la conexión con el servicio Aspen. Esto permite que los
desarrolladores se centren en la lógica de su servicio/negocio en lugar de en los detalles técnicos necesarios para interactuar con el  servicio. De esta forma, los desarrolladores no necesitan comprender aspectos ténicos como establecer una conexión, la administración segura de los valores de conexión o aprender cómo conectar el depurador a los servicios para solucionar problemas.

### ¿Cómo hace esto el cliente de Aspen? 

Cuando un desarrollador usa el cliente de Aspen, crear una conexión con el servicio es tan fácil como crear una aplicación de consola (en realidad cualquier tipo de aplicación). Una vez que se crea la aplicación, el desarrollador solo tendrá que proporcionar los datos de conexión y con unas pocas líneas de configuración, el desarrollador prodrá establecer una conexión segura con el servicio.

### ¿Qué sucede si mi desarrollo requiere opciones personalizadas? 

El cliente de Aspen admite la personalización de opciones comúnmente utilizadas que incluyen entre otras:

- Personalizar logs
- Personalizar los procesos de serialización
- Personalizar el proxy de conexión con Internet
- Muchas personalizaciones más que se mostrarán en detalle en la sección [Uso de extensiones](ServiceLocator.md)

### ¿Como luce el código para conectar con el servicio Aspen?

```c#

// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client =  AutonomousApp.Initialize()
  .RoutingTo("YourUrl")
  .WithIdentity("YourApiKey", "YourApiSecret")
  .Authenticate()
  .GetClient();
```

Donde:

- **YourUrl** => Corresponde con la URL del servicio a donde desea conectar (puede variar entre ambientes QA/Dev/Prod). Por ejemplo: https://dev.aspen.com/api (esta URL no es real). Variará entre ambientes y dependerá en gran parte de la forma como se conecta con nuestros servicios (a través de una red pública, VPN, WAN, LAN, etc)

- **YourApiKey** => Corresponde con el valor del ApiKey entregado a su entidad a través del correo electrónico de forma privada y segura.

- **YourApiSecret** => Corresponde con el valor del ApiSecret ([una cadena altamente entrópica](https://es.wikipedia.org/wiki/Entrop%C3%ADa_(computaci%C3%B3n))) entregado a su entidad a través del correo electrónico de forma privada y segura.


