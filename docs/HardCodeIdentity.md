# HardCodeIdentity

NO SE RECOMIENDA EL USO DE ESTA CLASE. Se provee solo con fines de pruebas de concepto.


<div class="admonition error">
   <p class="first admonition-title">NO SE RECOMIENDA EL USO DE ESTA CLASE</p>
   <p class="last">Esta clase se provee solo con fines de pruebas de concepto. Se marca con el atributo <a href="https://docs.microsoft.com/en-us/dotnet/api/system.obsoleteattribute" target="_blank">Obsolete</a> para que genere un mensaje de advertencia en el proceso de compilación.<p>
</div>

## Ejemplo de uso para pruebas de concepto

```c#
var identity = new HardCodeIdentity("YourApiKey", "YourApiSecret");
ServiceLocator.Instance.SetDefaultIdentity(identity);
```

Para este caso se utilizaran los valores proporcionados en el constructor de la clase para asociar los valores con el ApiKey y el ApiSecret respectivamente. Luego, [registre la instancia para ser utilizada como extensión](ServiceLocator.md).

## Vea también
 
- [EnvironmentIdentity](EnvironmentIdentity.md)

- [AppConfigIdentity](AppConfigIdentity.md)

- [RegistryIdentity](RegistryIdentity.md)

- [SecureIdentity](SecureIdentity.md)
