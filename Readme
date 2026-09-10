# Automatización para el Cálculo de Recuperatorios

Aplicación desarrollada en Python para automatizar el procesamiento de información académica correspondiente a una segunda etapa de cursada.

El programa integra información proveniente de archivos de **notas** e **inasistencias**, realiza controles de consistencia entre ambas fuentes, calcula los resultados correspondientes a los recuperatorios y genera un archivo final con la información procesada y diferentes controles de calidad.

El proyecto busca reducir tareas manuales y repetitivas, mejorar la confiabilidad del procesamiento y facilitar la detección de diferencias o inconsistencias en los datos.

---

## Objetivo

Automatizar el proceso de generación de información correspondiente a la **segunda etapa de cursada**, evitando el procesamiento manual de los archivos y centralizando en una única herramienta:

* Validación de los archivos de entrada.
* Validación del contenido.
* Identificación y comparación de alumnos.
* Control de DNI.
* Control de notas.
* Cálculo de recuperatorios.
* Control de inasistencias.
* Identificación de alumnos libres.
* Identificación de alumnos regulares que exceden el límite de faltas.
* Generación de observaciones y alertas.
* Generación automática del archivo final.

Además de automatizar los cálculos, el programa incorpora controles destinados a detectar problemas de calidad de los datos antes de generar el resultado final.

---

## Funcionamiento general

El proceso se divide en diferentes etapas:

1. **Elegir archivos**
2. **Validar archivos**
3. **Validar contenido**
4. **Calcular**
5. **Comparar**
6. **Crear reporte**

Durante el procesamiento se muestran estas etapas mediante una ventana de progreso, permitiendo visualizar el avance de la operación.

---

## Archivos de entrada

El programa trabaja con dos archivos principales:

### Archivo de notas

Contiene la información correspondiente a las evaluaciones de los alumnos.

Entre los datos utilizados se encuentran:

* Identificación del alumno.
* DNI.
* TP3.
* TP4.
* PRM1.
* Otras notas necesarias para realizar los controles.

El archivo debe contener la hoja correspondiente al reporte y las estructuras esperadas por el programa.

### Archivo de inasistencias

Contiene la información relacionada con la asistencia de los alumnos.

Se utilizan las hojas:

* `REPORTE`
* `INAS`
* `INAS2`

La hoja `REPORTE` contiene, entre otros datos, la información de `PRM1` utilizada durante el proceso de comparación.

---

## Validación de archivos

Antes de comenzar el procesamiento, el programa verifica que los archivos seleccionados sean compatibles con el proceso.

Se controla, entre otros aspectos:

* Que los archivos puedan abrirse correctamente.
* Que las hojas necesarias estén presentes.
* Que se encuentren las columnas requeridas.
* Que las estructuras de los archivos sean compatibles con el procesamiento.

Si se detecta un problema, el proceso se detiene y se informa la situación en lugar de generar un resultado potencialmente incorrecto.

---

## Validación y control de datos

Uno de los objetivos principales del programa es evitar que errores en los archivos de origen pasen inadvertidos.

### Identificación de alumnos

Para relacionar la información de los distintos archivos, el programa utiliza principalmente el **DNI**.

Cuando es necesario, también realiza una comparación mediante el nombre normalizado del alumno.

La normalización contempla situaciones como:

* Mayúsculas y minúsculas.
* Acentos.
* Signos de puntuación.
* Espacios innecesarios.
* Números correspondientes al DNI incluidos dentro del nombre.

Esto permite mejorar la identificación de un mismo alumno cuando la información no está escrita exactamente de la misma manera en los distintos archivos.

También se detectan situaciones como:

* Alumnos que no pudieron ser encontrados.
* Registros duplicados.
* Coincidencias ambiguas.
* Diferencias entre los DNI de los archivos.

---

## Control de notas

El programa valida las notas utilizadas durante el procesamiento.

Se consideran válidos:

* Valores enteros entre `0` y `10`.
* La letra `A`.
* Celdas vacías cuando corresponde.

Se rechazan valores que no cumplen con el formato esperado, como notas decimales o textos no válidos.

Además, se realizan controles entre las notas presentes en los distintos archivos para detectar modificaciones.

### Control visual

La hoja `OBS` contiene una sección denominada:

