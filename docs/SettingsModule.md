# Módulo de configuraciones

Comprende las operaciones soportadas para acceder a las entidades de información relacionadas con parametrización del sistema, como pueden ser los tipos de documentos reconocidos, tipos de transacción, valores de configuración, etc para utilizar en su proyecto/aplicación.

## Tipos de documentos

Obtiene la lista de tipos de documento reconocidos por el sistema Aspen.

```c#
// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Settings.GetDocTypes();
```

El resultado de la consulta será una lista de elementos representados por la entidad `DocTypeInfo` asi:

![DocTypeInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsDocTypesExample.png?raw=true)

## Operadores de telefonía móvil

Un operador o proveedor de telefonía móvil es una compañía que proporciona servicios para los usuarios de teléfonos móviles. El servicio de Aspen facilita esta información para operaciones de recarga a celular.

```c#
// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Settings.GetCarriers();
```

El resultado de la consulta será una lista de elementos representados por la entidad `CarrierInfo` asi:

![CarrierInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsCarriersExample.png?raw=true)

## Valores admitidos de recarga por operador

Por cada operador de telefonía configurado, se dispone de los valores permitidos para realizar recargas a celular. Si los valores no se ajustan a los que su proyecto/aplicación requiere, puede solicitar la personalización o configuración de nuevos valores.

```c#
// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Settings.GetTopUpValues();
```

El resultado de la consulta será una lista de elementos representados por la entidad `TopUpInfo` asi:

![TopUpInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsTopUpValuesExample.png?raw=true)

## Tipos de transacción

Son los tipos de operaciones financieras soportadas para su aplicación.

```c#
// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Settings.GetTranTypes();
```

El resultado de la consulta será una lista de elementos representados por la entidad `TranTypeInfo` asi:

![TranTypeInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsTranTypesExample.png?raw=true)

## Tipos de pagos

Son los tipos de pagos que se pueden realizar a una cuenta y que están soportados para la aplicación.

```c#
// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Settings.GetPaymentTypes();
```

El resultado de la consulta será una lista de elementos representados por la entidad `PaymentTypeInfo` asi:

![PaymentTypeInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsPaymentTypesExample.png?raw=true)
