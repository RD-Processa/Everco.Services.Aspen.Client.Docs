# Módulo de configuraciones

Comprende las operaciones soportadas para acceder a las entidades de información relacionadas con parametrización del sistema, como pueden ser los tipos de documentos reconocidos, tipos de transacción, valores de configuración, etc para utilizar en su proyecto/aplicación.

## Tipos de documentos

Obtiene la lista de tipos de documento reconocidos por el sistema Aspen.

```c#
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Settings.GetDocTypes();
```

El resultado de la consulta será una lista de elementos representados por la entidad `DocTypeInfo` asi:

![GetDocTypes](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsDocTypesExample.png?raw=true)
