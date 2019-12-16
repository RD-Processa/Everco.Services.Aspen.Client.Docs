# Módulo de configuraciones

Comprende las operaciones soportadas para acceder a las entidades de información relacionadas con parametrización del sistema, como pueden ser los tipos de documentos reconocidos, tipos de transacción, valores de configuración, etc para utilizar en su proyecto/aplicación.

## Consultar tipos de documentos

Obtiene la lista de tipos de documento reconocidos por el sistema Aspen.

```c#
client.Settings.GetDocTypes();
```

El resultado de la consulta será una lista de elementos representados por la entidad `DocTypeInfo` asi:

![DocTypeInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsDocTypesExample.png?raw=true)

## Consultar operadores de telefonía móvil

Un operador o proveedor de telefonía móvil es una compañía que proporciona servicios para los usuarios de teléfonos móviles. El servicio de Aspen facilita esta información para operaciones de recarga a celular.

```c#
client.Settings.GetCarriers();
```

El resultado de la consulta será una lista de elementos representados por la entidad `CarrierInfo` asi:

![CarrierInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsCarriersExample.png?raw=true)

## Consultar valores de recarga por operador de telefonía móvil

Por cada operador de telefonía configurado, se dispone de los valores permitidos para realizar recargas a celular. Si los valores no se ajustan a los que su proyecto/aplicación requiere, puede solicitar la personalización o configuración de nuevos valores.

```c#
client.Settings.GetTopUpValues();
```

El resultado de la consulta será una lista de elementos representados por la entidad `TopUpInfo` asi:

![TopUpInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsTopUpValuesExample.png?raw=true)

## Consultar tipos de transacción

Son los tipos de operaciones financieras soportadas para su aplicación.

```c#
client.Settings.GetTranTypes();
```

El resultado de la consulta será una lista de elementos representados por la entidad `TranTypeInfo` asi:

![TranTypeInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsTranTypesExample.png?raw=true)

## Consultar tipos de pagos

Son los tipos de pagos que se pueden realizar a una cuenta y que están soportados para la aplicación.

```c#
client.Settings.GetPaymentTypes();
```

El resultado de la consulta será una lista de elementos representados por la entidad `PaymentTypeInfo` asi:

![PaymentTypeInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/SettingsPaymentTypesExample.png?raw=true)
