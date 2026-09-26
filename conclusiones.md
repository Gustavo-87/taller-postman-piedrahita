## Tarea 9
## Idempotencia

Un método HTTP es idempotente cuando repetir la misma petición varias veces produce el mismo resultado final.

En la prueba con PUT, envié varias veces la misma actualización y el resultado se mantuvo igual.

Con POST, cada ejecución representa una nueva creación, por eso POST no se considera idempotente.

De los métodos trabajados:
- GET: idempotente
- PUT: idempotente
- PATCH: no se garantiza que sea idempotente
- DELETE: idempotente
- POST: no idempotente

## Tarea 9
## Cabeceras de la respuesta

### Content-Type
Indica el tipo de contenido que devuelve el servidor.

En este caso la respuesta es JSON, por eso aparece algo relacionado con:

`application/json`

Esta cabecera es importante porque permite saber cómo debe interpretarse la respuesta.

### Cache-Control
Indica cómo puede almacenarse temporalmente la respuesta en caché.

Sirve para controlar si una respuesta puede reutilizarse o si debe solicitarse nuevamente al servidor.

### Date
Indica la fecha y hora en la que el servidor generó la respuesta.

Sirve como referencia para saber cuándo fue enviada la respuesta.

### ¿Por qué es importante Content-Type?

Porque permite verificar que la API esté devolviendo la información en el formato esperado.

## Tarea 10 - Prueba de límites

- Id más alto que devuelve 200: 100
- Primer id que devuelve 404: 101

### Hallazgo

El recurso con id 100 existe y devuelve 200 OK, mientras que el id 101 ya no existe y devuelve 404 Not Found.

### ¿Cómo se llama este tipo de prueba?

Se llama prueba de valores límite.

### ¿Por qué los defectos se concentran ahí?

Porque los errores suelen aparecer cerca de los valores mínimos y máximos permitidos.

En este caso, el límite está entre 100 y 101, por eso probar esos valores ayuda a comprobar si la API maneja correctamente el cambio entre un recurso existente y uno inexistente.

## Tarea 11 - Exploración de otros recursos

Probé otros recursos diferentes a "/posts".

### Recurso 1 - /users

La petición: "GET /users" devolvió una colección de usuarios.

### Recurso 2 - /comments

La petición: "GET /comments" devolvió una colección de comentarios.

### Ruta anidada

También probé: "GET /posts/1/comments" Esta ruta devuelve los comentarios relacionados con el post que tiene id 1.

### ¿Cómo deduje la estructura de las URL?

Observé que la API organiza la información por recursos.

Por ejemplo:

- "/users" representa usuarios.
- "/comments" representa comentarios.
- "/posts/1/comments" representa los comentarios que pertenecen al post con id 1.

## Tarea 12 - Primera prueba automática

Primero configuré la prueba para esperar un código 200 y la prueba pasó correctamente.

Después cambié el valor esperado a 201 y la prueba falló.

### ¿Por qué es importante ver una prueba fallar antes de confiar en ella?

Porque así comprobamos que la prueba realmente detecta cuando el resultado no es el esperado.

Si una prueba siempre aparece en verde, incluso cuando ponemos un valor incorrecto, entonces no estaría verificando correctamente la respuesta.

### 1. ¿Qué le faltaría a la tabla de la Fase 2 para ser un plan de pruebas formal?

La tabla ya tiene la petición, el resultado esperado y el resultado obtenido, pero para ser un plan de pruebas formal le faltarían más datos, por ejemplo:

- El objetivo de la prueba.
- Los pasos para ejecutarla.
- Los datos de entrada.
- Las condiciones previas.
- El resultado esperado detallado.
- El estado final de la prueba, por ejemplo si pasó o falló.

Con esa información, otra persona podría repetir la prueba de forma clara y obtener el mismo resultado.

### 2. ¿Por qué un 404 puede ser una buena noticia y un 200 puede ser un defecto?

Un código 404 puede ser una buena noticia cuando es exactamente el resultado que esperábamos.

Por ejemplo, si consultamos un recurso que no existe, lo correcto es recibir un 404. En ese caso la prueba pasa porque el resultado obtenido coincide con el esperado.

En cambio, un 200 puede ser un defecto si esperábamos otra respuesta.

Por ejemplo, si consultamos un recurso que no existe y la API devuelve 200 con un cuerpo vacío, la prueba falla, porque la API estaría indicando que la petición fue exitosa cuando en realidad el recurso no existe.

Por eso, una prueba no pasa o falla por el número del código HTTP, sino por si el resultado obtenido coincide con el resultado esperado.