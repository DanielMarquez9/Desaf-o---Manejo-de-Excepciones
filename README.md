Codigo utilizado para implmentar las diferentes pruebas del desafio

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;

// Clase principal que representa el libro de ventas
public class LibroVenta {
    
    private String nombreVenta;
    private String fechaVenta;

    // Constructor que inicializa la venta con un nombre y fecha
    public LibroVenta(String nombreVenta, String fechaVenta) {
        this.nombreVenta = nombreVenta;
        this.fechaVenta = fechaVenta;
    }

    // Métodos para obtener y establecer el nombre de la venta
    public String obtenerNombreVenta() {
        return nombreVenta;
    }

    public void establecerNombreVenta(String nombreVenta) {
        this.nombreVenta = nombreVenta;
    }

    // Métodos para obtener y establecer la fecha de la venta
    public String obtenerFechaVenta() {
        return fechaVenta;
    }

    public void establecerFechaVenta(String fechaVenta) {
        this.fechaVenta = fechaVenta;
    }

    // Método para guardar la venta en un archivo
    public void guardarVenta(Cliente cliente, Vehiculo vehiculo) {
        String datosVenta = cliente.obtenerPatente() + "," + cliente.obtenerEdad() + "," + fechaVenta + "," + nombreVenta;

    
        String rutaArchivo = "ficheros/ventas.txt";

     
        try (BufferedWriter escritor = new BufferedWriter(new FileWriter(rutaArchivo, true))) {
          
            escritor.write(datosVenta);
            escritor.newLine(); 
        } catch (IOException e) {
            System.err.println("Error al escribir en el archivo: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        Cliente cliente = new Cliente("ABC123", 30);
        Vehiculo vehiculo = new Vehiculo("Toyota", "Corolla");
        LibroVenta libroVenta = new LibroVenta("Venta1", obtenerFechaActual());
        libroVenta.guardarVenta(cliente, vehiculo);
    }

    private static String obtenerFechaActual() {
        SimpleDateFormat formatoFecha = new SimpleDateFormat("ddMMyyyy");
        return formatoFecha.format(new Date());
    }
}
