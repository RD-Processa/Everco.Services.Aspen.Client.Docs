# URL del servicio

Como se mencionó anteriormente, este valor corresponde con la URL de la instancia del servicio a donde desea conectar. Por ejemplo: https://dev.aspen.com/api (esta URL no es real). Tenga presente que este valor puede cambiar entre ambientes y dependerá en gran parte de la forma como se conecta con nuestros servicios (a través de una red pública, VPN, WAN, LAN, etc), así que es conveniente que el procesamiento de este valor de configuración sea bastante flexible para poder actualizar su valor sin necesidad de realizar un nuevo despliegue. El cliente de Aspen define la interfaz [IEndpointProvider](IEndpointProvider.md) e implementa las clases [EnvironmentEndpointProvider](EnvironmentEndpointProvider.md),  [RegistryEndpointProvider](RegistryEndpointProvider.md) y [AppConfigEndpointProvider](AppConfigEndpointProvider.md) para tal fin. Si ninguna de estas clases satisface sus necesidades, podría hacer su propia implementación de la interfaz IEndpointProvider y [reemplazar el componente en tiempo de ejecución](ServiceLocator.md).

<div class="admonition info">
   <p class="first admonition-title">Nota</p>
   <p class="last">Por defecto, el cliente de Aspen utiliza la clase [EnvironmentEndpointProvider](EnvironmentEndpointProvider.md) para obtener el valor de la URL a donde se debe conectar.</p>
</div>