### Código Java

##### Enum `NivelPersonalizacion`

```java
package model;

public enum NivelPersonalizacion {
    ALTO,
    MEDIO,
    BAJO;
}

```

##### Clase `Distribucion`

```java
package model;

import java.util.Date;

public class Distribucion {
    private int id;
    private String nombre;
    private String version;
    private String descripcion;
    private Date fechaLanzamiento;
    private String nivelUsuario;
    private NivelPersonalizacion nivelPersonalizacion;
    private int idCasoUso;

    public Distribucion(int id, String nombre, String version, String descripcion, Date fechaLanzamiento, String nivelUsuario, NivelPersonalizacion nivelPersonalizacion, int idCasoUso) {
        this.id = id;
        this.nombre = nombre;
        this.version = version;
        this.descripcion = descripcion;
        this.fechaLanzamiento = fechaLanzamiento;
        this.nivelUsuario = nivelUsuario;
        this.nivelPersonalizacion = nivelPersonalizacion;
        this.idCasoUso = idCasoUso;
    }

 // Getters and setters, etc
}

```

##### Clase `GestorVentanas`

```java
package model;

public class GestorVentanas {
    private int id;
    private String nombre;
    private String descripcion;
    private String caracteristicas;

    // Constructor, getters y setters
    public GestorVentanas(int id, String nombre, String descripcion, String caracteristicas) {
        this.id = id;
        this.nombre = nombre;
        this.descripcion = descripcion;
        this.caracteristicas = caracteristicas;
    }

    // Getters and setters, etc
}
```

##### Clase `CasoUso`

```java
package model;

public class CasoUso {
    private int id;
    private String casoUso;
    private String comentarios;

    // Constructor, getters y setters
    public CasoUso(int id, String casoUso, String comentarios) {
        this.id = id;
        this.casoUso = casoUso;
        this.comentarios = comentarios;
    }

    // Getters and setters, etc
}
```


##### Clase Compatibilidad

```java
package model;

public class Compatibilidad {
    private int idDistribucion;
    private int idGestorVentanas;

    // Constructor
    public Compatibilidad(int idDistribucion, int idGestorVentanas) {
        this.idDistribucion = idDistribucion;
        this.idGestorVentanas = idGestorVentanas;
    }

// Getters and setters, etc
}

```

##### Clase DAO para `Distribucion`

```java
package examen3t.distromanager.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

import examen3t.distromanager.model.Distribucion;
import examen3t.distromanager.model.NivelPersonalizacion;

public class DistribucionDAO {
    private Connection establecerConexion() throws SQLException {
        String url = "jdbc:mysql://localhost:3307/prg_distromanager";
        String javi = "javi";
        String contrasena = "1qaz2wsx";
        return DriverManager.getConnection(url, javi, contrasena);
    }

// OK pero NO añade el ID al objeto pasado como parámetro
//    public void crearDistribucion(Distribucion distribucion) {
//        String sql = "INSERT INTO Distribuciones (nombre, version, descripcion, fechaLanzamiento, nivelUsuario, nivelPersonalizacion, idCasoUso) VALUES (?, ?, ?, ?, ?, ?, ?)";
//        try (Connection conexion = establecerConexion();
//             PreparedStatement consulta = conexion.prepareStatement(sql)) {
//            consulta.setString(1, distribucion.getNombre());
//            consulta.setString(2, distribucion.getVersion());
//            consulta.setString(3, distribucion.getDescripcion());
//            consulta.setDate(4, new java.sql.Date(distribucion.getFechaLanzamiento().getTime()));
//            consulta.setString(5, distribucion.getNivelUsuario());
//            consulta.setString(6, distribucion.getNivelPersonalizacion().name());
//            consulta.setInt(7, distribucion.getIdCasoUso());
//            consulta.executeUpdate();
//        } catch (SQLException e) {
//            e.printStackTrace();
//        }
//    }

    // añade el ID al objeto pasado como parámetro con PreparedStatement.RETURN_GENERATED_KEYS porque la BD es quien lo genera AUTOINCREMENT
    public void crearDistribucion(Distribucion distribucion) {
        String sql = "INSERT INTO distribuciones (nombre, version, descripcion, fechaLanzamiento, nivelUsuario, nivelPersonalizacion) VALUES (?, ?, ?, ?, ?, ?)";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql, PreparedStatement.RETURN_GENERATED_KEYS)) {
            consulta.setString(1, distribucion.getNombre());
            consulta.setString(2, distribucion.getVersion());
            consulta.setString(3, distribucion.getDescripcion());
            consulta.setDate(4, new java.sql.Date(distribucion.getFechaLanzamiento().getTime()));
            consulta.setString(5, distribucion.getNivelUsuario());
            consulta.setString(6, distribucion.getNivelPersonalizacion().toString());
            int affectedRows = consulta.executeUpdate();

            if (affectedRows > 0) {
                try (ResultSet generatedKeys = consulta.getGeneratedKeys()) {
                    if (generatedKeys.next()) {
                        distribucion.setId(generatedKeys.getInt(1));
                    } else {
                        throw new SQLException("La creación de distribución falló, no se obtuvo ID.");
                    }
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    
    public Distribucion leerDistribucion( int id) {
    	Distribucion distribucion = null;
    	String sql = "SELECT * FROM Distribuciones where id=?";
    	try (
    			Connection conexion = establecerConexion();
    			PreparedStatement consulta = conexion.prepareStatement(sql); 
                
    		) {

    		consulta.setString(1, distribucion.getNombre());
			ResultSet resultados = consulta.executeQuery();
    		
			while (resultados.next()) {
    			distribucion = new Distribucion(
    					resultados.getInt("id"),
    					resultados.getString("nombre"),
    					resultados.getString("version"),
    					resultados.getString("descripcion"),
    					resultados.getDate("fechaLanzamiento"),
    					resultados.getString("nivelUsuario"),
    					NivelPersonalizacion.valueOf(resultados.getString("nivelPersonalizacion")),
    					resultados.getInt("idCasoUso")
    					);
    		}
    	} catch (SQLException e) {
    		e.printStackTrace();
    	}
    	return distribucion;
    }
    
    
    public List<Distribucion> leerDistribuciones() {
        List<Distribucion> distribuciones = new ArrayList<>();
        String sql = "SELECT * FROM Distribuciones";
        try (Connection conexion = establecerConexion();
             Statement consulta = conexion.createStatement();
             ResultSet resultados = consulta.executeQuery(sql)) {
            while (resultados.next()) {
                Distribucion distribucion = new Distribucion(
                    resultados.getInt("id"),
                    resultados.getString("nombre"),
                    resultados.getString("version"),
                    resultados.getString("descripcion"),
                    resultados.getDate("fechaLanzamiento"),
                    resultados.getString("nivelUsuario"),
                    NivelPersonalizacion.valueOf(resultados.getString("nivelPersonalizacion")),
                    resultados.getInt("idCasoUso")
                );
                distribuciones.add(distribucion);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return distribuciones;
    }

    public void actualizarDistribucion(Distribucion distribucion) {
        String sql = "UPDATE Distribuciones SET nombre = ?, version = ?, descripcion = ?, fechaLanzamiento = ?, nivelUsuario = ?, nivelPersonalizacion = ?, idCasoUso = ? WHERE id = ?";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql)) {
            consulta.setString(1, distribucion.getNombre());
            consulta.setString(2, distribucion.getVersion());
            consulta.setString(3, distribucion.getDescripcion());
            consulta.setDate(4, new java.sql.Date(distribucion.getFechaLanzamiento().getTime()));
            consulta.setString(5, distribucion.getNivelUsuario());
            consulta.setString(6, distribucion.getNivelPersonalizacion().name());
            consulta.setInt(7, distribucion.getIdCasoUso());
            consulta.setInt(8, distribucion.getId());
            consulta.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    // funciona gracias a la constrain ON CASCADE DELETE de la FK de la tabla Compatibilidad
    public void eliminarDistribucion(int id) {
        String sql = "DELETE FROM Distribuciones WHERE id = ?";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql)) {
            consulta.setInt(1, id);
            consulta.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

   
    
}

```

