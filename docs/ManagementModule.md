# Módulo de Administración

Comprende las operaciones soportadas para proporcionar y gestionar la información relacionada con un usuario/tarjetahabiente/cliente.

## Administración de cuentas para transferencias

### Consultar las cuentas registradas de un usuario/tarjetahabiente/cliente

Obtiene la información de las cuentas registradas por un usuario para transferencia de saldos.

```c#
// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

// Información del usuario/tarjetahabiente/cliente que se desea consultar.
string userDocType = "CC";
string userDocNumber = "0000000000";

client.Management.GetTransferAccounts(docType, docNumber);
```

El resultado de la consulta será una lista de elementos representados por la entidad `TransferAccountInfo` asi:

![Preview](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/ManagementTransferAccountsExample.png?raw=true)

### Registrar una cuenta para transferencias

Vincula la información de una cuenta de un tarjetahabiente a la lista de cuentas registradas para transferencia de fondos de un usuario.

#### Utilizando el número de cuenta a registrar

```c#
// Información del usuario que registra la cuenta.
string userDocType = "CC";
string userDocNumber = "0000000000";

// Información de la cuenta que se desea registrar.
string cardHolderDocType = "CC";
string cardHolderDocNumber = "0000000001";

// Nombre con el que se distingue la cuenta en la lista.
string accountAlias = "Luke Marshall";
string accountNumber = "0000000000000000";

var linkTransferAccountInfo = new LinkTransferAccountInfo(
  cardHolderDocType,
  cardHolderDocNumber,
  accountAlias,
  accountNumber);

// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Management.LinkTransferAccount(userDocType, userDocNumber, linkTransferAccountInfo);
```

#### Utilizando el número de documento asociado con la cuenta a registrar

```c#
// Información del usuario que registra la cuenta.
string userDocType = "CC";
string userDocNumber = "0000000000";

// Información del usuario/cuenta que se desea registrar.
string cardHolderDocType = "CC";
string cardHolderDocNumber = "0000000001";

// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Management.LinkTransferAccount(userDocType, userDocNumber, cardHolderDocType, cardHolderDocNumber);
``` 

### Eliminar una cuenta registrada

#### Utilizando el alias del registro

Desvincula la información de una cuenta de la lista de cuentas registradas para transferencias de un cliente, usando el alias asociado en el momento del registro:

```c#

// Alias que se utilizó en el registro
string accountAlias = "Luke Marshall";

// Información del usuario que registró la cuenta.
string userDocType = "CC";
string userDocNumber = "0000000000";

// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Management.UnlinkTransferAccount(userDocType, userDocNumber, accountAlias);
```

#### Usando la información del titular de la cuenta registrada

Utilizando el número de documento asociado con la cuenta registrada.

```c#
// Información del usuario que registró la cuenta.
string userDocType = "CC";
string userDocNumber = "0000000000";

// Información del usuario/cuenta que se registró.
string cardHolderDocType = "CC";
string cardHolderDocNumber = "0000000001";

// Este código se debería ejecutar una sola vez y conservar la referencia a la instancia del cliente.
var client = AutonomousApp.Initialize()
  .WithDefaults()
  .Authenticate()
  .GetClient();

client.Management.UnlinkTransferAccount(userDocType, userDocNumber, cardHolderDocType, cardHolderDocNumber);
```