**CONTROL DE NOTAS**

Cuando no se detectan diferencias, se informa:

`MATERIA SIN CAMBIOS`

Cuando se detectan modificaciones, se detallan los alumnos y los valores correspondientes para facilitar la revisión.

---

## Control de diferencias de DNI

El programa compara la identificación de los alumnos entre los archivos utilizados durante el procesamiento.

Cuando encuentra diferencias, estas se registran en una sección independiente:

**DIFERENCIAS DE DNI**

Se informa, según corresponda:

* Alumno.
* DNI encontrado en cada archivo.
* Información necesaria para identificar el origen de la diferencia.

Esto permite detectar rápidamente posibles errores de identificación.

Si no se encuentran diferencias, también se informa:

`MATERIA SIN CAMBIOS`

De esta manera, el control de DNI se mantiene separado del control de notas, ya que ambos verifican aspectos diferentes de la información.

---

## Control de inasistencias

El programa utiliza la información de `INAS` e `INAS2` para realizar el control de asistencia.

Se calcula la diferencia entre ambas fuentes:

**Diferencia de inasistencias = INAS2 - INAS**

También se detectan diferencias negativas, que pueden indicar inconsistencias que requieren revisión.

Los resultados se presentan en la sección:

**CONTROL DE INASISTENCIAS**

Cuando corresponde, se informa el alumno y los valores encontrados en cada archivo.

---

## Cálculo de PRM2

El programa calcula la segunda instancia de recuperatorio a partir de las calificaciones de TP3 y TP4.

La fórmula utilizada es:

```text
PRM2 = (TP3 + TP4) / 2
```

El resultado se incorpora al reporte generado por el programa.

---

## Identificación de alumnos libres

A partir del resultado de `PRM2`, el programa identifica a los alumnos que no alcanzan el valor mínimo establecido.

Cuando:

```text
PRM2 < 4
```

el alumno es identificado como **libre**.

Estos alumnos son incorporados a la hoja:

`LIB`

Además, sus registros son resaltados en el reporte para facilitar su identificación.

Si no existen alumnos libres, la hoja informa:

`MATERIA SIN ALUMNOS LIBRES`

---

## Control de alumnos regulares

Para los alumnos que alcanzan el mínimo requerido en `PRM2`, también se controla la cantidad de inasistencias.

Si un alumno regular supera el límite de faltas establecido, se lo identifica mediante la observación:

`ALUMNO REGULAR EXCEDIDO EN FALTAS`

Esto permite diferenciar los resultados obtenidos a partir de las notas de aquellos derivados del control de asistencia.

---

## Hoja OBS

La hoja `OBS` concentra los principales controles realizados durante el procesamiento.

Contiene:

* **CONTROL DE NOTAS**
* **DIFERENCIAS DE DNI**
* **CONTROL DE INASISTENCIAS**

Además de mostrar las diferencias encontradas, la hoja utiliza colores para facilitar una revisión rápida.

### 🟩 Verde — Sin cambios

Cuando un control no detecta diferencias, la sección correspondiente se muestra con fondo verde y contiene:

`MATERIA SIN CAMBIOS`

### 🟥 Rojo — Con modificaciones

Cuando se detectan diferencias o modificaciones, la sección correspondiente se muestra con fondo rojo y contiene el detalle de los registros que requieren revisión.

Este sistema permite identificar visualmente, sin necesidad de revisar todo el contenido del reporte, qué controles requieren atención.

---

## Archivo de salida

El archivo final se genera tomando como base el **nombre del archivo de inasistencias**.

La generación del nombre sigue la siguiente lógica:

1. Se toma el nombre del archivo de inasistencias.
2. La terminación `1ET` se reemplaza por `2ET`.
3. Se agrega al final la fecha correspondiente en formato:

```text
MMDD
```

Por ejemplo, si el archivo de entrada corresponde a una primera etapa, el archivo generado pasa a identificarse como correspondiente a la **segunda etapa**, incorporando además el mes y día de generación.

De esta manera, el nombre del archivo final permite identificar automáticamente:

* La etapa del proceso.
* El período de generación.

El archivo original de inasistencias no se utiliza como archivo de salida directo, evitando modificar la fuente original.

---