##### Clase DAO para `GestorVentanas`

```java
package examen3t.distromanager.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

import examen3t.distromanager.model.GestorVentanas;

public class GestorVentanasDAO {
    private Connection establecerConexion() throws SQLException {
        String url = "jdbc:mysql://localhost:3307/prg_distromanager";
        String javi = "javi";
        String contrasena = "1qaz2wsx";
        return DriverManager.getConnection(url, javi, contrasena);


    }

//    public void crearGestorVentanas(GestorVentanas gestor) {
//        String sql = "INSERT INTO gestoresventanas (nombre, descripcion, caracteristicas) VALUES (?, ?, ?)";
//        try (Connection conexion = establecerConexion();
//             PreparedStatement consulta = conexion.prepareStatement(sql)) {
//            consulta.setString(1, gestor.getNombre());
//            consulta.setString(2, gestor.getDescripcion());
//            consulta.setString(3, gestor.getCaracteristicas());
//            consulta.executeUpdate();
//        } catch (SQLException e) {
//            e.printStackTrace();
//        }
//    }
    
    // Añade el ID al objeto pasado como parámetro con PreparedStatement.RETURN_GENERATED_KEYS porque la BD es quien lo genera (AUTO_INCREMENT)
    public void crearGestorVentanas(GestorVentanas gestorVentanas) {
        String sql = "INSERT INTO gestoresventanas (nombre, descripcion, caracteristicas) VALUES (?, ?, ?)";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql, PreparedStatement.RETURN_GENERATED_KEYS)) {
            consulta.setString(1, gestorVentanas.getNombre());
            consulta.setString(2, gestorVentanas.getDescripcion());
            consulta.setString(3, gestorVentanas.getCaracteristicas());
            int affectedRows = consulta.executeUpdate();

            if (affectedRows > 0) {
                try (ResultSet generatedKeys = consulta.getGeneratedKeys()) {
                    if (generatedKeys.next()) {
                        gestorVentanas.setId(generatedKeys.getInt(1));
                    } else {
                        throw new SQLException("La creación del gestor de ventanas falló, no se obtuvo ID.");
                    }
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }


    public List<GestorVentanas> leerGestoresVentanas() {
        List<GestorVentanas> gestores = new ArrayList<>();
        String sql = "SELECT * FROM gestoresventanas";
        try (Connection conexion = establecerConexion();
             Statement consulta = conexion.createStatement();
             ResultSet resultados = consulta.executeQuery(sql)) {
            while (resultados.next()) {
                GestorVentanas gestor = new GestorVentanas(
                    resultados.getInt("id"),
                    resultados.getString("nombre"),
                    resultados.getString("descripcion"),
                    resultados.getString("caracteristicas")
                );
                gestores.add(gestor);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return gestores;
    }

    public void actualizarGestorVentanas(GestorVentanas gestor) {
        String sql = "UPDATE gestoresventanas SET nombre = ?, descripcion = ?, caracteristicas = ? WHERE id = ?";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql)) {
            consulta.setString(1, gestor.getNombre());
            consulta.setString(2, gestor.getDescripcion());
            consulta.setString(3, gestor.getCaracteristicas());
            consulta.setInt(4, gestor.getId());
            consulta.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

//    public void eliminarGestorVentanas(int id) {
//        String sql = "DELETE FROM gestoresventanas WHERE id = ?";
//        try (Connection conexion = establecerConexion();
//             PreparedStatement consulta = conexion.prepareStatement(sql)) {
//            consulta.setInt(1, id);
//            consulta.executeUpdate();
//        } catch (SQLException e) {
//            e.printStackTrace();
//        }
//    }
    
    // con control a nivel de código Java del proceso en orden de borrado en las diferentes tablas de la base de datos
    public void eliminarGestorVentanas(int idGestorVentanas) {
        String sqlDeleteCompatibilidad = "DELETE FROM Compatibilidad WHERE idGestorVentanas = ?";
        String sqlDeleteGestorVentanas = "DELETE FROM GestoresVentanas WHERE id = ?";

        try (Connection conexion = establecerConexion();
             PreparedStatement stmtDeleteCompatibilidad = conexion.prepareStatement(sqlDeleteCompatibilidad);
             PreparedStatement stmtDeleteGestorVentanas = conexion.prepareStatement(sqlDeleteGestorVentanas)) {
            
            // Primero, eliminar todas las entradas en Compatibilidad que referencien este gestor de ventanas
            stmtDeleteCompatibilidad.setInt(1, idGestorVentanas);
            stmtDeleteCompatibilidad.executeUpdate();

            // Segundo, eliminar el gestor de ventanas
            stmtDeleteGestorVentanas.setInt(1, idGestorVentanas);
            stmtDeleteGestorVentanas.executeUpdate();

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
}

```

