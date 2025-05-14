# Universidad del caribe 
**Materia: Computo de Alto desempeño**  
**Nombre del estudiante: Liliana Jazmin Basto Euan**  

## **Reporte de Evaluación de Rendimiento Web mediante Herramientas de Carga**

### **1. Introducción**

En este informe se presentan los resultados de una evaluación del rendimiento de un servidor web local utilizando dos herramientas especializadas: **Siege** y **ApacheBench (ab)**. El objetivo principal fue analizar el comportamiento del servidor bajo diferentes escenarios de carga, midiendo parámetros clave como disponibilidad, concurrencia, tasa de transacciones, tiempo de respuesta y capacidad de transferencia. Estas pruebas son esenciales para detectar cuellos de botella y asegurar un desempeño eficiente en entornos de producción.


### **2. Herramientas Utilizadas**

- **Siege**: Herramienta de línea de comandos que permite realizar pruebas de carga simulando múltiples usuarios concurrentes, útil para evaluar el rendimiento y la resistencia de aplicaciones web.
  
- **ApacheBench (ab)**: Utilidad incluida con el servidor Apache HTTP que permite medir el rendimiento del servidor bajo diferentes niveles de carga simultánea.


### **3. Resultados Obtenidos**

#### **3.1 Resultados con Siege**

| Métrica                       | Prueba 1 (Básica) | Prueba 2 (Mixta) | Prueba 3 (Host distinto) |
|------------------------------|------------------|------------------|---------------------------|
| Transacciones                | 216              | 741              | 102                       |
| Disponibilidad (%)           | 100              | 58.21            | 100                       |
| Tiempo transcurrido (s)      | 14.94            | 30.42            | 14.45                     |
| Tiempo de respuesta (s)      | 0.06             | 0.18             | 0.04                      |
| Tasa de transacciones (req/s)| 14.46            | 24.36            | 7.06                      |
| Concurrencia                 | 5.05             | 14.73            | 25.19                     |
| Transacciones fallidas       | 0                | 532              | 826                       |

**Observaciones**:
- En condiciones normales, el servidor mantuvo disponibilidad del 100%.
- Con carga elevada y pausas (prueba mixta), se observaron más de 500 fallos.
- La prueba 3 arrojó errores posiblemente por configuración o saturación de recursos.


#### **3.2 Resultados con ApacheBench**

| Métrica                         | Prueba 1 (200 req, c=20) | Prueba 2 (1331 req, c=40) |
|--------------------------------|--------------------------|---------------------------|
| Peticiones completadas         | 200                      | 1331                      |
| Peticiones fallidas            | 0                        | 0                         |
| Tiempo total de prueba (s)     | 3.775                    | 30.00                     |
| Tiempo promedio por petición   | 18.876 ms                | 22.543 ms                 |
| Solicitudes por segundo        | 52.98                    | 44.36                     |
| Tasa de transferencia          | 21.37 KB/s               | 2182.24 KB/s              |
| Tiempo máximo de espera (ms)   | 1125                     | 2256                      |

**Observaciones**:
- ApacheBench mostró una mayor estabilidad bajo carga creciente.
- A pesar del alto volumen de solicitudes, no se reportaron errores.
- La transferencia de datos fue significativamente mayor en la prueba 2.


### **4. Análisis y Discusión**

Los resultados reflejan que el servidor es competente para manejar carga moderada con tiempos de respuesta óptimos. Sin embargo, la herramienta Siege reveló que el servidor puede volverse inestable cuando se enfrentan múltiples usuarios concurrentes y peticiones mixtas, lo cual indica una posible necesidad de optimización de recursos o implementación de mecanismos como caché o balanceadores de carga.

Por su parte, ApacheBench mostró mayor consistencia y permite analizar de forma más detallada los tiempos de respuesta individuales. La ausencia de errores en ambas pruebas refuerza su utilidad para establecer líneas base de rendimiento.


### **5. Conclusiones**

- El servidor presentó un buen rendimiento bajo condiciones controladas, con alta disponibilidad y baja latencia.
- La presencia de errores en pruebas mixtas (Siege) sugiere limitaciones bajo carga concurrente extensa.
- ApacheBench ofrece una mejor perspectiva del rendimiento sostenido y muestra mayor estabilidad.
- Se recomienda aplicar técnicas de escalabilidad y análisis continuo con herramientas complementarias como JMeter o Locust para escenarios más complejos.
