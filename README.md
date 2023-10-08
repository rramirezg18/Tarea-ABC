# Tarea-ABC

**AGREGAR - MODIFICAR - ELIMINAR REGISTROS DE UNA BASE DE DATOS**

*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 */

package com.mycompany.ejerciciobasedatos;

/**
 *
 * @author ianto
 */
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class EjercicioBaseDatos {

    public static void main(String[] args) {
        System.out.println("Hello World!");
        String jdbcUrl = "jdbc:mysql://localhost:3306/basedatosproducto";
        String usuario = "root";
        String contraseña = "futbol123";
        Connection conexion = null;

        try {
            conexion = DriverManager.getConnection(jdbcUrl, usuario, contraseña);

            // Agregar un producto
            String insertQuery = "INSERT INTO Productos (Nombre, Precio, Stock) VALUES (?, ?, ?)";
            PreparedStatement insertStatement = conexion.prepareStatement(insertQuery);
            insertStatement.setString(1, "Producto1");
            insertStatement.setDouble(2, 19.99);
            insertStatement.setInt(3, 100);
            insertStatement.executeUpdate();

            // Modificar un producto
            String updateQuery = "UPDATE Productos SET Precio = ?, Stock = ? WHERE ID = ?";
            PreparedStatement updateStatement = conexion.prepareStatement(updateQuery);
            updateStatement.setDouble(1, 24.99);
            updateStatement.setInt(2, 150);
            updateStatement.setInt(3, 1); // ID del producto que deseas modificar
            updateStatement.executeUpdate();

            // Eliminar un producto
            String deleteQuery = "DELETE FROM Productos WHERE ID = ?";
            PreparedStatement deleteStatement = conexion.prepareStatement(deleteQuery);
            deleteStatement.setInt(1, 1); // ID del producto que deseas eliminar
            deleteStatement.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (conexion != null) {
                    conexion.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}

