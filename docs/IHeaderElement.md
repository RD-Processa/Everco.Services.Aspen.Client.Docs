# IHeaderElement

Establece la instancia que se debe utilizar para establecer los nombres que se utilizan en las cabeceras personalizadas de las solicitudes hacia el servicio Aspen.

**IHeaderElement.cs**

```c#
public interface IHeaderElement
{
  string PayloadHeaderName { get; }
  string ApiKeyHeaderName { get; }
  string ApiVersionHeaderName { get; }
  string DeviceInfoHeaderName { get; }
}
```

También podria hacer su propia implementación de la interfaz `IHeaderElement` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterRequestHeaderNames(new MyHeaderElement());
```
