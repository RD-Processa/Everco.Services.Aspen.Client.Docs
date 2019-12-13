# IPayloadClaimsManager

Establece la instancia que se debe utilizar para agregar las reclamaciones que se utilizan en la carga útil (Payload) de una solicitud hacia el servicio Aspen.

**IPayloadClaimsManager.cs**

```c#
public interface IPayloadClaimsManager
{
  void AddDeviceIdClaim(IDictionary<string, object> payload, string deviceId);
  void AddDocNumberClaim(IDictionary<string, object> payload, string docNumber);
  void AddDocTypeClaim(IDictionary<string, object> payload, string docType);
  void AddEpochClaim(IDictionary<string, object> payload, double epoch);
  void AddNonceClaim(IDictionary<string, object> payload, string nonce);
  void AddPasswordClaim(IDictionary<string, object> payload, string password);
  void AddTokenClaim(IDictionary<string, object> payload, string token);
  void AddUsernameClaim(IDictionary<string, object> payload, string username);
}
```

También podria hacer su propia implementación de la interfaz `IPayloadClaimsManager` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterPayloadClaimsManager(new MyPayloadClaimsManager());
```
