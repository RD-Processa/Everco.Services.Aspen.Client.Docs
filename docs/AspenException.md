# Control de errores

El cliente de Aspen, está preparado para propagar una excepción de tipo: `AspenException` cuando se recibe una respuesta fuera del rango de códigos de estado HTTP `2xx` desde el API del servicio. Esta clase se asegura de recopilar y proporcionar la información relevante de la respuesta HTTP.

Imaginemos con el siguiente ejemplo donde se intenta inicializar una instancia del cliente usando un **ApiKey** y un **ApiSecret** de un programa/aplicación desconocida.

```c#
try{
    var client = AutonomousApp.Initialize()
        .RoutingTo("http://localhost/api")
        .WithIdentity("InvalidApiKey", "InvalidApiSecret")
        .Authenticate()
        .GetClient();
}
catch(AspenException exception)
{

}
```

El resultado esperado debería ser una excepción de tipo `AspenException` ya que los valores que identifican a la aplicación, no son reconocidos por el sistema.

Accediendo a la variable `exception` podrá obtener los detalles del problema, así:

| Propiedad | Descripción |
|:-:|---|
| **Message** | Un mensaje personalizado que describirá el resultado de la operación; también incluye el identificador de evento con el formato: `EventId: (0000000)` que podría utilizar si necesita personalizar la respuesta. |
| **EventId** | Un identificador de evento emitido para la respuesta inválida del servicio. Puede encontrar mayor detalle al respecto de los identificadores de eventos en la sección **[Mensajes de respuesta](https://processa-aspen.readthedocs.io/en/latest/Responses/)** de la documentación funcional del servicio. |
| **StatusCode** | El código de estado de respuesta HTTP devuelto por el servicio. |
| **HelpLink** | El enlace al archivo de ayuda en línea, asociado con la respuesta generada por el servicio. |
| **DumpLink** | El enlace de la traza de seguimiento de la solicitud. Durante el procesamiento de una solicitud al API de Aspen, se escriben trazas de seguimiento como las entradas recibidas y comportamientos esperados que permitirán verificar la respuesta generada por el servicio. Esta información podría no estar disponible si las trazas están deshabilitadas en el servidor que aloja el API de Aspen. |

![AspenException](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/AspenException.png?raw=true)