##### Clase DAO para `CasoUso`

```java
package examen3t.distromanager.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

import examen3t.distromanager.model.CasoUso;

public class CasoUsoDAO {
    private Connection establecerConexion() throws SQLException {
        String url = "jdbc:mysql://localhost:3307/prg_distromanager";
        String javi = "javi";
        String contrasena = "1qaz2wsx";
        return DriverManager.getConnection(url, javi, contrasena);
    }

//    public void crearCasoUso(CasoUso caso) {
//        String sql = "INSERT INTO casosuso (casoUso, comentarios) VALUES (?, ?)";
//        try (Connection conexion = establecerConexion();
//             PreparedStatement consulta = conexion.prepareStatement(sql)) {
//            consulta.setString(1, caso.getCasoUso());
//            consulta.setString(2, caso.getComentarios());
//            consulta.executeUpdate();
//        } catch (SQLException e) {
//            e.printStackTrace();
//        }
//    }

    // añade el ID al objeto pasado como parámetro con PreparedStatement.RETURN_GENERATED_KEYS
    public void crearCasoUso(CasoUso caso) {
        String sql = "INSERT INTO casosuso (casoUso, comentarios) VALUES (?, ?)";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql, PreparedStatement.RETURN_GENERATED_KEYS)) {
            consulta.setString(1, caso.getCasoUso());
            consulta.setString(2, caso.getComentarios());
            int affectedRows = consulta.executeUpdate();

            if (affectedRows > 0) {
                try (ResultSet generatedKeys = consulta.getGeneratedKeys()) {
                    if (generatedKeys.next()) {
                        caso.setId(generatedKeys.getInt(1));
                    } else {
                        throw new SQLException("La creación de caso de uso falló, no se obtuvo ID.");
                    }
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    public List<CasoUso> leerCasosUso() {
        List<CasoUso> casos = new ArrayList<>();
        String sql = "SELECT * FROM casosuso";
        try (Connection conexion = establecerConexion();
             Statement consulta = conexion.createStatement();
             ResultSet resultados = consulta.executeQuery(sql)) {
            while (resultados.next()) {
                CasoUso caso = new CasoUso(
                    resultados.getInt("id"),
                    resultados.getString("casoUso"),
                    resultados.getString("comentarios")
                );
                casos.add(caso);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return casos;
    }

    public void actualizarCasoUso(CasoUso caso) {
        String sql = "UPDATE casosuso SET casoUso = ?, comentarios = ? WHERE id = ?";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql)) {
            consulta.setString(1, caso.getCasoUso());
            consulta.setString(2, caso.getComentarios());
            consulta.setInt(3, caso.getId());
            consulta.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public void eliminarCasoUso(int id) {
        String sql = "DELETE FROM casosuso WHERE id = ?";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql)) {
            consulta.setInt(1, id);
            consulta.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

```



##### Clase DAO para Compatibilidad

