# IHeadersManager

Define las operaciones necesarias para establecer las cabeceras personalizadas requeridas por el servicio Aspen.

**IHeadersManager.cs**

```c#
public interface IHeadersManager
{
  void AddApiKeyHeader(
    IRestRequest request,
    string apiKey);

  void AddApiVersionHeader(
    IRestRequest request,
    string apiVersion);

  void AddSignedPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret,
    string token);

  void AddSignedPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret,
    string token,
    string username);

  void AddSigninPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret);

  void AddSigninPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret,
    IUserIdentity userIdentity);
}
```

También podria hacer su propia implementación de la interfaz `IHeadersManager` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterHeadersManager(new MyHeadersManager());
```

