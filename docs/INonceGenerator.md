# INonceGenerator

Define un generador de números arbitrarios de un solo uso.

**INonceGenerator.cs**

```c#
public interface INonceGenerator
{
  string GetNonce();
}
```

También podria hacer su propia implementación de la interfaz `INonceGenerator` y registrar el uso de su clase así:

```c#
ServiceLocator.Instance.RegisterNonceGenerator(new MyNonceGenerator());
```
