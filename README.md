# MARCO CONCEPTUAL

### Tarea 1
### ¿Qué es una API-Rest?
Una Api-Rest es una interfaz de programación de aplicaciones que permite la interacción de datos entre sistemas informaticos de una forma estandarizada, atravez de internet (IBM, 2026)

### ¿Qué significa que una Api sea Rest?
REST significa Representational State Transfer (Transferencia de Estado Representacional). No es un lenguaje de programación ni un protocolo, es un estilo arquitectónico para diseñar servicios que permiten la comunicación entre aplicaciones a través de la web. Normalmente el método usado es HTTP (GET, POST, PUT, PATCH, DELETE)(IBM,2026)

### ¿Qué es un recurso y qué es un endpoint?
Un recurso es la información, objeto o entidad que una API pone a disposición. Puede representar, por ejemplo, un usuario, un producto, una factura, un documento o una colección de datos.
IBM define los recursos de una API como los objetos o conjuntos de datos que esta proporciona.
Un endpoint, por otro lado, es la ubicación específica a la que una aplicación envía una solicitud para acceder a un recurso o ejecutar una operación. Normalmente se representa mediante una URL.

### Ejemplo de una aplicación que uses a diario y que dependa de APIs
Un ejemplo sencillo es una aplicación de mensajería como WhatsApp.
Cuando el usuario abre una conversación, envía un mensaje, descarga una fotografía o consulta determinada información, la aplicación necesita comunicarse con servidores remotos. Esa comunicación puede realizarse mediante APIs.

### Fuentes consultadas: 
https://www.ibm.com/mx-es/think/topics/rest-apis

https://www.ibm.com/docs/es/integration-bus/10.0.0?topic=apis-rest

### Tarea 2
### Métodos HTTP

| Método | Operación CRUD | Qué hace |
|--------|----------------|----------|
| GET | Leer | Consulta u obtiene uno o varios recursos. |
| POST | Crear | Crea un nuevo recurso enviando datos al servidor. |
| PUT | Actualizar | Actualiza o reemplaza completamente un recurso existente. |
| PATCH | Actualizar | Actualiza parcialmente un recurso existente. |
| DELETE | Eliminar | Elimina un recurso existente. |

### Tarea 3
### Códigos de estado
Los códigos HTTP se dividen en cinco familias según el tipo de respuesta que da el servidor. IBM y MDN los clasifican de esta forma:

| Familia | Qué significa | Ejemplo |
|---------|----------------|---------|
| 1xx | Respuestas informativas. La solicitud fue recibida y el proceso continúa. | `100 Continue`: el servidor indica que el cliente puede continuar enviando la solicitud. |
| 2xx | La solicitud fue procesada correctamente. | `200 OK`: la petición se realizó con éxito. |
| 3xx | Indican una redirección. El cliente debe ir a otra dirección o realizar otra acción. | `301 Moved Permanently`: el recurso fue movido de forma permanente a otra URL. |
| 4xx | Error del cliente. Hay algún problema en la solicitud enviada. | `404 Not Found`: el recurso solicitado no fue encontrado. |
| 5xx | Error del servidor. La solicitud puede ser válida, pero el servidor tiene un problema para procesarla. | `500 Internal Server Error`: ocurrió un error interno en el servidor. |

#### ¿Por qué se separan los errores 4xx de los 5xx? ¿Qué cambia entre unos y otros desde el punto de vista de quién tiene la culpa?

IBM describe los códigos 4xx como errores relacionados con la solicitud del cliente y los 5xx como errores producidos del lado del servidor (IBM, 2026).
La diferencia importante entre 4xx y 5xx es quién debe solucionar el problema.
En un error 4xx, normalmente el problema está del lado del cliente. Por ejemplo, puede estar solicitando una dirección que no existe, enviando información incorrecta o intentando acceder sin permisos.

En cambio, un error 5xx significa que el problema está del lado del servidor. El cliente hizo una petición que el servidor recibió, pero este no pudo procesarla correctamente (IBM,2026)

