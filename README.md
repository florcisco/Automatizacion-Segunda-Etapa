# Automatización para el Cálculo de Recuperatorios

Herramienta desarrollada en Python para automatizar el procesamiento y cálculo de recuperatorios a partir de archivos académicos en formato Excel.

El programa permite reducir tareas manuales y repetitivas, centralizando el procesamiento de información, la validación de datos y la generación de reportes.

## Objetivo

El objetivo principal es automatizar una parte del procesamiento académico que anteriormente requería revisar y modificar manualmente diferentes archivos de Excel.

La herramienta busca:

- Automatizar el procesamiento de información.
- Reducir tareas repetitivas.
- Disminuir errores producidos por la manipulación manual de datos.
- Realizar controles de calidad sobre la información.
- Comparar información proveniente de diferentes archivos.
- Calcular automáticamente los recuperatorios.
- Generar un archivo final listo para continuar con el procesamiento académico.

## Tecnologías utilizadas

- Python
- Tkinter
- OpenPyXL
- Threading
- Queue

## Características principales

### Selección de archivos

El programa permite seleccionar los archivos necesarios mediante una interfaz gráfica.

Los archivos de entrada pueden encontrarse en formatos:

- `.xlsx`
- `.xlsm`

### Validación de archivos

Antes de comenzar el procesamiento, el programa verifica que los archivos seleccionados sean los correspondientes y que puedan ser procesados correctamente.

### Validación del contenido

Se realizan controles sobre los datos contenidos en los archivos, incluyendo:

- Identificación de alumnos.
- DNI.
- Nombres y apellidos.
- Notas.
- Inasistencias.
- Datos necesarios para el cálculo de recuperatorios.

La herramienta también contempla diferentes formatos de identificación de los alumnos y realiza una normalización de nombres para facilitar las comparaciones.

### Comparación de alumnos

La identificación de los alumnos se realiza priorizando el DNI.

Cuando es necesario, se utiliza también el nombre normalizado para realizar la correspondencia entre los distintos archivos.

El sistema informa situaciones como:

- Alumnos que no fueron encontrados.
- Diferencias de DNI.
- Coincidencias por nombre.
- Coincidencias ambiguas.
- Diferencias entre los datos de los archivos.

### Cálculo de recuperatorios

A partir de la información validada y comparada, el programa realiza automáticamente los cálculos correspondientes a los recuperatorios.

Esto permite evitar cálculos manuales y mantener un procedimiento uniforme para todos los alumnos.

### Generación del reporte

Una vez finalizado el procesamiento, el programa genera un archivo Excel con la información procesada y los resultados obtenidos.

El archivo final conserva las hojas y estructuras necesarias para continuar con el proceso académico.

El nombre del archivo final se genera tomando como referencia el **nombre del archivo de inasistencias utilizado como entrada**.

## Flujo de procesamiento

El programa sigue diferentes etapas durante su ejecución:

1. **Elegir archivos**
2. **Validar archivos**
3. **Validar contenido**
4. **Calcular**
5. **Comparar**
6. **Crear reporte**

El avance se muestra mediante una interfaz gráfica para que el usuario pueda conocer en qué etapa se encuentra el procesamiento.

## Control de calidad de datos

Uno de los objetivos del proyecto es incorporar controles que permitan detectar inconsistencias antes de generar el resultado final.

Entre los controles implementados se encuentran:

- Validación de DNI.
- Normalización de nombres.
- Detección de alumnos no encontrados.
- Detección de coincidencias ambiguas.
- Comparación de información entre archivos.
- Validación de notas.
- Control de datos de asistencia.
- Identificación de diferencias entre registros.

Estos controles permiten detectar posibles problemas en los archivos de origen antes de continuar con el procesamiento.

## Interfaz gráfica

La aplicación cuenta con una interfaz desarrollada con `Tkinter`.

Durante el procesamiento se muestra una ventana de progreso con las diferentes etapas de ejecución, permitiendo al usuario visualizar el avance de la tarea.

El procesamiento se realiza utilizando hilos (`threading`) y una cola (`queue`) para evitar que la interfaz quede bloqueada mientras se procesan los archivos.

## Estructura general

El proyecto se encuentra organizado para separar las diferentes funciones relacionadas con:

- Lectura de archivos.
- Extracción y normalización de datos.
- Validación.
- Comparación de alumnos.
- Cálculo de recuperatorios.
- Generación de reportes.
- Interfaz gráfica.

Esta organización facilita el mantenimiento y la incorporación de nuevas funcionalidades.

## Uso

Para utilizar la herramienta:

1. Ejecutar el programa.
2. Seleccionar los archivos solicitados.
3. Esperar la validación de los archivos y su contenido.
4. Revisar los controles realizados por el sistema.
5. Ejecutar el procesamiento.
6. Obtener el archivo final generado.

## Proyecto

Este repositorio forma parte de un proyecto más amplio de automatización de procesos académicos.

La idea es dividir el procesamiento en diferentes etapas independientes, permitiendo que cada herramienta tenga una función específica y pueda evolucionar de manera separada.

## Autor

**Francisco Lombroni**

Proyecto desarrollado como parte de un proceso de aprendizaje y desarrollo de herramientas orientadas a la automatización, procesamiento y control de calidad de datos mediante Python.
