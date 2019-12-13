# UnixEpochGenerator

Implementa un generador de épocas o marcas de tiempo Unix (número de segundos que han transcurrido desde 1970-01-01T00:00:00Z)

```c#
public interface IEpochGenerator
{
  double GetSeconds();
}

public class UnixEpochGenerator : IEpochGenerator
{
  public double GetSeconds() => DateTimeOffset.Now.ToUnixTimeSeconds();
}
```

También podria hacer su propia implementación de la interfaz `IEpochGenerator` y registrar el uso de su clase así:

```c#
var epoch = new MyEpochGenerator();
```
