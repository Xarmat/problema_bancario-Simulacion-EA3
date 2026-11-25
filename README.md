# Simulación del problema bancario

## Contexto

Este ejercicio analiza el funcionamiento de las cajas de un banco que atiende dos operaciones: retiros y pagos o consignaciones. El objetivo es comparar distintas distribuciones de cajeros y observar su efecto sobre los tiempos de espera y la atención de los usuarios.

## Modelo

Se utiliza una simulación de eventos discretos. Cada cajero funciona como un servidor independiente con una cola propia y atención por orden de llegada, siguiendo el planteamiento M/M/1 de la actividad.

Los usuarios se generan según las probabilidades del enunciado: 70 % realiza retiros y 30 % pagos o consignaciones. Su clasificación (rápido, normal, lento o muy lento) determina las medias exponenciales de los intervalos entre llegadas y los tiempos de servicio.

Cada réplica representa una jornada de 480 minutos. Se ejecutan 30 réplicas y se comparan cuatro configuraciones:

- Tres cajas mixtas.
- Una caja exclusiva para retiros y dos para pagos.
- Dos cajas exclusivas para retiros y una para pagos.
- Cuatro cajas mixtas.

En cada réplica se utiliza la misma secuencia de usuarios para todos los escenarios, de modo que la comparación se realice bajo una demanda equivalente. Cada usuario se asigna al cajero habilitado que tenga el menor tiempo estimado de espera.

## Herramientas

El modelo se ejecuta en **Google Colab** con Python y las siguientes librerías:

- **NumPy:** generación de variables aleatorias y distribuciones exponenciales.
- **Pandas:** organización y análisis de los datos.
- **Matplotlib:** elaboración de gráficas.
- **SciPy:** cálculo de intervalos de confianza del 95 %.

Estas librerías suelen estar disponibles en Google Colab. Si alguna no está instalada, se puede ejecutar:

```python
!pip install numpy pandas matplotlib scipy
```

## Ejecución

1. Abrir el cuaderno de simulación en Google Colab.
2. Ejecutar las celdas en orden: parámetros, funciones del modelo y ejecución/análisis.
3. Esperar a que finalicen las 30 réplicas para los cuatro escenarios.
4. Descargar el archivo Excel generado al final del proceso.

## Resultados generados

El cuaderno calcula, entre otras medidas:

- Tiempo promedio de atención por cajero.
- Cantidad promedio de usuarios por clasificación.
- Usuarios que llegan y servicios que se completan durante la jornada.
- Tiempos promedio de espera por escenario, operación y clasificación.
- Utilización observada y carga aproximada de los cajeros.
- Intervalos de confianza del 95 % y gráficas comparativas.

El archivo `resultados_simulacion_banco.xlsx` reúne los registros de la simulación y las tablas resumen en hojas separadas.

## Consideraciones

- Los tiempos se expresan en minutos.
- Los usuarios que llegan antes del cierre permanecen en el sistema hasta terminar su servicio, aunque este finalice después de los 480 minutos.
- La utilización observada mide el tiempo ocupado dentro de la jornada; la carga aproximada (`rho`) es una estimación distinta y no debe confundirse con esa utilización.
- El modelo no incorpora costos de personal, costos de apertura de cajas ni variaciones de demanda por hora. Por ello, la decisión sobre una caja adicional se basa en las métricas de servicio simuladas y no en un análisis económico.
