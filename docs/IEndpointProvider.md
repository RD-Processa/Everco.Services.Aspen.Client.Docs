# IEndpointProvider

Define la Url base del servicio Aspen con el que se requiere conectar y el tiempo de espera para las respuestas.

```c#
public interface IEndpointProvider
{
	string Url { get; }
	TimeSpan Timeout { get; }
}
```
Donde:

- **Url** => Obtiene la URL a donde se envian las solicitudes del servicio Aspen.
- **Timeout** => Obtiene el tiempo de espera para las respuestas del servicio Aspen.

## Vea también

- [RegistryEndpoint](RegistryEndpoint.md)

- [EnvironmentEndpoint](EnvironmentEndpointmd)

- [AppConfigEndpoint](AppConfigEndpoint.md)
