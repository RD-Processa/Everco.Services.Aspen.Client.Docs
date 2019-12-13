# IWebProxy

Establece la instancia que se debe utilizar como la configuración del servidor Proxy que permite establecer la comunicación hacia el servicio Aspen.

```c#
public interface IWebProxy
{
  ICredentials Credentials { get; set; }
  Uri GetProxy(Uri destination);
  bool IsBypassed(Uri host);
} 
```

También podria hacer su propia implementación de la interfaz `IWebProxy` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterWebProxy(new MyWebProxy());
```
