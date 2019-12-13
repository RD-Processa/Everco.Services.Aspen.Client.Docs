# ILoggingProvider

Define la instancia que se debe utilizar para escribir la información de seguimiento (logging) generada localmente por la librería.

**ILoggingProvider.cs**

```c#
public interface ILoggingProvider
{
  void WriteDebug(string message);
  void WriteInfo(string message, object @object = null);
  void WriteError(Exception exception, string message = null);
}
```

También podria hacer su propia implementación de la interfaz `ILoggingProvider` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterLoggingProvider(new MyLoggingProvider());
```