#### Código DDL para crear las tablas en MySQL

```sql

CREATE DATABASE prg_DistroManager;
USE prg_DistroManager;

CREATE TABLE GestoresVentanas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(255) NOT NULL,
    descripcion TEXT,
    caracteristicas TEXT
);

CREATE TABLE CasosUso (
    id INT AUTO_INCREMENT PRIMARY KEY,
    casoUso VARCHAR(255),
    comentarios TEXT
);

CREATE TABLE Distribuciones (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(255) NOT NULL,
    version VARCHAR(50) NOT NULL,
    descripcion TEXT,
    fechaLanzamiento DATE,
    nivelUsuario VARCHAR(50),
    nivelPersonalizacion ENUM('ALTO', 'MEDIO', 'BAJO'),
    idCasoUso INT,
    FOREIGN KEY (idCasoUso) REFERENCES CasosUso(id)
);

CREATE TABLE Compatibilidad (
    idDistribucion INT,
    idGestorVentanas INT,
    PRIMARY KEY (idDistribucion, idGestorVentanas),
    FOREIGN KEY FK_Distribucion (idDistribucion) REFERENCES Distribuciones(id) ON DELETE CASCADE,
    FOREIGN KEY FK_GestorVentanas (idGestorVentanas) REFERENCES GestoresVentanas(id)
);
```





A continuación, se presenta un script DML (Data Manipulation Language) para insertar datos de prueba en las tablas de la base de datos, asegurando que todas las tablas contengan información y que existan registros relacionados entre ellas.

### Script DML para Insertar Datos de Prueba

```sql
-- Insertar datos en la tabla CasosUso
INSERT INTO CasosUso (id, casoUso, comentarios) VALUES 
(1, 'Servidor', 'Ideal para servidores web.'),
(2, 'Desarrollo', 'Excelente para desarrolladores avanzados.'),
(3, 'Multimedia', 'Software con drivers instalado para diseñadores gráficos.');

-- Insertar datos en la tabla Distribuciones
INSERT INTO Distribuciones (id, nombre, version, descripcion, fechaLanzamiento, nivelUsuario, nivelPersonalizacion, idCasoUso) VALUES 
(1, 'Ubuntu', '20.04', 'Distribución popular para usuarios principiantes.', '2020-04-23', 'Principiante', 'MEDIO', 1),
(2, 'Arch Linux', '2021.05.01', 'Distribución flexible para usuarios avanzados.', '2021-05-01', 'Avanzado', 'ALTO', 2),
(3, 'Fedora', '34', 'Distribución para desarrolladores y usuarios avanzados.', '2021-04-27', 'Intermedio', 'MEDIO', 2),
(4, 'Debian', '10', 'Distribución universal para todo tipo de usuarios.', '2019-07-06', 'Intermedio', 'BAJO', 1);

-- Insertar datos en la tabla GestoresVentanas
INSERT INTO GestoresVentanas (id, nombre, descripcion, caracteristicas) VALUES 
(1, 'GNOME', 'Entorno de escritorio completo y fácil de usar.', 'Integrado con muchas distribuciones.'),
(2, 'i3', 'Gestor de ventanas en mosaico.', 'Alta personalización y eficiencia.'),
(3, 'KDE Plasma', 'Entorno de escritorio moderno y altamente configurable.', 'Múltiples opciones de personalización.'),
(4, 'XFCE', 'Entorno de escritorio ligero y rápido.', 'Ideal para equipos con recursos limitados.');

-- Insertar datos en la tabla Compatibilidad
INSERT INTO Compatibilidad (idDistribucion, idGestorVentanas) VALUES 
(1, 1), -- Ubuntu con GNOME
(1, 4), -- Ubuntu con XFCE
(2, 2), -- Arch Linux con i3
(2, 3), -- Arch Linux con KDE Plasma
(3, 1), -- Fedora con GNOME
(3, 3), -- Fedora con KDE Plasma
(4, 1), -- Debian con GNOME
(4, 4); -- Debian con XFCE
```

