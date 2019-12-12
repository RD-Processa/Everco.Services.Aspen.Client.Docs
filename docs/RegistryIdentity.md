# RegistryIdentity

Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de la configuración en el registro de Windows.

## Ejemplo de la entrada en el registro de Windows

![RegistryEndpoint](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/RegistryEndpointProvider.png?raw=true)

Tambien puede utilizar el constructor de la clase para personalizar el nombre de las entradas de configuración. Por ejemplo:

```c#
var identity = new RegistryIdentity(RegistryRoot.LocalMachine, "SOFTWARE\Aspen\Credentials", "MyApiKey", "MyApiSecret");
```

Para este caso se buscaran las entradas `MyApiKey` y `MyApiSecret` en el registro de Windows bajo la clave `HKEY_LOCAL_MACHINE\SOFTWARE\Aspen\Credentials` para asociar los valores con el ApiKey y el ApiSecret respectivamente. Luego, [registre la instancia para ser utilizada como extensión](ServiceLocator.md).

## Vea también
 
- [EnvironmentIdentity](EnvironmentIdentity.md)

- [RegistryIdentity](RegistryIdentity.md)

- [HardCodeIdentity](HardCodeIdentity.md)

- [SecureFileIdentity](SecureFileIdentity.md)