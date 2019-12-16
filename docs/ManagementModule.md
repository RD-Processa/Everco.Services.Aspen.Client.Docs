# Módulo de administración

Comprende las operaciones soportadas para proporcionar y gestionar la información relacionada con un usuario/tarjetahabiente/cliente.

## Consultar cuentas registradas

Obtiene la información de las cuentas registradas por un usuario/tarjetahabiente/cliente para transferencia de saldos.

```c#
// Información del usuario/tarjetahabiente/cliente que se desea consultar.
string userDocType = "CC";
string userDocNumber = "0000000000";

client.Management.GetTransferAccounts(docType, docNumber);
```

El resultado de la consulta será una lista de elementos representados por la entidad `TransferAccountInfo` asi:

![Preview](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/ManagementTransferAccountsExample.png?raw=true)

## Registrar cuenta para transferencias

Vincula la información de una cuenta de un tarjetahabiente a la lista de cuentas registradas para transferencia de fondos de un usuario.

**Utilizando el número de cuenta a registrar**

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

client.Management.LinkTransferAccount(userDocType, userDocNumber, linkTransferAccountInfo);
```

**Utilizando el número de documento asociado con la cuenta a registrar**

```c#
// Información del usuario que registra la cuenta.
string userDocType = "CC";
string userDocNumber = "0000000000";

// Información del usuario/cuenta que se desea registrar.
string cardHolderDocType = "CC";
string cardHolderDocNumber = "0000000001";

client.Management.LinkTransferAccount(userDocType, userDocNumber, cardHolderDocType, cardHolderDocNumber);
``` 

## Eliminar cuenta registrada

**Utilizando el alias del registro**

Desvincula la información de una cuenta de la lista de cuentas registradas para transferencias de un cliente, usando el alias asociado en el momento del registro:

```c#

// Alias que se utilizó en el registro
string accountAlias = "Luke Marshall";

// Información del usuario que registró la cuenta.
string userDocType = "CC";
string userDocNumber = "0000000000";

client.Management.UnlinkTransferAccount(userDocType, userDocNumber, accountAlias);
``

**Utilizando la información del titular de la cuenta registrada**

Desvincula la información de una cuenta de la lista de cuentas registradas para transferencias de un cliente, usando el tipo y número de docuento del titular de la cuenta registrada:

```c#
// Información del usuario que registró la cuenta.
string userDocType = "CC";
string userDocNumber = "0000000000";

// Información del usuario/cuenta que se registró.
string cardHolderDocType = "CC";
string cardHolderDocNumber = "0000000001";

client.Management.UnlinkTransferAccount(userDocType, userDocNumber, cardHolderDocType, cardHolderDocNumber);
```
