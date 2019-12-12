# IAppIdentity

Define la información de identidad de una aplicación para autenticar las solicitudes al servicio Aspen.

> Estos valores son proporcionados por Evertec Colombia a través del correo electrónico configurado como responsable del ApiKey. Recuerde que este correo electrónico es de un solo uso por lo que es conveniente guardar de forma segura estos valores al recibirlos.

```c#
public interface IAppIdentity
{
	string ApiKey { get; }
	string ApiSecret { get; }
}
```

Donde:

- **ApiKey** => Corresponde con el valor del ApiKey entregado a su entidad a través del correo electrónico de forma privada y segura.

- **ApiSecret** => Corresponde con el valor del ApiSecret ([una cadena altamente entrópica](https://es.wikipedia.org/wiki/Entrop%C3%ADa_(computaci%C3%B3n))) entregado a su entidad a través del correo electrónico de forma privada y segura.

## Vea también

- [EnvironmentIdentity](EnvironmentIdentity.md)

- [RegistryIdentity](RegistryIdentity.md)

- [AppConfigIdentity](AppConfigIdentity.md)

- [HardCodeIdentity](HardCodeIdentity.md)

- [SecureIdentity](SecureIdentity.md)