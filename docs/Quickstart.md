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
var client =  AutonomousApp.Initialize()
	.RoutingTo("YourUrl")
	.WithIdentity("YourApyKey", "YourApiSecret")
	.Authenticate()
	.GetClient();
```

Donde:

- **YourUrl** => Corresponde con la URL del servicio a donde desea conectar (puede variar entre ambientes QA/Dev/Prod). Por ejemplo: https://dev.aspen.com/api (esta URL no es real). Variará entre ambientes y dependerá en gran parte de la forma como se conecta con nuestros servicios (a través de una red pública, VPN, WAN, LAN, etc)

- **YourApyKey** => Corresponde con el valor del ApiKey entregado a su entidad a través del correo electrónico de forma privada y segura.

- **YourApiSecret** => Corresponde con el valor del ApiSecret ([valor altamente entrópico](https://es.wikipedia.org/wiki/Entrop%C3%ADa_(computaci%C3%B3n))) entregado a su entidad a través del correo electrónico de forma privada y segura.


### ¿Por qué necesito usar claves de API?

Las claves de API identifican al proyecto (la aplicación o el sitio) que realiza la llamada a la API. Ayudan a Identificar a la aplicación o proyecto que hace uso del API y se generan para el proyecto que realiza la llamada.  Su uso puede restringirse a un entorno específico o una aplicación específica.

Dado que identifican al proyecto que las usa, las claves de API permiten que la información se asocie con ese proyecto y que se rechace llamadas de otros proyectos que no tienen acceso o que no se habilitaron para el uso de la API o de la operación (método) en la API.

### Mejores prácticas para mantener sus claves API seguras

Cuando use claves API en sus aplicaciones, tenga cuidado de mantenerlas seguras. Exponer públicamente sus credenciales puede hacer que su cuenta se vea comprometida, lo que podría generar cargos inesperados. Para ayudar a mantener sus claves API seguras, se recomienda seguir algunas prácticas de la industria:

- No incrustar claves API directamente en el código. Las claves API que están incrustadas en el código pueden exponerse accidentalmente al público. Por ejemplo, puede olvidar eliminar las claves del código en su repositorio de código fuente. En lugar de incrustar sus claves API en sus aplicaciones, almacénelas en variables de entorno o en archivos fuera del código fuente de su aplicación.

- No almacenar claves API en archivos dentro del código fuente de su aplicación. Si almacena claves API en archivos, mantenga los archivos fuera del código fuente de su aplicación para asegurarse de que sus claves no terminen en su sistema de control de código fuente. Esto es particularmente importante si utiliza un sistema de administración de código fuente público como GitHub.

- Configurar restricciones para su uso en la aplicación y la clave API. Al agregar restricciones, puede reducir el impacto de una clave API comprometida.

- Eliminar las claves API innecesarias para minimizar la exposición a los ataques.

- Reciclar sus claves API periódicamente. Puede solicitar la generación de claves API en cualquier momento. Luego, actualice sus aplicaciones para usar las claves recién generadas. Sus claves antiguas dejaran de funcionar luego de que sus aplicaciones estén listas para utilizar las claves de reemplazo.

- Usar una clave API por cada ambiente. De esta forma mantiene control de los datos a los que se está accediendo en cada ambiente. No es lo mismo que se comprometa una clave en un ambiente de pruebas (donde los datos están despersonalizados y muchas veces son ficticios), a que se comprometa una clave en ambiente de producción donde los datos son reales. 

- Revisar su código antes de publicarlo públicamente. Asegúrese de que su código no contenga claves API ni ninguna otra información privada antes de hacer que su código esté disponible públicamente.
