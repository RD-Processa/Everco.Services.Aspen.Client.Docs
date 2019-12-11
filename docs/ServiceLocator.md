## Reemplazando componentes

La clase ServiceLocator tiene como objetivo facilitar la modularidad de la aplicación eliminando las dependencias entre implementaciones. Las interfaces son una de las herramientas más flexibles y potentes para desacoplar los componentes de software y mejorar la capacidad de mantenimiento del código. El patrón del localizador de servicios es una opción para evitar las dependencias, al actuar como un registro central que proporciona implementaciones de diferentes interfaces. Al hacerlo, los componentes que usan una interfaz ya no necesitan conocer la clase que implementa la interfaz. En lugar de crear una instancia de cada clase, se obtiene una implementación a través del localizador de servicios, que actúa como el registrador único para todos los servicios que se utilizan en la aplicación.

Como siempre en la ingeniería de software, no hay balas de plata por lo que el uso de este patrón tiene apoyo y rechazo en la comunidad.

Para acceder a la instancia actual de `ServiceLocator`, se utiliza la propiedad estática `Instance` y a partir de esta instancia se pueden establecer valores para cada componente en tiempo de ejecución.  

Por ejemplo, para establecer la instancia de configuración para el descubrimiento de la Url del servicio Aspen, puede utilizar el método `SetDefaultEndpoint` que recibe como parámetro la instancia de una clase que implemente la interfaz `IEndpointProvider`.

## Veamos un ejemplo

```c#
// Establece que se utilice una instancia de RegistryEndpoint para obtener la configuración de conexión con el servicio Aspen.
ServiceLocator.Instance.SetDefaultEndpoint(new RegistryEndpoint());
```

El mismo principio aplica para los componentes del sistema que se mencionan en la siguiente lista:

| Operación/Método  | Descripción  | Valor predeterminado |
|:-:|---|:-:|
| **SetDefaultEndpoint**  | Establece la instancia de configuración que se debe utilizar para el descubrimiento de la Url y el tiempo de espera del servicio Aspen.  | **EnvironmentEndpoint** |
| **SetDefaultIdentity**  | Establece la instancia de configuración que se debe utilizar para el descubrimiento de las credenciales de conexión que se envían en las cabeceras de autenticación.  | **EnvironmentIdentity** |
| **RegisterEpochGenerator**   | Establece la instancia que se debe utilizar para generar las marcas de tiempo Unix que se requieren en cada petición que se envía al servicio Aspen.  | **UnixEpochGenerator** |
| **RegisterHeadersManager**  |  Establece la instancia que se debe utilizar para establecer las cabeceras personalizadas requeridas por el servicio Aspen. | **DefaultHeadersManager** |
| **RegisterJwtJsonSerializer**  | Establece la instancia que se debe utilizar para serializar la información enviada y generada para las solicitudes hacia/desde el servicio Aspen.  | **JsonSerializer** |
| **RegisterLoggingProvider**  | Establece la instancia que se debe utilizar para escribir la información de seguimiento (logging) generada localmente por la librería.  | **NullLoggingProvider** |
| **RegisterNonceGenerator**  |  Establece la instancia que se debe utilizar para generar números o cadenas aleatorias de un único uso. | **GuidNonceGenerator** |
| **RegisterPayloadClaimNames**  | Establece la instancia que se debe utilizar para establecer los nombres de las reclamaciones que se utilizan en la carga útil (Payload) de una solicitud hacia el servicio Aspen.  | **DefaultPayloadClaimElement** |
| **RegisterPayloadClaimsManager**  | Establece la instancia que se debe utilizar para establecer las reclamaciones que se utilizan en la carga útil (Payload) de una solicitud hacia el servicio Aspen.  | **DefaultPayloadClaimsManager**|
| **RegisterRequestHeaderNames**  | Establece la instancia que se debe utilizar para establecer los nombres que se utilizan en las cabeceras personalizadas de las solicitudes hacia el servicio Aspen. | **DefaultHeaderElement** |
| **RegisterWebProxy** | Establece la instancia que se debe utilizar para establecer la configuración del servidor Proxy que se utiliza para establecer la comunicación hacia el servicio Aspen   | **NullWebProxy** |
