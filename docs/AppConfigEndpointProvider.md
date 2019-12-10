# AppConfigEndpointProvider

Obtiene la Url base del servicio Aspen con el que se requiere conectar y el tiempo de espera para las respuestas a partir de las entradas en una sección appSettings de un archivo de configuración XML.

El valor de la variable **ASPEN:SERVICE_URL** debería tener la [forma de una URL](https://en.wikipedia.org/wiki/URL)

El valor de la variable **ASPEN:SERVICE_TIMEOUT** debería corresponder con la forma `[ws][-]{ d | [d.]hh:mm[:ss[.ff]] }[ws]` como se describe [aquí](https://docs.microsoft.com/en-us/dotnet/api/system.timespan.parse). Por ejemplo, para especificar una espera de máximo 15 segundos en cada solicitud, el valor a configurar sería `00:00:15`.

## Archivo de ejemplo

Suponga un archivo XML de configuración con el siguiente texto:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <add key="ASPEN:SERVICE_URL" value="https://dev.aspen.com/api" />
	<add key="ASPEN:SERVICE_TIMEOUT" value="00:00:15" />
  </appSettings>
</configuration>
```

Tambien puede utilizar el constructor de la clase para personalizar el nombre de las entradas de configuración. Por ejemplo:

```c#
var provider = new AppConfigEndpointProvider("My_Key_Url", "My_Key_Timeout");
```

Para este caso se buscaran las entradas `My_Key_Url` y `My_Key_Timeout` para asociar los valores con la Url del servicio y el tiempo de espera respectivamente. Luego, [registre la instancia para ser utilizada como extensión](ServiceLocator.md).

### Vea también

- [IEndpointProvider](IEndpointProvider.md)

- [RegistryEndpointProvider](RegistryEndpointProvider.md)

- [EnvironmentEndpointProvider](EnvironmentEndpointProvider.md)
