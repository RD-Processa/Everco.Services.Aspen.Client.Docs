# EnvironmentEndpointProvider

Obtiene la Url base del servicio Aspen con el que se requiere conectar y el tiempo de espera para las respuestas desde las variables de ambiente con el nombre **ASPEN:SERVICE_URL** y **ASPEN:SERVICE_TIMEOUT**

El valor de la variable **ASPEN:SERVICE_URL** debería tener la [forma de una URL](https://en.wikipedia.org/wiki/URL)

El valor de la variable **ASPEN:SERVICE_TIMEOUT** debería corresponder con la forma `[ws][-]{ d | [d.]hh:mm[:ss[.ff]] }[ws]` como se describe [aquí](https://docs.microsoft.com/en-us/dotnet/api/system.timespan.parse). Por ejemplo, para especificar una espera de máximo 15 segundos en cada solicitud, el valor a configurar sería `00:00:15`.

<div class="admonition warning">
   <p class="first admonition-title">Atención</p>
   <p class="last">Recuerde que los valores establecidos para una variable de sesión solo se procesan al iniciar el proceso del sistema operativo, así que cualquier cambio en una variable de entorno solo será <i>visible</i> hasta que se reinicie el proceso.</p>
</div>

Tambien puede utilizar el constructor de la clase para personalizar el nombre de las variables de ambiente. Por ejemplo:

```c#
var provider = new EnvironmentEndpointProvider("MyVAR1", "MyVAR2");
```

Para este caso se buscaran las varibles de ambiente `MyVAR1` y `MyVAR2` para asociar los valores con la Url del servicio y el tiempo de espera respectivamente. Luego, [registre la instancia para ser utilizada como extensión](ServiceLocator.md).

## Vea también

- [IEndpointProvider](IEndpointProvider.md)

- [RegistryEndpointProvider](RegistryEndpointProvider.md)

- [AppConfigEndpointProvider](AppConfigEndpointProvider.md)