```java
package examen3t.distromanager.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import examen3t.distromanager.model.Compatibilidad;
import examen3t.distromanager.model.Distribucion;
import examen3t.distromanager.model.GestorVentanas;
import examen3t.distromanager.model.NivelPersonalizacion;

public class CompatibilidadDAO {
    private Connection establecerConexion() throws SQLException {
        String url = "jdbc:mysql://localhost:3307/prg_distromanager";
        String javi = "javi";
        String contrasena = "1qaz2wsx";
        return DriverManager.getConnection(url, javi, contrasena);
    }

    // NO tiene sentido añadir el ID al objeto pasado como parámetro con PreparedStatement.RETURN_GENERATED_KEYS porque este ID no es autogenerado por la BD
    public void crearCompatibilidad(Compatibilidad compatibilidad) {
        String sql = "INSERT INTO Compatibilidad (idDistribucion, idGestorVentanas) VALUES (?, ?)";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql)) {
            consulta.setInt(1, compatibilidad.getIdDistribucion());
            consulta.setInt(2, compatibilidad.getIdGestorVentanas());
            consulta.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public List<Compatibilidad> leerCompatibilidades() {
        List<Compatibilidad> compatibilidades = new ArrayList<>();
        String sql = "SELECT * FROM Compatibilidad";
        try (Connection conexion = establecerConexion();
             Statement consulta = conexion.createStatement();
             ResultSet resultados = consulta.executeQuery(sql)) {
            while (resultados.next()) {
                Compatibilidad compatibilidad = new Compatibilidad(
                    resultados.getInt("idDistribucion"),
                    resultados.getInt("idGestorVentanas")
                );
                compatibilidades.add(compatibilidad);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return compatibilidades;
    }

    public void eliminarCompatibilidad(int idDistribucion, int idGestorVentanas) {
        String sql = "DELETE FROM Compatibilidad WHERE idDistribucion = ? AND idGestorVentanas = ?";
        try (Connection conexion = establecerConexion();
             PreparedStatement consulta = conexion.prepareStatement(sql)) {
            consulta.setInt(1, idDistribucion);
            consulta.setInt(2, idGestorVentanas);
            consulta.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public String obtenerGestorMasPopular() {
        String sql = "SELECT gv.nombre, COUNT(c.idGestorVentanas) AS conteo " +
                     "FROM Compatibilidad c " +
                     "JOIN GestoresVentanas gv ON c.idGestorVentanas = gv.id " +
                     "GROUP BY gv.nombre " +
                     "ORDER BY conteo DESC " +
                     "LIMIT 1";

        try (Connection conexion = establecerConexion();
             Statement consulta = conexion.createStatement();
             ResultSet resultados = consulta.executeQuery(sql)) {
            if (resultados.next()) {
                return resultados.getString("nombre");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return "No hay gestores populares";
    }
    
    
    
    public Map<Distribucion, List<GestorVentanas>> obtenerMapaDistribucionGestores() {
        Distribucion distribucion = null;
        GestorVentanas gestorVentanas = null;
        
    	Map<Distribucion, List<GestorVentanas>> mapa = new HashMap<>();
        String sql = "SELECT d.*, g.* FROM Compatibilidad c " +
                     "JOIN Distribuciones d ON c.idDistribucion = d.id " +
                     "JOIN GestoresVentanas g ON c.idGestorVentanas = g.id";
        try (Connection conexion = establecerConexion();
             PreparedStatement stmt = conexion.prepareStatement(sql);
             ResultSet rs = stmt.executeQuery()) {
            while (rs.next()) {
               
            	distribucion = new Distribucion(
            			rs.getInt("d.id"),
            			rs.getString("d.nombre"),
            			rs.getString("d.version"),
            			rs.getString("d.descripcion"),
            			rs.getDate("d.fechaLanzamiento"),
            			rs.getString("d.nivelUsuario"),
    					NivelPersonalizacion.valueOf(rs.getString("nivelPersonalizacion")),
    					rs.getInt("idCasoUso")
    					);
            	gestorVentanas = new GestorVentanas(
                        rs.getInt("id"),
                        rs.getString("nombre"),
                        rs.getString("descripcion"),
                        rs.getString("caracteristicas")
                    );
            	
                mapa.computeIfAbsent(distribucion, k -> new ArrayList<>()).add(gestorVentanas);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return mapa;
    }
}


```

##### Clase Principal para Ejecutar las pruebas


