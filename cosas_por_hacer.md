
Guia 01

Objetivos de Evaluación
Implementación de Migraciones: Evaluar la capacidad de definir y versionar
la estructura de la base de datos mediante código, asegurando el uso correcto
de tipos de datos, restricciones y llaves foráneas.
Construcción de Modelos ORM: Verificar la correcta vinculación entre las
tablas del motor de base de datos y las clases del lenguaje de programación,
incluyendo la definición de relaciones (1:1, 1:N, N:N).
Operaciones CRUD: Validar la habilidad para manipular datos (Crear, Leer,
Actualizar y Eliminar) utilizando las abstracciones del ORM en lugar de
consultas SQL nativas.
Indicaciones generales:
Deberan subir el codigo a un repositorio publico en github y compartir como
respuesta en el espacio correspondiente en classroom
Fecha de entrega 22 de abril de 2026
Pueden usar el repositorio base para comenzar la guia
https://github.com/alejandrorh97/instructoria/tree/base (en la guia 01 estan las
indicaciones como usar el proyecto)
Indicaciones:
Framework a utilizar: laravel (php)
Respetar los nombres dados para las tablas y campos, no se aceptaran
cambios
Modelar la base de datos usando migraciones
Crear el codigo necesario para los modelos
Hacer un CRUD basico para las tablas prestamos, libros, autores y categorias.
Usando api rest con los siguientes endpoints:
index: listar todos los registros

Guia 01 1

show: listar un registro en especifico
store: guardar registro nuevo
update: actualizar un registro
delete: eliminar un registro
Base de datos a modelar
Nota: pueden usar la tabla de users, que se crea automaticamente por el
framework

-- Crear la base de datos
CREATE DATABASE Biblioteca;
USE Biblioteca;

-- 1. Tabla Categorias
CREATE TABLE Categorias (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL
);

-- 2. Tabla Autores
CREATE TABLE Autores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(150) NOT NULL
);

-- 3. Tabla Usuarios
CREATE TABLE Usuarios (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(150) NOT NULL,
    email VARCHAR(100),
    telefono VARCHAR(20)
);

-- 4. Tabla Libros
CREATE TABLE Libros (
    id INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(200) NOT NULL,
    año_publicacion INT,
    id_categoria INT,
    FOREIGN KEY (id_categoria) REFERENCES Categorias(id)
);

-- 5. Tabla Libro_Autor (Relación de muchos a muchos)
CREATE TABLE Libro_Autor (
    id_libro INT,
    id_autor INT,
    PRIMARY KEY (id_libro, id_autor),
    FOREIGN KEY (id_libro) REFERENCES Libros(id),
    FOREIGN KEY (id_autor) REFERENCES Autores(id)
);

-- 6. Tabla Prestamos
CREATE TABLE Prestamos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_usuario INT,
    fecha_prestamo DATE,
    fecha_devolucion DATE,
    FOREIGN KEY (id_usuario) REFERENCES Usuarios(id)
);

-- 7. Tabla Detalle_Prestamo
CREATE TABLE Detalle_Prestamo (
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_prestamo INT,
    id_libro INT,
    FOREIGN KEY (id_prestamo) REFERENCES Prestamos(id),
    FOREIGN KEY (id_libro) REFERENCES Libros(id)
);
