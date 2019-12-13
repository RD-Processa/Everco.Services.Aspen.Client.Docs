# DefaultHeadersManager

Implementa las operaciones necesarias para establecer las cabeceras personalizadas requeridas por el servicio Aspen.

IHeadersManager.cs

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

DefaultHeadersManager.cs

```c#
public class DefaultHeadersManager : IHeadersManager
{
  public void AddApiKeyHeader(IRestRequest request, string apiKey)
  {
    request.AddHeader(ServiceLocator.Instance.RequestHeaderNames.ApiKeyHeaderName, apiKey);
  }

  public void AddApiVersionHeader(IRestRequest request, string apiVersion)
  {
    request.AddHeader(ServiceLocator.Instance.RequestHeaderNames.ApiVersionHeaderName, Version.Parse(apiVersion).ToString());
  }

  public void AddSignedPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret,
    string token)
  {
    Dictionary<string, object> payload = new Dictionary<string, object>();
    ServiceLocator.Instance.PayloadClaimsManager.AddNonceClaim(payload, ServiceLocator.Instance.NonceGenerator.GetNonce());
    ServiceLocator.Instance.PayloadClaimsManager.AddEpochClaim(payload, ServiceLocator.Instance.EpochGenerator.GetSeconds());
    ServiceLocator.Instance.PayloadClaimsManager.AddTokenClaim(payload, token);
    string jwt = jwtEncoder.Encode(payload, apiSecret);
    request.AddHeader(ServiceLocator.Instance.RequestHeaderNames.PayloadHeaderName, jwt);
  }

  public void AddSignedPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret,
    string token,
    string username)
  {
    IDeviceInfo deviceInfo = CacheStore.GetDeviceInfo() ?? DeviceInfo.Current;
    Dictionary<string, object> payload = new Dictionary<string, object>();
    ServiceLocator.Instance.PayloadClaimsManager.AddNonceClaim(payload, ServiceLocator.Instance.NonceGenerator.GetNonce());
    ServiceLocator.Instance.PayloadClaimsManager.AddEpochClaim(payload, ServiceLocator.Instance.EpochGenerator.GetSeconds());
    ServiceLocator.Instance.PayloadClaimsManager.AddTokenClaim(payload, token);
    ServiceLocator.Instance.PayloadClaimsManager.AddUsernameClaim(payload, username);
    ServiceLocator.Instance.PayloadClaimsManager.AddDeviceIdClaim(payload, deviceInfo.DeviceId);
    string jwt = jwtEncoder.Encode(payload, apiSecret);
    request.AddHeader(ServiceLocator.Instance.RequestHeaderNames.PayloadHeaderName, jwt);
  }

  public void AddSigninPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret)
  {
    Dictionary<string, object> payload = new Dictionary<string, object>();
    ServiceLocator.Instance.PayloadClaimsManager.AddNonceClaim(payload, ServiceLocator.Instance.NonceGenerator.GetNonce());
    ServiceLocator.Instance.PayloadClaimsManager.AddEpochClaim(payload, ServiceLocator.Instance.EpochGenerator.GetSeconds());
    string jwt = jwtEncoder.Encode(payload, apiSecret);
    request.AddHeader(ServiceLocator.Instance.RequestHeaderNames.PayloadHeaderName, jwt);
  }

  public void AddSigninPayloadHeader(
    IRestRequest request,
    IJwtEncoder jwtEncoder,
    string apiSecret,
    IUserIdentity userIdentity)
  {
    IDeviceInfo deviceInfo = userIdentity.Device ?? CacheStore.GetDeviceInfo() ?? DeviceInfo.Current;
    request.AddHeader(ServiceLocator.Instance.RequestHeaderNames.DeviceInfoHeaderName, deviceInfo.ToJson());
    CacheStore.SetDeviceInfo(deviceInfo);

    Dictionary<string, object> payload = new Dictionary<string, object>();
    ServiceLocator.Instance.PayloadClaimsManager.AddNonceClaim(payload, ServiceLocator.Instance.NonceGenerator.GetNonce());
    ServiceLocator.Instance.PayloadClaimsManager.AddEpochClaim(payload, ServiceLocator.Instance.EpochGenerator.GetSeconds());
    ServiceLocator.Instance.PayloadClaimsManager.AddDocTypeClaim(payload, userIdentity.DocType);
    ServiceLocator.Instance.PayloadClaimsManager.AddDocNumberClaim(payload, userIdentity.DocNumber);
    ServiceLocator.Instance.PayloadClaimsManager.AddPasswordClaim(payload, userIdentity.Password);
    ServiceLocator.Instance.PayloadClaimsManager.AddDeviceIdClaim(payload, deviceInfo.DeviceId);
    string jwt = jwtEncoder.Encode(payload, apiSecret);
    request.AddHeader(ServiceLocator.Instance.RequestHeaderNames.PayloadHeaderName, jwt);
  }
}
```

También podria hacer su propia implementación de la interfaz `IHeadersManager` y registrar el uso de su clase así:

MyEpochGenerator.cs

```c#
ServiceLocator.Instance.RegisterEpochGenerator(new MyRegisterHeadersManager());
```