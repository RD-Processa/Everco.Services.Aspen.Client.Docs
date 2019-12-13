# Módulo de operaciones dinámicas

Algunas operaciones en Aspen son resueltas por sistemas externos por lo que la URL de la operación dependerá de un parámetro. Este tipo de operaciones se denominan en Aspen `endpoints dinámicos`. En estos casos el cliente de Aspen no tiene una implementación definida para cada operación; en su lugar expone métodos que se utilizan como __una pasarela de información__ que procesa datos en crudo de entrada y de salida.

Cada operación expuesta en el cliente, esta asociada con el [método HTTP (verbo)](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods) definido en la parametrización del `endpoint dinámico`. Esta información le será entregada por Evertec, pero al ser una operación __separada__ de Aspen, el cliente simplemente actuará como
intermediario para enviar la información requerida y procesar los datos de respuesta, manteniendo el mismo manejo del [código de estado HTTP](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) y generando excepciones de tipo [AspenException](AspenException.md) para respuestas [fuera del rango (2xx)](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

## Ejemplo general

Para describir estas operaciones, supongamos como ejemplo una [operación CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) para una entidad llamada `Person`, cuyas operaciones están expuestas en el `endpoint dinámico` con la URL https://localhost/api/ext/demo/person

Supongamos tambien que la clase `Person` tiene las propiedades `LastName`, `FirstName` y `Number`.

```c#
public class Person
{
  public Person()
  {
  }

  public Person(int number, string firstName, string lastName)
  {
      this.Number = number;
      this.FirstName = firstName;
      this.LastName = lastName;
  }

  public string FirstName { get; set; }
  public string LastName { get; set; }
  public int Number { get; set; }
}
```

### Agregar una persona a través del método POST

Supongamos que para esta operación se requieren los valores de `LastName`, `FirstName` y `Number`. Podríamos invocar la operación así:

```c#
var request = new Person(123, “juan”, “perez”);
client.Post<Person>(request);
```

Utilizaremos la sobrecarga que no retorna un valor. En su lugar, esta sobrecarga generaría una excepción del tipo [AspenException](AspenException.md) si la operación retornará un código diferente a los del grupo (2xx).

### Actualizar una persona a través del método PUT

```c#
var request = new Person(123, “juanito”, “perez”);
client.Put<Person>(request);
``````

Utilizaremos la sobrecarga que no retorna un valor. En su lugar, esta sobrecarga genera una excepción del tipo [AspenException](AspenException.md) si la operación retornará un código diferente a los del grupo (2xx).

### Obtener la lista de personas a través del método GET

```c#
var response = client.Get<List<Person>>($”/demo/person”);
```

Utilizaremos la sobrecarga que retorna un valor del tipo especificado en el parámetro.

### Eliminar una persona a través del método DELETE

```c#
client.Delete($”/demo/person/id/123”);
```

Utilizaremos la sobrecarga que no retorna un valor. En su lugar, esta sobrecarga generaría una excepción del tipo [AspenException](AspenException.md) si la operación retornará un código diferente a los del grupo (2xx).

## Operaciones disponibles

### GET

Envia una solicitud al servicio Aspen, utilizando el verbo [Get](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

```c#
// Invoca el verbo GET en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
var response = client.Dynamics.Get<MyResponse>("ResourceName");
```

### POST

Envia una solicitud al servicio Aspen, utilizando el verbo [Post](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

```c#
// Invoca el verbo POST en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
var request = new MyRequest("MyValue1");
var response = client.Dynamics.Post<MyRequest,MyResponse>("ResourceName", request);
```

### PUT

Envia una solicitud al servicio Aspen, utilizando el verbo [Put](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

```c#
// Invoca el verbo PUT en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
var request = new MyRequest("MyValue1");
var response = client.Dynamics.Put<MyRequest,MyResponse>("ResourceName", request);
```

### DELETE

Envia una solicitud al servicio Aspen, utilizando el verbo [Delete](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

```c#
// Invoca el verbo DELETE en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
client.Dynamics.Delete("ResourceName");
```
