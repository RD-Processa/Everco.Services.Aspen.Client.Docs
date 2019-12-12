# Operaciones habilitadas en el cliente de Aspen

Ahora conozcamos las operaciones soportadas por el cliente de Aspen. Hemos ordenado por módulos las funcionalidades que pueden ser aprovechadas por su proyecto/aplicación asi:

## Configuraciones

Comprende a las operaciones soportadas para acceder a entidades de información relacionadas con parametrización del sistema, como son los tipos de documentos conocidos, tipos de transacción y valores de configuración disponibles para usar en su proyecto/aplicación.






## Operaciones dinámicas

Una operación dinámica en el servicio ASPEN, representa un endpoint de tipo REST que se conecta con una cola de RabbitMQ para procesar una operación. Esto facilita la flexibilidad del sistema al exponer operaciones a partir de verbos http específicos (GET, POST, PUT, DELETE)

### GET

```c#
client.Dynamics.Get("")
``` 

### POST

### PUT

### DELETE
