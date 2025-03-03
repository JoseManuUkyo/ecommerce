CREATE DATABASE IF NOT EXISTS negocio;
USE negocio;

-- Tabla de Usuarios
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    correo VARCHAR(100) UNIQUE NOT NULL,
    contrasena VARCHAR(255) NOT NULL,
    edad INT,
    sexo ENUM('Masculino', 'Femenino', 'Otro'));

-- Tabla de Almacén
CREATE TABLE almacen (
    id INT AUTO_INCREMENT PRIMARY KEY,
    producto VARCHAR(100) NOT NULL,
    cantidad DECIMAL(10,2) NOT NULL,
    unidad ENUM('gr', 'litros', 'unidad') NOT NULL);

-- Tabla de Ventas
CREATE TABLE ventas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    producto_id INT,
    precio DECIMAL(10,2) NOT NULL,
    cantidad INT NOT NULL,
    FOREIGN KEY (producto_id) REFERENCES almacen(id));

-- Tabla de Recetas
CREATE TABLE recetas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    tipo ENUM('Grupal', 'Individual') NOT NULL);

-- Relación entre Recetas y Almacén (Productos Necesarios)
CREATE TABLE receta_productos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    receta_id INT,
    producto_id INT,
    cantidad DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (receta_id) REFERENCES recetas(id),
    FOREIGN KEY (producto_id) REFERENCES almacen(id));
