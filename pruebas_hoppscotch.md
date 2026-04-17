# Pruebas API para Hoppscotch

Este archivo tiene pruebas listas para copiar y pegar en Hoppscotch para el CRUD de:
- categorias
- autores
- libros
- prestamos

## Configuracion rapida

- Base URL: http://127.0.0.1:8000/api
- Header para POST y PUT: Content-Type: application/json
- Levantar servidor Laravel:

```bash
php artisan serve
```

## Orden recomendado de pruebas

1. Crear categoria
2. Crear autor
3. Crear libro (usa categoria y autor)
4. Verificar user existente (id_usuario)
5. Crear prestamo

## Datos de prueba sugeridos

Usa estos datos en este orden para que las relaciones funcionen sin errores. Cada prueba indica metodo, URL y body para copiar en Hoppscotch.

### 1. Crear usuario
Si no tienes usuarios en la tabla users, primero crea uno con el endpoint de registro.

- Metodo: POST
- URL: http://127.0.0.1:8000/api/auth/register
- Body JSON:

```json
{
  "first_name": "Juan",
  "last_name": "Perez",
  "email": "juan@example.com",
  "password": "password123",
  "password_confirmation": "password123"
}
```

### 2. Crear categoria

- Metodo: POST
- URL: http://127.0.0.1:8000/api/categorias
- Body JSON:

```json
{
  "nombre": "Novela"
}
```

### 3. Crear autor

- Metodo: POST
- URL: http://127.0.0.1:8000/api/autores
- Body JSON:

```json
{
  "nombre": "Gabriel Garcia Marquez"
}
```

### 4. Crear libro

- Metodo: POST
- URL: http://127.0.0.1:8000/api/libros
- Body JSON:

```json
{
  "titulo": "Cien Anos de Soledad",
  "año_publicacion": 1967,
  "id_categoria": 1,
  "id_autores": [1]
}
```

### 5. Crear prestamo

- Metodo: POST
- URL: http://127.0.0.1:8000/api/prestamos
- Body JSON:

```json
{
  "id_usuario": 1,
  "fecha_prestamo": "2026-04-16",
  "fecha_devolucion": "2026-04-23",
  "id_libros": [1]
}
```

## Categorias

### INDEX
- Metodo: GET
- URL: http://127.0.0.1:8000/api/categorias
- Body: vacio

### STORE
- Metodo: POST
- URL: http://127.0.0.1:8000/api/categorias
- Body JSON:

```json
{
  "nombre": "Novela"
}
```

### SHOW
- Metodo: GET
- URL: http://127.0.0.1:8000/api/categorias/1
- Body: vacio

### UPDATE
- Metodo: PUT
- URL: http://127.0.0.1:8000/api/categorias/1
- Body JSON:

```json
{
  "nombre": "Novela Historica"
}
```

### DELETE
- Metodo: DELETE
- URL: http://127.0.0.1:8000/api/categorias/1
- Body: vacio

## Autores

### INDEX
- Metodo: GET
- URL: http://127.0.0.1:8000/api/autores
- Body: vacio

### STORE
- Metodo: POST
- URL: http://127.0.0.1:8000/api/autores
- Body JSON:

```json
{
  "nombre": "Gabriel Garcia Marquez"
}
```

### SHOW
- Metodo: GET
- URL: http://127.0.0.1:8000/api/autores/1
- Body: vacio

### UPDATE
- Metodo: PUT
- URL: http://127.0.0.1:8000/api/autores/1
- Body JSON:

```json
{
  "nombre": "Gabo"
}
```

### DELETE
- Metodo: DELETE
- URL: http://127.0.0.1:8000/api/autores/1
- Body: vacio

## Libros

### INDEX
- Metodo: GET
- URL: http://127.0.0.1:8000/api/libros
- Body: vacio

### STORE
- Metodo: POST
- URL: http://127.0.0.1:8000/api/libros
- Body JSON:

```json
{
  "titulo": "Cien Anos de Soledad",
  "año_publicacion": 1967,
  "id_categoria": 1,
  "id_autores": [1]
}
```

### SHOW
- Metodo: GET
- URL: http://127.0.0.1:8000/api/libros/1
- Body: vacio

### UPDATE
- Metodo: PUT
- URL: http://127.0.0.1:8000/api/libros/1
- Body JSON:

```json
{
  "titulo": "Cien Anos de Soledad Edicion 2",
  "año_publicacion": 1968,
  "id_categoria": 1,
  "id_autores": [1]
}
```

### DELETE
- Metodo: DELETE
- URL: http://127.0.0.1:8000/api/libros/1
- Body: vacio

## Prestamos

Nota: id_usuario debe existir en la tabla users.

### INDEX
- Metodo: GET
- URL: http://127.0.0.1:8000/api/prestamos
- Body: vacio

### STORE
- Metodo: POST
- URL: http://127.0.0.1:8000/api/prestamos
- Body JSON:

```json
{
  "id_usuario": 1,
  "fecha_prestamo": "2026-04-16",
  "fecha_devolucion": "2026-04-23",
  "id_libros": [1]
}
```

### SHOW
- Metodo: GET
- URL: http://127.0.0.1:8000/api/prestamos/1
- Body: vacio

### UPDATE
- Metodo: PUT
- URL: http://127.0.0.1:8000/api/prestamos/1
- Body JSON:

```json
{
  "id_usuario": 1,
  "fecha_prestamo": "2026-04-16",
  "fecha_devolucion": "2026-04-25",
  "id_libros": [1]
}
```

### DELETE
- Metodo: DELETE
- URL: http://127.0.0.1:8000/api/prestamos/1
- Body: vacio

## Errores comunes

1. Host mysql no resuelve en local:
- Usa DB_HOST=127.0.0.1 en .env
- Ejecuta php artisan config:clear

2. could not find driver:
- Habilita pdo_mysql en PHP

3. Falla de llaves foraneas:
- Crea primero categoria y autor
- Luego crea libro
- Luego crea prestamo
