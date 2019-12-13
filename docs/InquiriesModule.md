# Módulo de consultas financieras

Comprende las consultas a los productos financieros (cuentas débito y cuentas crédito) de un usuario.

## Consultar productos financieros

Obtiene la información resumida de las cuentas o productos financieros asociados al usuario especificando por el tipo y número de documento. Cuando el usuario no tiene productos asociados, la respuesta será una lista vacía.

```c#

// Información del titular del producto financiero
string userDocType = "CC";
string userDocNumber = "0000000000";

client.Inquiries.GetAccounts(userDocType, userDocNumber);
```

El resultado de la consulta será una lista de elementos representados por la entidad `AccountInfo` asi:

![AccountInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/InquiriesAccountsExample.png?raw=true)

**Propiedades de una cuenta (List&lt;AccountProperty&gt;)**

Es un conjunto de propiedades o atributos que representan información relevante de la cuenta.

Campo | Descripción
:---: | -----------
Label | Nombre o etiqueta para visualizar el contenido del atributo en la interfaz de usuario.
Key | Identificador interno del atributo.
Value | Valor asociado con el atributo.







<div class="admonition warning">
   <p class="first admonition-title">Atención</p>
   <p class="last">El conjunto de propiedades o atributos de una cuenta variará de acuerdo con el sistema de información origen del producto.</p>
</div>

**Sistemas de información origen**

Proveen la información financiera relacionada con usuarios/tarjetahabientes/clientes. A diciembre de 2019 se tienen habilitados los siguientes sistemas:

Sistema | Descripción
:----: | -----------
Tup | El origen de la información es el sistema de administración de tarjetas débito **TUP**.
Bancor | El origen de la información es el sistema de administración de cartera **BANCOR**.

## Consultar saldos

Permite obtener los saldos (balances) detallados de un producto financiero.

```c#
// Información del titular del producto financiero
string userDocType = "CC";
string userDocNumber = "0000000000";

// Obtener la lista de cuentas del usuario/tarjetahabiente/cliente
var accounts = client.Inquiries.GetAccounts(userDocType, userDocNumber);

// Obtener el saldo de cada cuenta
foreach (var account in accounts)
{
    client.Inquiries.GetBalances(userDocType, userDocNumber, account.SourceAccountId);
}
```

El resultado de la consulta será una lista de elementos representados por la entidad `BalanceInfo` asi:

![BalanceInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/InquiriesBalancesExample.png?raw=true)

## Consultar movimientos

Obtiene la información de transacciones finacieras realizadas en una cuenta.

```c#
// Información del titular del producto financiero
string userDocType = "CC";
string userDocNumber = "0000000000";

// Obtener la lista de cuentas del usuario/tarjetahabiente/cliente
var accounts = client.Inquiries.GetAccounts(userDocType, userDocNumber);

// Obtener los movimientos de cada cuenta
foreach (var account in accounts)
{
    client.Inquiries.GetStatements(userDocType, userDocNumber, account.SourceAccountId);
}
```

El resultado de la consulta será una lista de elementos representados por la entidad `MiniStatementInfo` asi:

![MiniStatementInfo](https://github.com/RD-Processa/Everco.Services.Aspen.Client.Docs/blob/master/images/InquiriesStatementsExample.png?raw=true)
