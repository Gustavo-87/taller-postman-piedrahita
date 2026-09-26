# Hallazgos

## Fase 2 - Experimentación con la API

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
|---|---|---|---|---|
| 1 | GET /posts/1 | 200 | 200 ok | Sí |
| 2 | GET /posts | 200 | 200 ok | Sí |
| 3 | GET /posts/9999 | 404 | 404 Not Found | Sí |
| 4 | POST /posts | 201 | 201 ok | Sí |
| 5 | PUT /posts/1 | 200 | 200 ok | Sí |
| 6 | PATCH /posts/1 | 200 | 200 ok | Sí |
| 7 | DELETE /posts/1 | 200 | 200 ok | Sí |

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

### Petición 7 - DELETE /posts/1

#### Hallazgo

La petición DELETE respondió correctamente con código 200.

La respuesta no devolvió información del recurso, lo que indica que la operación de eliminación fue aceptada por la API.

## Tarea 13 - Pruebas automáticas

Agregué tres pruebas adicionales a la petición `GET /posts/1`.

### Prueba 1 - Campo title

Verifica que la respuesta contenga el campo `title`.

~~~javascript
pm.test("La respuesta contiene el campo title", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("title");
});
~~~

### Prueba 2 - Tipo de dato del id

Verifica que el campo `id` sea de tipo numérico.

~~~javascript
pm.test("El id es un número", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.id).to.be.a("number");
});
~~~

### Prueba 3 - Tiempo de respuesta

Verifica que la respuesta tarde menos de 1000 milisegundos.

~~~javascript
pm.test("El tiempo de respuesta es menor a 1000 ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
~~~