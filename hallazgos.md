# Hallazgos

## Fase 2 - Experimentación con la API

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
|---|---|---|---|---|
| 1 | GET /posts/1 | 200 | 200 | Sí |
| 2 | GET /posts | 200 | 200 | Sí |
| 3 | GET /posts/9999 | 404 | 404 Not Found | Sí |
| 4 | POST /posts | 201 | 201 | Sí |
| 5 | PUT /posts/1 | 200 | 200 | Sí |
| 6 | PATCH /posts/1 | 200 | Por completar | Por completar |
| 7 | DELETE /posts/1 | 200 | Por completar | Por completar |

### Petición 1 - GET /posts/1

- Código esperado: 200
- Cantidad de elementos: 1
- Campos encontrados:
  - userId
  - id
  - title
  - body

### Petición 2 - GET /posts

- Código de estado: 200 OK
- Cantidad de elementos: 100
- Campos de cada elemento:
  - userId
  - id
  - title
  - body

### ¿En qué se diferencian los criterios de aceptación cuando pides un recurso y cuando pides una colección?

Cuando pido un recurso, espero que la API me devuelva un solo elemento.

Cuando pido una colección, espero que me devuelva varios elementos.

### Petición 3 - GET /posts/9999

#### ¿El caso de prueba pasó o falló?

El caso pasó, porque se esperaba un error 404 al consultar un recurso que no existe y la API respondió exactamente con 404.

#### ¿Qué pasaría si devolviera 200 con un cuerpo vacío?¿Sería un defecto?

Sí sería un defecto, porque estamos pidiendo un recurso que no existe y esperábamos recibir un código 404.

Si la API respondiera 200, estaría diciendo que la petición fue exitosa, aunque realmente no encontró ningún recurso. Por eso, el resultado obtenido no coincidiría con el resultado esperado.

### Petición 4 - POST /posts

#### ¿Qué observé?

Ejecuté la petición cinco veces y en todas las respuestas obtuve el mismo id.

#### ¿Por qué ocurre?

Esto ocurre porque JSONPlaceholder es una API de prueba. Simula la creación del recurso, pero realmente no lo guarda de forma permanente.

#### ¿Cómo comprobaría en una API real que el recurso se creó?

En una API real, después de hacer el POST, consultaría el recurso creado con un GET usando el id recibido. Si el recurso aparece con los datos enviados, significa que sí fue creado correctamente.

### Petición 5 - PUT

#### Hallazgo

Al enviar únicamente el campo "title" con PUT, la respuesta devolvió el nuevo título y el "id" 1.

### Petición 6 - PATCH /posts/1

#### Hallazgo

Al enviar únicamente el campo "title" con PATCH, la respuesta conservó los demás campos del recurso, como "userId", "id" y "body". Esto muestra que PATCH modifica solo el campo indicado y mantiene el resto de la información.

### Diferencia entre PUT y PATCH

Con PUT envié solo el campo "title" y la respuesta devolvió únicamente el título actualizado y el id.

Con PATCH envié también solo el campo "title", pero la respuesta conservó los demás campos del recurso.

Por eso, usaría PATCH para corregir un error de escritura en un solo campo, porque permite modificar solo esa parte sin reemplazar toda la información del recurso.