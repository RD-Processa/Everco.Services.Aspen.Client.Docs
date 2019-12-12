## Mejores prácticas para mantener sus claves API seguras

Cuando use claves API en sus aplicaciones, tenga cuidado de mantenerlas seguras. Exponer públicamente sus credenciales puede hacer que su cuenta se vea comprometida, lo que podría generar cargos inesperados. Para ayudar a mantener sus claves API seguras, se recomienda seguir algunas prácticas de la industria:

- No incrustar claves API directamente en el código. Las claves API que están incrustadas en el código pueden exponerse accidentalmente al público. Por ejemplo, puede olvidar eliminar las claves del código en su repositorio de código fuente. En lugar de incrustar sus claves API en sus aplicaciones, almacénelas en variables de entorno o en archivos fuera del código fuente de su aplicación.

- No almacenar claves API en archivos dentro del código fuente de su aplicación. Si almacena claves API en archivos, mantenga los archivos fuera del código fuente de su aplicación para asegurarse de que sus claves no terminen en su sistema de control de código fuente. Esto es particularmente importante si utiliza un sistema de administración de código fuente público como GitHub.

- Configurar restricciones para su uso en la aplicación y la clave API. Al agregar restricciones, puede reducir el impacto de una clave API comprometida.

- Eliminar las claves API innecesarias para minimizar la exposición a los ataques.

- Reciclar sus claves API periódicamente. Puede solicitar la generación de claves API en cualquier momento. Luego, actualice sus aplicaciones para usar las claves recién generadas. Sus claves antiguas dejaran de funcionar luego de que sus aplicaciones estén listas para utilizar las claves de reemplazo.

- Usar una clave API por cada ambiente. De esta forma mantiene control de los datos a los que se está accediendo en cada ambiente. No es lo mismo que se comprometa una clave en un ambiente de pruebas (donde los datos están despersonalizados y muchas veces son ficticios), a que se comprometa una clave en ambiente de producción donde los datos son reales. 

- Revisar su código antes de publicarlo públicamente. Asegúrese de que su código no contenga claves API ni ninguna otra información privada antes de hacer que su código esté disponible públicamente.