```java

package main;

import dao.DistribucionDAO;
import dao.GestorVentanasDAO;
import dao.CasoUsoDAO;
import dao.CompatibilidadDAO;
import model.Distribucion;
import model.GestorVentanas;
import model.CasoUso;
import model.Compatibilidad;
import model.NivelPersonalizacion;

import java.util.Date;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;
import java.util.Comparator;

public class DistroManager {
    public static void main(String[] args) {
        DistribucionDAO distribucionDAO = new DistribucionDAO();
        GestorVentanasDAO gestorVentanasDAO = new GestorVentanasDAO();
        CasoUsoDAO casoUsoDAO = new CasoUsoDAO();
        CompatibilidadDAO compatibilidadDAO = new CompatibilidadDAO();

        // Crear nuevos casos de uso
        CasoUso caso1 = new CasoUso(1, "Servidor", "Ideal para servidores web.");
        CasoUso caso2 = new CasoUso(2, "Desarrollo", "Excelente para desarrolladores avanzados.");
        casoUsoDAO.crearCasoUso(caso1);
        casoUsoDAO.crearCasoUso(caso2);

        // Crear nuevas distribuciones
        Distribucion distribucion1 = new Distribucion(1, "Ubuntu", "20.04", "Distribución popular para usuarios principiantes.", new Date(), "Principiante", NivelPersonalizacion.MEDIO, caso1.getId());
        Distribucion distribucion2 = new Distribucion(2, "Arch Linux", "2021.05.01", "Distribución flexible para usuarios avanzados.", new Date(), "Avanzado", NivelPersonalizacion.ALTO, caso2.getId());
        distribucionDAO.crearDistribucion(distribucion1);
        distribucionDAO.crearDistribucion(distribucion2);

        // Leer y mostrar distribuciones
        List<Distribucion> distribuciones = distribucionDAO.leerDistribuciones();
        distribuciones.forEach(d -> System.out.println(d.getNombre()));

        // Filtrar distribuciones por nivel de personalización
        List<Distribucion> distribucionesFiltradas = distribuciones.stream()
            .filter(d -> d.getNivelPersonalizacion() == NivelPersonalizacion.ALTO)
            .collect(Collectors.toList());
        distribucionesFiltradas.forEach(d -> System.out.println(d.getNombre() + " - " + d.getNivelPersonalizacion()));

        // Ordenar distribuciones por fecha de lanzamiento
        List<Distribucion> distribucionesOrdenadas = distribuciones.stream()
            .sorted(Comparator.comparing(Distribucion::getFechaLanzamiento))
            .collect(Collectors.toList());
        distribucionesOrdenadas.forEach(d -> System.out.println(d.getNombre()));

        // Agrupar distribuciones por nivel de usuario
        Map<String, List<Distribucion>> distribucionesPorNivelUsuario = distribuciones.stream()
            .collect(Collectors.groupingBy(Distribucion::getNivelUsuario));
        distribucionesPorNivelUsuario.forEach((nivel, lista) -> {
            System.out.println("Nivel de usuario: " + nivel);
            lista.forEach(d -> System.out.println(" - " + d.getNombre()));
        });

        // Crear y mostrar gestores de ventanas
        GestorVentanas gestor1 = new GestorVentanas(1, "GNOME", "Entorno de escritorio completo y fácil de usar.", "Integrado con muchas distribuciones.");
        GestorVentanas gestor2 = new GestorVentanas(2, "i3", "Gestor de ventanas en mosaico.", "Alta personalización y eficiencia.");
        gestorVentanasDAO.crearGestorVentanas(gestor1);
        gestorVentanasDAO.crearGestorVentanas(gestor2);

        List<GestorVentanas> gestores = gestorVentanasDAO.leerGestoresVentanas();
        gestores.forEach(g -> System.out.println(g.getNombre() + " - " + g.getDescripcion()));

        // Crear relaciones de compatibilidad
        Compatibilidad compatibilidad1 = new Compatibilidad(1, 1); // Ubuntu con GNOME
        Compatibilidad compatibilidad2 = new Compatibilidad(1, 2); // Ubuntu con i3
        compatibilidadDAO.crearCompatibilidad(compatibilidad1);
        compatibilidadDAO.crearCompatibilidad(compatibilidad2);

        // Leer y mostrar compatibilidades
        List<Compatibilidad> compatibilidades = compatibilidadDAO.leerCompatibilidades();
        compatibilidades.forEach(c -> System.out.println("Distribucion ID: " + c.getIdDistribucion() + " - Gestor Ventanas ID: " + c.getIdGestorVentanas()));

        // Mostrar casos de uso por distribución
        Map<Integer, List<Distribucion>> distribucionesPorCasoUso = distribuciones.stream()
            .collect(Collectors.groupingBy(Distribucion::getIdCasoUso));
        distribucionesPorCasoUso.forEach((idCasoUso, lista) -> {
            String casoUsoNombre = casoUsoDAO.leerCasosUso().stream()
                .filter(c -> c.getId() == idCasoUso)
                .map(CasoUso::getCasoUso)
                .findFirst()
                .orElse("Desconocido");
            System.out.println("Caso de uso: " + casoUsoNombre);
            lista.forEach(d -> System.out.println(" - " + d.getNombre()));
        });

        // Calcular la distribución más recomendada para principiantes
        String distribucionPrincipiante = distribuciones.stream()
            .filter(d -> d.getNivelUsuario().equals("Principiante"))
            .map(Distribucion::getNombre)
            .findFirst()
            .orElse("No hay distribuciones para principiantes");
        System.out.println("Distribución recomendada para principiantes: " + distribucionPrincipiante);

        // Calcular el gestor de ventanas más popular usando el nuevo método del DAO
        String gestorMasPopular = compatibilidadDAO.obtenerGestorMasPopular();
        System.out.println("Gestor de ventanas más popular: " + gestorMasPopular);
    }
}


```


Otra batería de pruebas más avanzadas y con métodos de borrado y generación de datos.

