# TALLERJAVA
package Reservavuelosavion;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.Duration;
import java.util.Scanner;

public class Reservavuelosavion {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Paso 1: Leer itinerario de vuelo I
        System.out.println("Ingrese el itinerario de vuelo (I1 o I2): ");
        String itinerario = scanner.nextLine();

        // Paso 2 y 3: Definir tiempos T1 y T2
        int T1 = 12; // Tiempo mínimo para reservar
        int T2 = 24; // Tiempo mínimo para cancelar

        // Paso 4 y 5: Evaluar fecha y hora del vuelo
        System.out.println("Ingrese la fecha y hora actual (formato: yyyy-MM-dd HH:mm): ");
        String fechaHoraActualInput = scanner.nextLine();
        System.out.println("Ingrese la fecha y hora del vuelo programado (formato: yyyy-MM-dd HH:mm): ");
        String fechaHoraVueloInput = scanner.nextLine();

        // Formateador para las fechas y horas
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm");

        // Parsear las entradas a objetos LocalDateTime
        LocalDateTime fechaHoraActual = LocalDateTime.parse(fechaHoraActualInput, formatter);
        LocalDateTime fechaHoraVuelo = LocalDateTime.parse(fechaHoraVueloInput, formatter);

        // Comparar las fechas y calcular la diferencia
        Duration diferencia = Duration.between(fechaHoraVuelo, fechaHoraActual);
        long minutosDiferencia = diferencia.toMinutes();

        // Paso 4 y 5: Evaluar si el vuelo está disponible para reserva
        if (minutosDiferencia < T1 * 60) {
            System.out.println("Vuelo no disponible. El tiempo mínimo para realizar una reserva es de " + T1 + " horas.");
        } else {
            System.out.println("El vuelo está disponible para reserva.");

            // Inicializar variables
            int A1 = 120, A2 = 140; // Asientos totales
            int R1 = 0, R2 = 0; // Asientos reservados
            int P1 = 0, P2 = 0; // Asientos a reservar

            // Mostrar opciones para reservar según el itinerario seleccionado
            if (itinerario.equals("I1")) {
                // Paso 10: Mostrar asientos disponibles antes de ingresar la reserva
                int D1 = A1 - R1;
                System.out.println("Asientos disponibles en I1: " + D1);
                
                // Paso 10: Seleccionar asientos a reservar para I1
                System.out.println("Ingrese cantidad de asientos a reservar para I1: ");
                P1 = scanner.nextInt();
                
                // Paso 11 y 12: Calcular reservas
                R1 += P1;
                
                // Paso 13 y 14: Calcular disponibilidad y mostrarla
                D1 = A1 - R1;
                System.out.println("Asientos disponibles en I1 después de la reserva: " + D1);
            } else if (itinerario.equals("I2")) {
                // Paso 10: Mostrar asientos disponibles antes de ingresar la reserva
                int D2 = A2 - R2;
                System.out.println("Asientos disponibles en I2: " + D2);
                
                // Paso 10: Seleccionar asientos a reservar para I2
                System.out.println("Ingrese cantidad de asientos a reservar para I2: ");
                P2 = scanner.nextInt();
                
                // Paso 11 y 12: Calcular reservas
                R2 += P2;
                
                // Paso 13 y 14: Calcular disponibilidad y mostrarla
                D2 = A2 - R2;
                System.out.println("Asientos disponibles en I2 después de la reserva: " + D2);
            }

            // Paso 15 y 16: Verificar equipaje permitido
            if (itinerario.equals("I1")) {
                System.out.println("Equipaje permitido en I1: Máx. 20 kg");
            } else if (itinerario.equals("I2")) {
                System.out.println("Equipaje permitido en I2: Máx. 45 kg");
            }

            // Paso 17 y 18: Verificar si hay asientos agotados
            if (R1 == A1) {
                System.out.println("SOLD OUT para I1");
            }
            if (R2 == A2) {
                System.out.println("SOLD OUT para I2");
            }

            // Paso 19: Preguntar si el usuario desea cancelar la reserva
            System.out.println("¿Desea cancelar una reserva? (si/no): ");
            scanner.nextLine(); // Consumir el salto de línea pendiente
            String cancelar = scanner.nextLine();

            if (cancelar.equalsIgnoreCase("si")) {
                // Paso 20: Evaluar si es posible cancelar la reserva, según T2
                System.out.println("Ingrese la fecha y hora actual para la cancelación (formato: yyyy-MM-dd HH:mm): ");
                String fechaHoraActualCancelacionInput = scanner.nextLine();
                System.out.println("Ingrese la fecha y hora del vuelo programado para cancelación (formato: yyyy-MM-dd HH:mm): ");
                String fechaHoraVueloCancelacionInput = scanner.nextLine();

                // Parsear las entradas de cancelación a objetos LocalDateTime
                LocalDateTime fechaHoraActualCancelacion = LocalDateTime.parse(fechaHoraActualCancelacionInput, formatter);
                LocalDateTime fechaHoraVueloCancelacion = LocalDateTime.parse(fechaHoraVueloCancelacionInput, formatter);

                // Comparar las fechas para cancelación
                Duration diferenciaCancelacion = Duration.between(fechaHoraVueloCancelacion, fechaHoraActualCancelacion);
                long minutosDiferenciaCancelacion = diferenciaCancelacion.toMinutes();

                // Paso 21: Si se cumple el tiempo mínimo para cancelación (T2)
                if (minutosDiferenciaCancelacion < T2 * 60) {
                    System.out.println("No es posible cancelar la reserva. El tiempo mínimo para cancelación es de " + T2 + " horas.");
                } else {
                    System.out.println("La cancelación fue procesada correctamente.");
                    double V = 300.00; // Valor del pasaje
                    double M = V * 0.20; // Recargo por cancelación extemporánea
                    System.out.println("Recargo por cancelación extemporánea: $" + M);
                }
            }
        }

        System.out.println("Fin del programa.");
        scanner.close();
    }
}
