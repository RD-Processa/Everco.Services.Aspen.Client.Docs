# SecureIdentity

Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de un archivo de texto cifrado donde previamente se han ingresdado las credenciales de acceso.

## ¿Cómo generar el archivo y cifrar su información?

```c#
var identity = new SecureIdentity("YourApiKey", "YourApiSecret");
string fileName = @"C:\Temp\MySecureFile.bin";
identity.Encrypt().SaveTo(fileName)
```

## ¿Cómo procesar la inforfmación del archivo cifrado?

```c#
string fileName = @"C:\Temp\MySecureFile.bin";
var identity = SecureIdentity.FromFile(fileName);
```

 Para asociar los valores del ApiKey y el ApiSecret [registre la instancia para ser utilizada como extensión](ServiceLocator.md).

<div class="admonition warning">
   <p class="first admonition-title">Atención</p>
   <p class="last">Los datos protegidos están asociados con el contexto de la máquina donde se guardaron. Cualquier proceso que se ejecute en la computadora puede desproteger estos datos, por lo que este archivo dejará de funcionar si se lleva o intenta utilizar desde otra máquina.</p>
</div>


## Vea también

- [EnvironmentIdentity](EnvironmentIdentity.md)

- [RegistryIdentity](RegistryIdentity.md)

- [HardCodeIdentity](HardCodeIdentity.md)

- [AppConfigIdentity](AppConfigIdentity.md)