```java
package examen3t.distromanager.main;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Random;
import java.util.stream.Collectors;

import examen3t.distromanager.dao.CasoUsoDAO;
import examen3t.distromanager.dao.CompatibilidadDAO;
import examen3t.distromanager.dao.DistribucionDAO;
import examen3t.distromanager.dao.GestorVentanasDAO;
import examen3t.distromanager.model.CasoUso;
import examen3t.distromanager.model.Compatibilidad;
import examen3t.distromanager.model.Distribucion;
import examen3t.distromanager.model.GestorVentanas;
import examen3t.distromanager.model.NivelPersonalizacion;

public class DistroManager {
	public static void main(String[] args) {
		DistribucionDAO distribucionDAO = new DistribucionDAO();
		GestorVentanasDAO gestorVentanasDAO = new GestorVentanasDAO();
		CasoUsoDAO casoUsoDAO = new CasoUsoDAO();
		CompatibilidadDAO compatibilidadDAO = new CompatibilidadDAO();

		// borrar datos
		borrarDatos();
		// generar datos
		generarDatos(10);

		// Crear nuevos casos de uso
		CasoUso caso1 = new CasoUso("Servidor LDAP", "Ideal para servidores LDAP.");
		CasoUso caso2 = new CasoUso("Desarrollo", "Excelente para desarrolladores avanzados.");
		casoUsoDAO.crearCasoUso(caso1);
		casoUsoDAO.crearCasoUso(caso2);

		// Crear nuevas distribuciones
		Distribucion distribucion1 = new Distribucion("Ubuntu 2 ", "20.04", "Distribución popular para usuarios principiantes.", new Date(), "Principiante", NivelPersonalizacion.MEDIO, caso1.getId());
		Distribucion distribucion2 = new Distribucion("Arch Linux 2", "2021.05.01", "Distribución flexible para usuarios avanzados.", new Date(), "Avanzado", NivelPersonalizacion.ALTO, caso2.getId());
		distribucionDAO.crearDistribucion(distribucion1);
		distribucionDAO.crearDistribucion(distribucion2);

		// Leer y mostrar distribuciones
		List<Distribucion> distribuciones = distribucionDAO.leerDistribuciones();
		distribuciones.forEach(d -> System.out.println(d.getNombre()));

		// Filtrar distribuciones por nivel de personalización
		List<Distribucion> distribucionesFiltradas = distribuciones.stream()
				.filter(d -> d.getNivelPersonalizacion() == NivelPersonalizacion.ALTO)
				.collect(Collectors.toList());
		distribucionesFiltradas.forEach(d -> System.out.println(d.getNombre() + " - " + d.getNivelPersonalizacion()));

		// Ordenar distribuciones por fecha de lanzamiento
		List<Distribucion> distribucionesOrdenadas = distribuciones.stream()
				.sorted(Comparator.comparing(Distribucion::getFechaLanzamiento))
				.collect(Collectors.toList());
		distribucionesOrdenadas.forEach(d -> System.out.println(d.getNombre()));

		// Agrupar distribuciones por nivel de usuario
		Map<String, List<Distribucion>> distribucionesPorNivelUsuario = distribuciones.stream()
				.collect(Collectors.groupingBy(Distribucion::getNivelUsuario));
		distribucionesPorNivelUsuario.forEach((nivel, lista) -> {
			System.out.println("Nivel de usuario: " + nivel);
			lista.forEach(d -> System.out.println(" - " + d.getNombre()));
		});

		// Crear y mostrar gestores de ventanas
		GestorVentanas gestor1 = new GestorVentanas("GNOME 2", "Entorno de escritorio completo y fácil de usar.", "Integrado con muchas distribuciones.");
		GestorVentanas gestor2 = new GestorVentanas("i3 2", "Gestor de ventanas en mosaico.", "Alta personalización y eficiencia.");
		gestorVentanasDAO.crearGestorVentanas(gestor1);
		gestorVentanasDAO.crearGestorVentanas(gestor2);

		List<GestorVentanas> gestores = gestorVentanasDAO.leerGestoresVentanas();
		gestores.forEach(g -> System.out.println(g.getNombre() + " - " + g.getDescripcion()));

		// Crear relaciones de compatibilidad
		Compatibilidad compatibilidad1 = new Compatibilidad(distribucion1.getId(), gestor1.getId()); // Ubuntu con GNOME
		Compatibilidad compatibilidad2 = new Compatibilidad(distribucion2.getId(), gestor2.getId()); // Arch Linux con i3
		compatibilidadDAO.crearCompatibilidad(compatibilidad1);
		compatibilidadDAO.crearCompatibilidad(compatibilidad2);

		// Leer y mostrar compatibilidades
		List<Compatibilidad> compatibilidades = compatibilidadDAO.leerCompatibilidades();
		compatibilidades.forEach(c -> System.out.println("Distribucion ID: " + c.getIdDistribucion() + " - Gestor Ventanas ID: " + c.getIdGestorVentanas()));

		// Mostrar casos de uso por distribución
		Map<Integer, List<Distribucion>> distribucionesPorCasoUso = distribuciones.stream()
				.collect(Collectors.groupingBy(Distribucion::getIdCasoUso));
		distribucionesPorCasoUso.forEach((idCasoUso, lista) -> {
			String casoUsoNombre = casoUsoDAO.leerCasosUso().stream()
					.filter(c -> c.getId() == idCasoUso)
					.map(CasoUso::getCasoUso)
					.findFirst()
					.orElse("Desconocido");
			System.out.println("Caso de uso: " + casoUsoNombre);
			lista.forEach(d -> System.out.println(" - " + d.getNombre()));
		});

		// Calcular la distribución más recomendada para principiantes
		String distribucionPrincipiante = distribuciones.stream()
				.filter(d -> d.getNivelUsuario().equals("Principiante"))
				.map(Distribucion::getNombre)
				.findFirst()
				.orElse("No hay distribuciones para principiantes");
		System.out.println("Distribución recomendada para principiantes: " + distribucionPrincipiante);

		// Calcular el gestor de ventanas más popular usando el nuevo método del DAO
		String gestorMasPopular = compatibilidadDAO.obtenerGestorMasPopular();
		System.out.println("Gestor de ventanas más popular: " + gestorMasPopular);


		System.out.println("\n---\n");
		// Mostrar un Map < Distribucion , List<GestorVentanas> > que relacione cada distribución con los gestores de ventanas que le son compatibles leyendo la información disponible desde la BD utilizando los diferentes DAO y operaciones sobre Stream  
		long principioStream = System.nanoTime();
		mapaDistroGestoresStream();
		long finStream = System.nanoTime(); 
		long tiempoStream =  finStream - principioStream;


		System.out.println("\n---\n");
		// Mostrar mapa Map < Distribucion , List<GestorVentanas> idem al anterior PERO usando un método implementado en CompatibilidadDAO
		long principioDAO = System.nanoTime();
		mapaDistroGestoresDAO();
		long finDAO = System.nanoTime();
		long tiempoDAO = finDAO - principioDAO;
		
		long tiempoMayor = Math.max(tiempoStream, tiempoDAO);
		long tiempoMenor = Math.min(tiempoStream, tiempoDAO);
		double porcentajeDiferencia = ((double)(tiempoMayor - tiempoMenor) / tiempoMayor) * 100;

		System.out.println("Tiempo Stream: \t" + tiempoStream + " nanosegundos");
		System.out.println("Tiempo DAO: \t" + tiempoDAO + " nanosegundos");
		System.out.println("Diferencia: " + Math.abs(tiempoStream - tiempoDAO) +  " nanosegundos");
		System.out.println("Solución DAO es un " + String.format("%.2f", porcentajeDiferencia) +  "% más rápido que Stream si es menor, si no lo contrario.");


		// Ahora realizamos las pruebas de borrado por ID utilizando los DAO

		// Suponiendo que ya tenemos IDs existentes para las pruebas
		int idDistribucion = distribucion1.getId();  // ( Ubuntu 2 ) Asegúrate de que este ID exista en tu base de datos
		int idGestorVentanas = gestor1.getId(); // ( Gnome 2 ) Asegúrate de que este ID exista en tu base de datos
		int idCasoUso = caso1.getId();  // ( Servidor LDAP) Asegúrate de que este ID exista en tu base de datos


		// Borrar una compatibilidad (esto no debería afectar otras tablas pues ninguna tiene un FK hacia ella)
		compatibilidadDAO.eliminarCompatibilidad(compatibilidad1.getIdDistribucion(),compatibilidad1.getIdGestorVentanas());

		// Borrar un gestor de ventanas (debería borrar primero las referencias en Compatibilidad si es necesario, hecho en código eliminarGestorVentanas )
		gestorVentanasDAO.eliminarGestorVentanas(idGestorVentanas);

		// Borrar una distribución (las referencias en Compatibilidad se borran por el SGBD debido a ON CASCADE DELETE sobre la FK)
		distribucionDAO.eliminarDistribucion(idDistribucion);

		// Borrar un caso de uso (esto podría fallar si hay distribuciones que lo referencian, dependiendo de tu esquema)
		casoUsoDAO.eliminarCasoUso(idCasoUso);

	}


	public static void mapaDistroGestoresDAO() {
		CompatibilidadDAO compatibilidadDAO = new CompatibilidadDAO();

		// Obtener el mapa de distribuciones a gestores de ventanas
		Map<Distribucion, List<GestorVentanas>> mapaDistribucionGestores = compatibilidadDAO.obtenerMapaDistribucionGestores();

		// Mostrar los resultados
		for (Map.Entry<Distribucion, List<GestorVentanas>> entrada : mapaDistribucionGestores.entrySet()) {
			Distribucion distribucion = entrada.getKey();
			List<GestorVentanas> gestores = entrada.getValue();

			// Imprimir detalles de la distribución
			System.out.println("Distribución: " + distribucion.getNombre() + " (ID: " + distribucion.getId() + ")");
			System.out.println("Versión: " + distribucion.getVersion());
			System.out.println("Descripción: " + distribucion.getDescripcion());
			System.out.println("Nivel de Personalización: " + distribucion.getNivelPersonalizacion());

			// Imprimir los gestores de ventanas asociados
			System.out.println("Gestores de Ventanas Compatibles:");
			for (GestorVentanas gestor : gestores) {
				System.out.println(" - " + gestor.getNombre() + " (ID: " + gestor.getId() + ")");
				System.out.println("   Descripción: " + gestor.getDescripcion());
			}
			System.out.println();
		}
	}

	public static void mapaDistroGestoresStream() {
		DistribucionDAO distribucionDAO = new DistribucionDAO();
		GestorVentanasDAO gestorVentanasDAO = new GestorVentanasDAO();
		CompatibilidadDAO compatibilidadDAO = new CompatibilidadDAO();

		// Recuperar listas de entidades desde la base de datos
		List<Distribucion> distribuciones = distribucionDAO.leerDistribuciones();
		List<GestorVentanas> gestores = gestorVentanasDAO.leerGestoresVentanas();
		List<Compatibilidad> compatibilidades = compatibilidadDAO.leerCompatibilidades();

		// Crear el mapa de distribución a gestores
		Map<Distribucion, List<GestorVentanas>> mapaDistribucionGestores = new HashMap<>();
		for (Compatibilidad comp : compatibilidades) {
			Distribucion distribucion = distribuciones.stream()
					.filter(d -> d.getId() == comp.getIdDistribucion())
					.findFirst()
					.orElse(null);

			GestorVentanas gestor = gestores.stream()
					.filter(g -> g.getId() == comp.getIdGestorVentanas())
					.findFirst()
					.orElse(null);

			if (distribucion != null && gestor != null) {
				mapaDistribucionGestores.computeIfAbsent(distribucion, k -> new ArrayList<>()).add(gestor);
			}
		}

		// Mostrar los resultados
		for (Map.Entry<Distribucion, List<GestorVentanas>> entrada : mapaDistribucionGestores.entrySet()) {
			Distribucion distribucion = entrada.getKey();
			List<GestorVentanas> gestoresCompatibles = entrada.getValue();

			System.out.println("Distribución: " + distribucion.getNombre() + " (ID: " + distribucion.getId() + ")");
			System.out.println("Versión: " + distribucion.getVersion());
			System.out.println("Descripción: " + distribucion.getDescripcion());
			System.out.println("Nivel de Personalización: " + distribucion.getNivelPersonalizacion());
			System.out.println("Gestores de Ventanas Compatibles:");
			for (GestorVentanas gestor : gestoresCompatibles) {
				System.out.println(" - " + gestor.getNombre() + " (ID: " + gestor.getId() + ")");
				System.out.println("   Descripción: " + gestor.getDescripcion());
			}
			System.out.println();
		}
	}


	public static void borrarDatos() {
		try (Connection conexion = DriverManager.getConnection("jdbc:mysql://localhost:3307/prg_distromanager", "root", "27z1a26y2b");
				Statement consulta = conexion.createStatement()) {
			// Deshabilitar las restricciones de clave externa
			consulta.execute("SET FOREIGN_KEY_CHECKS = 0");

			// Deshabilitar el modo seguro
			consulta.execute("SET SQL_SAFE_UPDATES = 0");

			// Borrar los datos de las tablas
			consulta.execute("DELETE FROM Compatibilidad");
			consulta.execute("DELETE FROM Distribuciones");
			consulta.execute("DELETE FROM GestoresVentanas");
			consulta.execute("DELETE FROM CasosUso");

			// Reiniciar los contadores de AUTO_INCREMENT
			consulta.execute("ALTER TABLE Compatibilidad AUTO_INCREMENT = 1");
			consulta.execute("ALTER TABLE Distribuciones AUTO_INCREMENT = 1");
			consulta.execute("ALTER TABLE GestoresVentanas AUTO_INCREMENT = 1");
			consulta.execute("ALTER TABLE CasosUso AUTO_INCREMENT = 1");

			// Volver a habilitar el modo seguro
			consulta.execute("SET SQL_SAFE_UPDATES = 1");

			// Volver a habilitar las restricciones de clave externa
			consulta.execute("SET FOREIGN_KEY_CHECKS = 1");

			System.out.println("Todos los datos han sido borrados exitosamente y los contadores de AUTO_INCREMENT reiniciados.");

		} catch (SQLException e) {
			e.printStackTrace();
		}
	}



	public static void generarDatos(int registros) {
		DistribucionDAO distribucionDAO = new DistribucionDAO();
		GestorVentanasDAO gestorVentanasDAO = new GestorVentanasDAO();
		CasoUsoDAO casoUsoDAO = new CasoUsoDAO();
		CompatibilidadDAO compatibilidadDAO = new CompatibilidadDAO();

		Random random = new Random();
		int numeroRegistros = registros; // Define la cantidad de entradas que deseas generar

		// Crear Casos de Uso
		for (int i = 1; i <= 10; i++) {
			CasoUso caso = new CasoUso("Uso " + i, "Descripción del caso de uso " + i);
			casoUsoDAO.crearCasoUso(caso);
		}

		// Crear Distribuciones y Gestores de Ventanas
		for (int i = 1; i <= numeroRegistros; i++) {
			Distribucion distribucion = new Distribucion(
					"Distribucion " + i,
					"v" + (i % 10 + 1),
					"Descripción de Distribución " + i,
					new Date(),
					i % 2 == 0 ? "Principiante" : "Avanzado",
							i % 3 == 0 ? NivelPersonalizacion.ALTO : NivelPersonalizacion.MEDIO,
									random.nextInt(10) + 1  // ID de Caso de Uso aleatorio entre 1 y 10
					);
			distribucionDAO.crearDistribucion(distribucion);

			GestorVentanas gestor = new GestorVentanas(
					"Gestor " + i,
					"Descripción del gestor " + i,
					"Características del gestor " + i
					);
			gestorVentanasDAO.crearGestorVentanas(gestor);


		}

		// Crea relaciones de compatibilidad
		// Asociar cada distribución con hasta 10 gestores diferentes
		for (int i = 1; i <= numeroRegistros; i++) {
			for (int j = 1; j <= 10; j++) {
				Compatibilidad compatibilidad = new Compatibilidad(i, j);
				compatibilidadDAO.crearCompatibilidad(compatibilidad);
			}
		}


		System.out.println("Datos de prueba generados exitosamente.");
	}


}



```
