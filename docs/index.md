# Introducción

El cliente de Aspen es una librería que facilita la conexión con el servicio [Aspen](https://processa-aspen.readthedocs.io/) de Evertec Colombia.

Su motivación principal es permitir  a los desarrolladores crear una aplicación con unas pocas líneas de código a través del uso de una librería lista para los ambientes producción, facilitando la depuración y simplificando el acceso al servicio.

```c#

// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client =  AutonomousApp.Initialize()
  .RoutingTo("https://locahost")
  .WithIdentity("YourApyKey", "YourApiSecret")
  .Authenticate()
  .GetClient();
```

<br/>

<a href="Quickstart" class="btn btn-neutral float-right" title="Guia rápida">Ir a la guia rápida de uso <span class="icon icon-circle-arrow-right"></span></a>

<p>&nbsp;</p>