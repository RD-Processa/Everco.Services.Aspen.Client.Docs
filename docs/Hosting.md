# API Server y URL Base

La URL del servicio, corresponde con la instancia del servicio a donde desea conectar. Por ejemplo: https://dev.aspen.com/api (esta URL no es real). Tenga presente que este valor puede cambiar entre ambientes y dependerá en gran parte de la forma como se conecta con nuestros servicios (a través de una red pública, VPN, WAN, LAN, etc), así que es conveniente que el procesamiento de este valor de configuración sea bastante flexible para poder actualizar su valor sin necesidad de realizar un nuevo despliegue. El cliente de Aspen define la interfaz [IEndpointProvider](IEndpointProvider.md) e implementa las clases [EnvironmentEndpoint](EnvironmentEndpoint.md),  [RegistryEndpoint](RegistryEndpoint.md) y [AppConfigEndpoint](AppConfigEndpoint.md) para tal fin. Si ninguna de estas clases satisface sus necesidades, podría hacer su propia implementación de la interfaz [IEndpointProvider](IEndpointProvider.md) y [reemplazar el componente en tiempo de ejecución](ServiceLocator.md).

<div class="admonition info">
   <p class="first admonition-title">Nota</p>
   <p class="last">Por defecto, el cliente de Aspen utiliza la clase <a href="../EnvironmentEndpoint">EnvironmentEndpoint</a> para obtener el valor de la URL a donde se debe conectar.</p>
</div>

> Puede utilizar cualquiera de las clases que se mencionan a continuación para definir los valores que utilizará el cliente de Aspen.

## [IEndpointProvider](IEndpointProvider.md)

- Define la Url base del servicio Aspen con el que se requiere conectar y el tiempo de espera para las respuestas.

## [EnvironmentEndpoint](EnvironmentEndpoint.md)

- Obtiene la Url base del servicio Aspen con el que se requiere conectar y el tiempo de espera para las respuestas desde [variables de ambiente](https://docs.microsoft.com/en-us/dotnet/api/system.environment).

## [RegistryEndpoint](RegistryEndpoint.md)

- Obtiene la Url base del servicio Aspen con el que se requiere conectar y el tiempo de espera para las respuestas a partir de la configuración en el [registro de Windows](https://docs.microsoft.com/en-us/dotnet/api/microsoft.win32.registry).

## [AppConfigEndpoint](AppConfigEndpoint.md)

- Obtiene la Url base del servicio Aspen con el que se requiere conectar y el tiempo de espera para las respuestas a partir de las entradas de configuración en una sección appSettings de un [archivo de configuración en formato XML](https://docs.microsoft.com/en-us/dotnet/framework/configure-apps/index).
