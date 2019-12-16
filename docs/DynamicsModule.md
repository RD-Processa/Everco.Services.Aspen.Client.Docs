# Módulo de operaciones dinámicas

Algunas operaciones en Aspen son resueltas por sistemas externos por lo que la URL de la operación dependerá de un parámetro. Este tipo de operaciones se denominan en Aspen `endpoints dinámicos`. En estos casos el cliente de Aspen no tiene una implementación definida para cada operación; en su lugar expone métodos que se utilizan como __una pasarela de información__ que procesa datos en crudo de entrada y de salida.

Cada operación expuesta en el cliente, esta asociada con el [método HTTP (verbo)](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods) definido en la parametrización del `endpoint dinámico`. Esta información le será entregada por Evertec, pero al ser una operación __separada__ de Aspen, el cliente simplemente actuará como
intermediario para enviar la información requerida y procesar los datos de respuesta, manteniendo el mismo manejo del [código de estado HTTP](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) y generando excepciones de tipo [AspenException](AspenException.md) para respuestas [fuera del rango (2xx)](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

## Veamos un ejemplo

Para describir estas operaciones, supongamos como ejemplo una [operación CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) para una entidad llamada `Person`, cuyas operaciones están expuestas en el `endpoint dinámico` con la URL `https://localhost/api/ext/demo/person`

Supongamos también que la clase `Person` tiene las propiedades `Id`, `LastName`, `FirstName`.

```c#
public class Person
{
  public Person()
  {
  }

  public Person(int id, string firstName, string lastName)
  {
      this.Id = id;
      this.FirstName = firstName;
      this.LastName = lastName;
  }

  public int Id { get; set; }
  public string FirstName { get; set; }
  public string LastName { get; set; }
}
```

## Operaciones disponibles

### GET

Envia una solicitud al servicio Aspen, utilizando el verbo **[Get](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)**

```c#
// Invoca el verbo GET en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
var response = client.Dynamics.Get<MyResponse>("ResourceName");

// Obtener la lista de personas a través del método GET
// Utilizaremos la sobrecarga que retorna un valor del tipo especificado en el parámetro.
var response = client.Dynamics.Get<List<Person>>("demo/person");

// Obtener la información de una persona a través del método GET
// Utilizaremos la sobrecarga que retorna un valor del tipo especificado en el parámetro.
var response = client.Dynamics.Get<Person>("demo/person/id/000");
```

### POST

Envia una solicitud al servicio Aspen, utilizando el verbo **[Post](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)**

```c#
// Invoca el verbo POST en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
var request = new MyRequest("MyValue1", "MyValue2");
var response = client.Dynamics.Post<MyRequest, MyResponse>("ResourceName", request);

// Agregar una persona a través del método POST
var request = new Person(123, "Juan", "Perez");

// Utilizaremos la sobrecarga que no retorna un valor. En su lugar, esta sobrecarga generaría una excepción del tipo AspenException  si la operación retornará un código diferente a los del grupo (2xx).
client.Dynamics.Post<Person>("demo/person", request);
```

### PUT

Envia una solicitud al servicio Aspen, utilizando el verbo **[Put](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)**

```c#
// Invoca el verbo PUT en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
var request = new MyRequest("NewValue1", "NewValue2");
var response = client.Dynamics.Put<MyRequest, MyResponse>("ResourceName", request);

// Actualizar una persona a través del método PUT
var request = new Person(123, "Juanito", "Perez");

// Utilizaremos la sobrecarga que no retorna un valor. En su lugar, esta sobrecarga genera una excepción del tipo AspenException si la operación retornará un código diferente a los del grupo (2xx).
client.Dynamics.Put<Person>("demo/person", request);
```

### DELETE

Envia una solicitud al servicio Aspen, utilizando el verbo **[Delete](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)**

```c#
// Invoca el verbo DELETE en el recurso y serializa la respuesta a un objeto de tipo MyResponse.
// ResourceName corresponde con el texto a la derecha de la palabra /ext/ en la URL de la documentación que Evertec le entregó.
// Supongamos que la URL completa entregada es: https://localhost/api/ext/demo/calc, para este ejemplo, ResourceName sería "demo/calc"
client.Dynamics.Delete("ResourceName");

// Eliminar una persona a través del método DELETE

// Utilizaremos la sobrecarga que no retorna un valor. En su lugar, esta sobrecarga generaría una excepción del tipo AspenException si la operación retornará un código diferente a los del grupo (2xx).
client.Dynamics.Delete("demo/person/id/000");
```

## ¿Y cuando el endpoint dinámico tiene parámetros en la URL?

La información entre corchetes en una URL se denomina **segmentos de URL** y aplican solo para operaciones específicas. Cuando aparezcan, deben ser reemplazados por sus valores correspondientes omitiendo los corchetes.

Imaginemos que tenemos un endpoint dinámico con la siguiente URL: `http://localhost/api/ext/demo/value/{value}` y se espera en el segmento `{value}` un valor que permita realizar la operación esperada. Como ejemplo se establecerá el valor: `123` en el segmento: `{value}` y la URL final sería: `http://localhost/api/operation/value/123`

Tenga en cuenta que debería generar la URL (resource) de acuerdo con las especificaciones entregadas por Evertec Colombia.

## Vea también

- [Conectar con Aspen](ManageApiKey.md#obtener-una-instancia-del-servicio)