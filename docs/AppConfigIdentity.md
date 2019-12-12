# AppConfigIdentity

Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de la entradas de configuración en la sección appSettings de un archivo de configuración XML.

## Archivo de ejemplo

Suponga un archivo XML de configuración con el siguiente texto:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <add key="ASPEN:APIKEY" value="YourApiKey" />
	<add key="ASPEN:APISECRET" value="YourApiSecret" />
  </appSettings>
</configuration>
```

Tambien puede utilizar el constructor de la clase para personalizar el nombre de las entradas de configuración. Por ejemplo:

```c#
var identity = new AppConfigIdentity("My_ApiKey", "My_ApiSecret");
```

Para este caso se buscaran las entradas `My_ApiKey` y `My_ApiSecret`para asociar los valores con el ApiKey y el ApiSecret respectivamente. Luego, [registre la instancia para ser utilizada como extensión](ServiceLocator.md).

## Vea también
 
- [EnvironmentIdentity](EnvironmentIdentity.md)

- [AppConfigIdentity](AppConfigIdentity.md)

- [HardCodeIdentity](HardCodeIdentity.md)

- [SecureFileIdentity](SecureFileIdentity.md)