## Flujo del procesamiento

El funcionamiento general puede representarse de la siguiente manera:

```text
                 ARCHIVO DE NOTAS
                        │
                        │
                        ▼
              ┌───────────────────┐
              │ Validación de     │
              │ archivos y datos  │
              └─────────┬─────────┘
                        │
                        │
                 ARCHIVO DE
                 INASISTENCIAS
                        │
                        ▼
              ┌───────────────────┐
              │ Identificación y  │
              │ comparación de    │
              │ alumnos           │
              └─────────┬─────────┘
                        │
                        ▼
              ┌───────────────────┐
              │ Control de notas  │
              │ y diferencias DNI │
              └─────────┬─────────┘
                        │
                        ▼
              ┌───────────────────┐
              │ Cálculo de PRM2   │
              └─────────┬─────────┘
                        │
                        ▼
              ┌───────────────────┐
              │ Control de        │
              │ inasistencias     │
              └─────────┬─────────┘
                        │
                        ▼
              ┌───────────────────┐
              │ Identificación de │
              │ alumnos libres y  │
              │ regulares         │
              └─────────┬─────────┘
                        │
                        ▼
              ┌───────────────────┐
              │ Generación de     │
              │ reportes y OBS    │
              └─────────┬─────────┘
                        │
                        ▼
                  ARCHIVO 2ETMMDD
```

---

## Tecnologías utilizadas

* **Python**
* **Tkinter** — interfaz gráfica.
* **OpenPyXL** — lectura, modificación y generación de archivos Excel.
* **Threading** — ejecución del procesamiento sin bloquear la interfaz.
* **Queue** — comunicación entre el procesamiento y la interfaz gráfica.

---

## Características técnicas

El proyecto incorpora diferentes conceptos de automatización y procesamiento de datos:

* Lectura y escritura de archivos Excel.
* Validación de estructuras.
* Validación de datos.
* Normalización de información.
* Comparación de múltiples fuentes.
* Detección de inconsistencias.
* Aplicación de reglas de negocio.
* Cálculos automáticos.
* Generación de reportes.
* Formateo automático de hojas.
* Identificación visual de errores y diferencias.
* Manejo de excepciones.
* Procesamiento mediante hilos para mantener una interfaz fluida.

---

## Instalación

Clonar el repositorio:

```bash
git clone https://github.com/florcisco/Automatizacion-Calculo-Recuperatorios.git
```

Ingresar al directorio:

```bash
cd Automatizacion-Calculo-Recuperatorios
```

Instalar las dependencias necesarias:

```bash
pip install openpyxl
```

Tkinter forma parte de las instalaciones habituales de Python para Windows.

---

## Ejecución

Ejecutar el archivo principal del programa desde Python.

```bash
python nombre_del_programa.py
```

El programa abrirá la interfaz gráfica y permitirá seleccionar los archivos de entrada.

Una vez seleccionados, el procesamiento se realiza siguiendo las diferentes etapas mostradas en la ventana de progreso.

---

## Resultado

El resultado final es un archivo Excel preparado para continuar con el proceso académico.

El archivo contiene la información procesada, los cálculos correspondientes y los controles necesarios para revisar posibles inconsistencias.

La información de control queda centralizada en `OBS`, mientras que los alumnos identificados como libres se registran en `LIB`.

La utilización de colores en `OBS` permite realizar una revisión rápida del estado de cada control:

```text
VERDE  → MATERIA SIN CAMBIOS
ROJO   → EXISTEN DIFERENCIAS / MODIFICACIONES
```

---

## Propósito del proyecto

Este proyecto forma parte de una serie de herramientas desarrolladas para automatizar procesos administrativos y académicos que anteriormente requerían una considerable cantidad de trabajo manual.

El enfoque no está únicamente puesto en realizar cálculos, sino en construir un proceso completo que incluya:

**automatización → procesamiento → validación → control de calidad → aplicación de reglas → generación de resultados**

De esta manera, el programa busca reducir tareas repetitivas, disminuir errores derivados de la manipulación manual de información y facilitar la revisión de los resultados obtenidos.

---

## Autor

**Francisco Lombroni**

Proyecto desarrollado como parte de un conjunto de herramientas de automatización y procesamiento de información académica.
