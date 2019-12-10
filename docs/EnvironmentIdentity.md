# EnvironmentIdentity

Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de variables de ambiente del sistema con el nombre **ASPEN:APIKEY** y **ASPEN:APISECRET**.

<div class="admonition warning">
   <p class="first admonition-title">Atención</p>
   <p class="last">Recuerde que los valores establecidos para una variable de sesión solo se procesan al iniciar el proceso del sistema operativo, así que cualquier cambio en una variable de entorno solo será <i>visible</i> hasta que se reinicie el proceso.</p>
</div>

Tambien puede utilizar el constructor de la clase para personalizar el nombre de las variables de ambiente. Por ejemplo:

```c#
var identity = new EnvironmentIdentity("My_Var_ApiKey", "My_Var_ApiSecret");
```

Para este caso se buscaran las varibles de ambiente `My_Var_ApiKey` y `My_Var_ApiSecret` para asociar los valores con el ApiKey y el ApiSecret respectivamente. Luego, [registre la instancia para ser utilizada como extensión](ServiceLocator.md).

## Vea también
 
- [RegistryIdentity](RegistryIdentity.md)

- [AppConfigIdentity](AppConfigIdentity.md)

- [HardCodeIdentity](HardCodeIdentity.md)

- [SecureIdentity](SecureIdentity.md)
