# IPayloadClaimElement

Establece la instancia que se debe utilizar para establecer los nombres de las reclamaciones que se utilizan en la carga útil (Payload) de una solicitud hacia el servicio Aspen.

**IPayloadClaimElement.cs**

```c#
public interface IPayloadClaimElement
{
  string DeviceIdClaimName { get; }
  string DocNumberClaimName { get; }
  string DocTypeClaimName { get; }
  string EpochClaimName { get; }
  string NonceClaimName { get; }
  string PasswordClaimName { get; }
  string TokenClaimName { get; }
  string UsernameClaimName { get; }
}
```

También podria hacer su propia implementación de la interfaz `IPayloadClaimElement` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterPayloadClaimNames(new MyPayloadClaimElement());
```