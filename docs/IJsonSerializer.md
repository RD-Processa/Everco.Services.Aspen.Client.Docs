# IJsonSerializer

Define las operaciones que se utilizan para serializar la información enviada y generada para las solicitudes hacia/desde el servicio Aspen.

**IJsonSerializer.cs**

```c#
public interface IJsonSerializer
{
  T Deserialize<T>(string json);
  string Serialize(object obj);
}
```

También podria hacer su propia implementación de la interfaz `IJsonSerializer` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterJwtJsonSerializer(new MyJsonSerializer());
```