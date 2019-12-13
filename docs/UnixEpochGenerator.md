# UnixEpochGenerator

Implementa un generador de épocas o marcas de tiempo Unix (número de segundos que han transcurrido desde 1970-01-01T00:00:00Z)

**IEpochGenerator.cs**

```c#
public interface IEpochGenerator
{
  double GetSeconds();
}
```

También podria hacer su propia implementación de la interfaz `IEpochGenerator` y registrar el uso de su clase así:

MyEpochGenerator.cs

```c#
ServiceLocator.Instance.RegisterEpochGenerator(new MyEpochGenerator());
```
