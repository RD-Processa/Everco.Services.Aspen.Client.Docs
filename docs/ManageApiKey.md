## ¿Por qué necesito usar claves de API?

Las claves de API identifican al proyecto (la aplicación o el sitio) que realiza la llamada a la API. Ayudan a Identificar a la aplicación o proyecto que hace uso del API y se generan para el proyecto que realiza la llamada.  Su uso puede restringirse a un entorno específico o una aplicación específica.

Dado que identifican al proyecto que las usa, las claves de API permiten que la información se asocie con ese proyecto y que se rechace llamadas de otros proyectos que no tienen acceso o que no se habilitaron para el uso de la API o de la operación (método) en la API.

## Mejores prácticas para mantener sus claves API seguras

Cuando use claves API en sus aplicaciones, tenga cuidado de mantenerlas seguras. Exponer públicamente sus credenciales puede hacer que su cuenta se vea comprometida, lo que podría generar cargos inesperados. Para ayudar a mantener sus claves API seguras, se recomienda seguir algunas prácticas de la industria:

- No incrustar claves API directamente en el código. Las claves API que están incrustadas en el código pueden exponerse accidentalmente al público. Por ejemplo, puede olvidar eliminar las claves del código en su repositorio de código fuente. En lugar de incrustar sus claves API en sus aplicaciones, almacénelas en variables de entorno o en archivos fuera del código fuente de su aplicación.

- No almacenar claves API en archivos dentro del código fuente de su aplicación. Si almacena claves API en archivos, mantenga los archivos fuera del código fuente de su aplicación para asegurarse de que sus claves no terminen en su sistema de control de código fuente. Esto es particularmente importante si utiliza un sistema de administración de código fuente público como GitHub.

- Configurar restricciones para su uso en la aplicación y la clave API. Al agregar restricciones, puede reducir el impacto de una clave API comprometida.

- Eliminar las claves API innecesarias para minimizar la exposición a los ataques.

- Reciclar sus claves API periódicamente. Puede solicitar la generación de claves API en cualquier momento. Luego, actualice sus aplicaciones para usar las claves recién generadas. Sus claves antiguas dejaran de funcionar luego de que sus aplicaciones estén listas para utilizar las claves de reemplazo.

- Usar una clave API por cada ambiente. De esta forma mantiene control de los datos a los que se está accediendo en cada ambiente. No es lo mismo que se comprometa una clave en un ambiente de pruebas (donde los datos están despersonalizados y muchas veces son ficticios), a que se comprometa una clave en ambiente de producción donde los datos son reales. 

- Revisar su código antes de publicarlo públicamente. Asegúrese de que su código no contenga claves API ni ninguna otra información privada antes de hacer que su código esté disponible públicamente.

El cliente de Aspen define la interfaz IAppIdentity e implementa las clases EnvironmentIdentity, RegistryIdentity, AppConfigIdentity, HardCodeIdentity y SecureIdentity para tal fin. Si ninguna de estas clases satisface sus necesidades, podría hacer su propia implementación de la interfaz IAppIdentity y reemplazar el componente en tiempo de ejecución.

<div class="admonition info">
   <p class="first admonition-title">Nota</p>
   <p class="last">Por defecto, el cliente de Aspen utiliza la clase <a href="../EnvironmentIdentity">EnvironmentIdentity</a> para obtener el valor de las credenciales de conexión.</p>
</div>

## [IAppIdentity](IAppIdentity.md)

-  Define la información de identidad de una aplicación para autenticar las solicitudes al servicio Aspen.

## [EnvironmentIdentity](EnvironmentIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de variables de ambiente del sistema.
 
## [RegistryIdentity](RegistryIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de la configuración en el registro de Windows.

## [AppConfigIdentity](AppConfigIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de la entradas de configuración en la sección appSettings de un archivo de configuración XML.

## [HardCodeIdentity](HardCodeIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de los valores proporcionados en el constructor de la clase. NO SE RECOMIENDA EL USO DE ESTA CLASE. Se provee solo con fines de pruebas de concepto.

## [SecureIdentity](SecureIdentity.md)

- Obtiene la información que se utiliza para autenticar la solicitud en el servicio Aspen a partir de un archivo de texto cifrado.
