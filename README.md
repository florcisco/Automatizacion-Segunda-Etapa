# Automatización del Procesamiento Académico — Segunda Etapa

Herramienta desarrollada en **Python** para automatizar el procesamiento, validación y comparación de información académica proveniente de diferentes archivos de Excel, con el objetivo de determinar automáticamente las condiciones correspondientes a la **segunda etapa de evaluación** y generar un reporte final.

Este repositorio forma parte de un proyecto de automatización dividido en diferentes etapas, donde cada una cumple una función específica dentro del proceso general.

**Proyecto de automatización académica — Etapa 2 de 4**

---

## 🎯 Objetivo

El objetivo de esta segunda etapa es automatizar un proceso que requiere combinar información proveniente de diferentes fuentes, validar que los datos sean consistentes y realizar los cálculos necesarios para determinar las condiciones académicas de cada alumno.

La herramienta permite:

* Procesar múltiples archivos de Excel.
* Validar la estructura de los archivos antes de comenzar.
* Identificar alumnos utilizando diferentes fuentes de información.
* Comparar registros mediante DNI y nombre.
* Detectar diferencias e inconsistencias entre archivos.
* Normalizar nombres y datos para facilitar las coincidencias.
* Validar notas e inasistencias.
* Calcular automáticamente el promedio correspondiente a la segunda instancia.
* Aplicar las reglas necesarias para determinar las condiciones académicas.
* Generar automáticamente un archivo Excel final.
* Mostrar el progreso del procesamiento mediante una interfaz gráfica.

El objetivo principal es **reducir tareas manuales, disminuir errores y mantener un procedimiento uniforme para el procesamiento de la información**.

---

# 📚 El proyecto completo

Esta herramienta forma parte de un proyecto de automatización académica que se está desarrollando progresivamente en **cuatro etapas**.

Cada etapa automatiza una parte específica del proceso:

```text
┌──────────────────────────────┐
│       PRIMERA ETAPA          │
│                              │
│ Procesamiento inicial        │
│ Validación de información    │
│ Generación de reportes       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       SEGUNDA ETAPA          │
│                              │
│ Integración de información   │
│ Validación y comparación     │
│ Cálculos                     │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       TERCERA ETAPA          │
│                              │
│ Procesamiento de             │
│ recuperatorios               │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│       CUARTA ETAPA           │
│                              │
│ Determinación de             │
│ condiciones finales          │
└──────────────────────────────┘
```

Las etapas 3 y 4 se desarrollarán posteriormente y tendrán como objetivo continuar el procesamiento de la información generada en las etapas anteriores.

### Evolución prevista

Una vez que todas las etapas funcionen correctamente de manera independiente, el objetivo a futuro es evaluar su integración en una **única aplicación**, manteniendo cada etapa como un módulo independiente dentro del sistema.

La integración se realizará una vez finalizado y validado el funcionamiento individual de cada etapa.

---

# 🔗 Relación con la Primera Etapa

La Segunda Etapa utiliza información generada durante la Primera Etapa y continúa el procesamiento a partir de esos resultados.

Entre los archivos generados durante la Primera Etapa se encuentra `REG 2ET`, que forma parte del flujo de información utilizado posteriormente.

### Flujo entre ambas etapas

```text
PRIMERA ETAPA
      │
      │ Procesamiento inicial
      │
      ▼
Información procesada
      +
REG 2ET
      │
      ▼
SEGUNDA ETAPA
      │
      ├── Validación
      ├── Normalización
      ├── Comparación
      ├── Cálculos
      └── Generación del reporte
```

👉 [Ir a la Primera Etapa](../Automatizacion-Procesamiento-Primera-Etapa)

---

# 📂 Archivos de entrada

La herramienta trabaja con archivos Excel que contienen información académica proveniente de diferentes fuentes.

Entre los datos procesados se encuentran:

* Información de alumnos.
* DNI.
* Nombres y apellidos.
* Inasistencias.
* Notas de evaluaciones.
* Información correspondiente a la primera instancia.
* Información correspondiente a la segunda instancia.
* Promedios.
* Datos necesarios para determinar las condiciones académicas.

Los archivos utilizados pueden encontrarse en formatos como:

* `.xlsx`
* `.xlsm`

Antes de comenzar el procesamiento, el programa verifica que los archivos seleccionados sean los correspondientes y que posean la estructura esperada.

---

# 🔎 Validación de archivos

Una de las primeras etapas del proceso consiste en verificar que los archivos seleccionados puedan ser procesados correctamente.

El programa controla aspectos como:

* Tipo de archivo.
* Existencia de las hojas necesarias.
* Estructura esperada.
* Disponibilidad de la información requerida.
* Correspondencia entre los archivos seleccionados.

Entre las hojas utilizadas durante el procesamiento se encuentran, según el archivo:

* `REPORTE`
* `INAS`
* `INAS2`
* `PRM1`

Esto permite detectar problemas en los archivos de origen antes de realizar cálculos o generar el resultado final.

---

# 🧹 Normalización e identificación de alumnos

Uno de los principales desafíos del proceso es identificar correctamente a un mismo alumno cuando la información proviene de diferentes archivos.

Para resolverlo, la herramienta utiliza diferentes mecanismos de identificación.

## DNI

El sistema intenta extraer el DNI incluso cuando aparece acompañado de texto.

Por ejemplo:

```text
DNI 12345678
```

puede ser interpretado como:

```text
12345678
```

El DNI constituye el principal criterio utilizado para relacionar registros.

## Nombre

Cuando no es posible encontrar una coincidencia mediante DNI, se utiliza el nombre normalizado como criterio alternativo.

Para facilitar esta comparación se realizan transformaciones como:

* Eliminación de acentos.
* Eliminación de caracteres especiales.
* Eliminación de información adicional.
* Conversión a un formato uniforme.
* Eliminación de espacios innecesarios.
* Normalización de mayúsculas y minúsculas.

De esta manera, nombres escritos de formas ligeramente diferentes pueden ser comparados de manera más robusta.

---

# 🔄 Comparación y conciliación de información

La herramienta no solamente busca alumnos, sino que también compara la información disponible en los diferentes archivos.

El proceso prioriza:

```text
DNI
 ↓
Coincidencia por DNI
 ↓
Si no existe:
 ↓
Nombre normalizado
```

Cuando una coincidencia por nombre puede corresponder a más de un registro, el sistema **no selecciona arbitrariamente un alumno**, sino que identifica la situación como ambigua para permitir su revisión.

Esto permite reducir el riesgo de asociar información de un alumno incorrecto.

---

# ⚠️ Detección de inconsistencias

Durante la comparación pueden detectarse situaciones como:

* Alumnos presentes en un archivo y ausentes en otro.
* Diferencias de DNI.
* Coincidencias realizadas mediante nombre.
* Coincidencias ambiguas.
* Diferencias entre los datos de distintos archivos.
* Diferencias entre registros de notas.
* Diferencias relacionadas con las inasistencias.

Estas situaciones forman parte del control de calidad de los datos.

---

# 📊 Validación de notas

Las notas son procesadas antes de realizar los cálculos.

El sistema contempla diferentes situaciones:

* Valores numéricos.
* Valores decimales.
* Celdas vacías.
* Valores fuera de rango.
* Formatos inválidos.
* Categorías especiales.

## Categoría `A`

El valor `A` forma parte de la lógica original del proceso y se considera **válido durante la etapa de validación**.

Cuando una nota debe utilizarse posteriormente en un cálculo numérico, la categoría:

```text
A
```

se transforma en:

```text
0
```

Esta conversión no representa un error en los datos, sino una **regla de negocio definida para el procesamiento**.

Por lo tanto:

```text
Validación → A es un valor válido
Cálculo     → A se convierte en 0
```

Esto permite mantener la información original durante las validaciones y, al mismo tiempo, utilizar un valor numérico cuando es necesario realizar operaciones matemáticas.

---

# 📝 Comparación de evaluaciones

La herramienta también permite comparar información correspondiente a diferentes evaluaciones entre las distintas fuentes.

Entre los datos analizados se encuentran:

* `TP1`
* `TP2`
* `TP3`
* `TP4`
* `PRM1`

La información se normaliza antes de realizar las comparaciones para reducir diferencias provocadas únicamente por formatos distintos.

---

# 🧮 Cálculo de la segunda instancia

Una de las funciones principales de esta etapa es calcular automáticamente el promedio correspondiente a las evaluaciones de la segunda instancia.

Para ello se utiliza:

```text
PRM2 = (TP3 + TP4) / 2
```

El cálculo se realiza después de validar y normalizar los datos necesarios.

A partir de esta información, el programa continúa con la determinación de las condiciones correspondientes a cada alumno.

---

# 📋 Cruce con información de asistencia

Además de las notas, la herramienta incorpora información relacionada con las inasistencias.

Esto permite combinar diferentes dimensiones de la información académica:

```text
                 ┌─────────────┐
                 │    Notas    │
                 └──────┬──────┘
                        │
                        ▼
                 ┌─────────────┐
                 │  PRM1/PRM2  │
                 └──────┬──────┘
                        │
                        │
┌──────────────┐        │        ┌────────────────┐
│ Inasistencias│────────┼────────│ Identificación │
└──────────────┘        │        │    alumno      │
                        │        └────────────────┘
                        ▼
                ┌─────────────────┐
                │   Condición     │
                │    académica    │
                └─────────────────┘
```

De esta forma, la determinación final no depende únicamente de las notas, sino que considera también la información de asistencia y las reglas definidas para el proceso.

---

# ⚙️ Flujo de procesamiento

La aplicación organiza el proceso en diferentes etapas:

### 1. Elegir archivos

El usuario selecciona los archivos necesarios mediante la interfaz gráfica.

### 2. Validar archivos

Se verifica que los archivos seleccionados sean correctos y tengan la estructura esperada.

### 3. Validar contenido

Se revisan los datos contenidos en los archivos:

* DNI.
* Nombres.
* Notas.
* Inasistencias.
* Estructuras internas.
* Datos necesarios para los cálculos.

### 4. Calcular

Se realizan los cálculos correspondientes, incluyendo el promedio `PRM2`.

### 5. Comparar

Se cruzan los datos provenientes de los diferentes archivos y se detectan inconsistencias.

### 6. Crear reporte

Finalmente se genera el archivo Excel con la información procesada y las condiciones determinadas.

---

# 🖥️ Interfaz gráfica

La aplicación cuenta con una interfaz gráfica desarrollada utilizando **Tkinter**.

El usuario puede seleccionar los archivos necesarios sin tener que modificar directamente el código.

Durante la ejecución se muestra el progreso del procesamiento mediante diferentes estados:

```text
Elegir archivos
       ↓
Validar archivos
       ↓
Validar contenido
       ↓
Calcular
       ↓
Comparar
       ↓
Crear reporte
```

Esto permite conocer en qué etapa se encuentra el procesamiento.

---

# 🚀 Procesamiento en segundo plano

Para evitar que la interfaz gráfica quede bloqueada durante el procesamiento de los archivos, se utilizan:

* `threading`
* `queue`

De esta manera, las tareas de procesamiento pueden ejecutarse sin bloquear la interfaz principal.

Este enfoque permite mejorar la interacción con la aplicación, especialmente cuando el procesamiento requiere trabajar con múltiples archivos y una cantidad considerable de registros.

---

# 📄 Generación del reporte

Una vez finalizado el procesamiento, el programa genera automáticamente un archivo Excel con la información resultante.

El archivo final contiene la información necesaria para continuar con el proceso académico y conserva las estructuras requeridas por el flujo de trabajo.

El nombre del archivo generado se construye tomando como referencia el archivo de inasistencias utilizado como entrada.

---

# 🛡️ Control de calidad de datos

El control de calidad es una parte fundamental de esta etapa.

Antes de generar el resultado final, el sistema busca detectar problemas como:

* DNI inválidos o inconsistentes.
* Alumnos no encontrados.
* Nombres que requieren normalización.
* Coincidencias ambiguas.
* Diferencias entre archivos.
* Notas inválidas.
* Datos faltantes.
* Inasistencias inconsistentes.
* Diferencias entre evaluaciones.

La idea no es solamente automatizar los cálculos, sino también **automatizar parte del proceso de control y conciliación de información**.

---

# 🧰 Tecnologías utilizadas

### Python

Lenguaje principal utilizado para desarrollar toda la aplicación.

### Tkinter

Utilizado para construir la interfaz gráfica y permitir la selección de archivos y visualización del progreso.

### OpenPyXL

Utilizado para leer, procesar y generar archivos de Excel.

### Pandas

Utilizado para facilitar el procesamiento y manipulación de los datos.

### Threading

Utilizado para ejecutar tareas de procesamiento sin bloquear la interfaz gráfica.

### Queue

Utilizado para facilitar la comunicación entre el procesamiento y la interfaz.

---

# 📁 Estructura del proyecto

Actualmente, el proyecto se concentra principalmente en el archivo:

```text
Automatizacion-Segunda-Etapa/
│
├── Procesador_Segunda_Etapa.py
│
└── README.md
```

El archivo principal contiene la lógica necesaria para:

* Lectura de archivos.
* Validación.
* Normalización.
* Identificación de alumnos.
* Comparación de registros.
* Procesamiento de notas.
* Procesamiento de inasistencias.
* Cálculos.
* Determinación de condiciones.
* Generación del reporte.
* Interfaz gráfica.

---

# ▶️ Cómo utilizarlo

## 1. Clonar el repositorio

```bash
git clone https://github.com/florcisco/Automatizacion-Segunda-Etapa.git
```

## 2. Ingresar al directorio

```bash
cd Automatizacion-Segunda-Etapa
```

## 3. Instalar las dependencias

Las principales bibliotecas utilizadas son:

```bash
pip install openpyxl pandas
```

`tkinter`, `threading` y `queue` forman parte de la biblioteca estándar de Python en las instalaciones habituales.

## 4. Ejecutar el programa

```bash
python Procesador_Segunda_Etapa.py
```

## 5. Seleccionar los archivos

La interfaz solicitará los archivos necesarios para realizar el procesamiento.

## 6. Ejecutar el procesamiento

El programa realizará automáticamente:

```text
Validación
    ↓
Normalización
    ↓
Comparación
    ↓
Cálculos
    ↓
Control de información
    ↓
Generación del reporte
```

---

# 🔗 Etapas del proyecto

Actualmente el proyecto está planteado en cuatro etapas.

### 1️⃣ Primera Etapa

Procesamiento inicial de la información académica y generación de los archivos necesarios para continuar el proceso.

👉 [Ir a la Primera Etapa](../Automatizacion-Procesamiento-Primera-Etapa)

### 2️⃣ Segunda Etapa — Este repositorio

Integración de diferentes fuentes, validación, comparación de registros, cálculo de la segunda instancia y generación del reporte correspondiente.

### 3️⃣ Tercera Etapa — Próximamente

Procesamiento de la información correspondiente a los recuperatorios.

### 4️⃣ Cuarta Etapa — Próximamente

Integración de los resultados obtenidos y determinación de las condiciones académicas finales.

---

# 🔮 Integración futura

El objetivo inmediato del proyecto es desarrollar y validar cada etapa de manera independiente.

Una vez que las cuatro etapas estén funcionando correctamente, se evaluará la posibilidad de integrarlas en una única aplicación.

La idea sería pasar progresivamente de:

```text
Programa Etapa 1
Programa Etapa 2
Programa Etapa 3
Programa Etapa 4
```

a una aplicación unificada:

```text
┌─────────────────────────────────────┐
│      AUTOMATIZACIÓN ACADÉMICA       │
│                                     │
│  Primera Etapa                      │
│  Segunda Etapa                      │
│  Recuperatorios                     │
│  Condiciones Finales                │
│                                     │
│  Ejecutar proceso completo          │
└─────────────────────────────────────┘
```

Esta integración se realizará **después de validar individualmente cada etapa**, evitando agregar complejidad antes de comprobar que cada parte del proceso funciona correctamente.

---

# 🔄 Evolución del proyecto

El proyecto se está desarrollando de manera incremental a partir de una necesidad concreta de automatización.

La evolución prevista puede resumirse de la siguiente manera:

```text
Proceso manual
      ↓
Automatización de tareas repetitivas
      ↓
Primera etapa
      ↓
Segunda etapa
      ↓
Recuperatorios
      ↓
Condiciones finales
      ↓
Integración de las etapas
      ↓
Aplicación completa
```

Este enfoque permite probar y validar cada componente antes de integrarlo en un sistema único.

---

# 💡 Posibles mejoras

Como evolución futura del proyecto, algunas mejoras posibles serían:

* Integrar las cuatro etapas en una única aplicación.
* Separar la lógica en diferentes módulos.
* Incorporar pruebas automatizadas.
* Mejorar el sistema de registro de errores.
* Agregar archivos de configuración.
* Incorporar una vista más detallada de las inconsistencias detectadas.
* Permitir revisar manualmente coincidencias ambiguas desde la interfaz.
* Incorporar validaciones adicionales según nuevas reglas académicas.
* Mejorar la documentación técnica del código.
* Incorporar un sistema de registro de las ejecuciones realizadas.

Estas mejoras se evaluarán una vez finalizado y validado el funcionamiento independiente de las distintas etapas.

---

# 🎯 ¿Qué problema resuelve?

El valor principal de esta herramienta no está solamente en calcular un promedio.

El proceso automatiza una tarea que requiere **integrar, validar y reconciliar información proveniente de diferentes archivos antes de obtener un resultado confiable**.

En términos generales:

```text
Múltiples archivos
        ↓
Datos con diferentes formatos
        ↓
Identificación de alumnos
        ↓
Normalización
        ↓
Validación
        ↓
Comparación
        ↓
Cálculos
        ↓
Control de inconsistencias
        ↓
Reporte
```

Esto permite reducir trabajo manual y establecer un procedimiento reproducible para el procesamiento de la información académica.

---

# 👤 Autor

**Francisco Lombroni**

Proyecto desarrollado como parte de un proceso de aprendizaje y desarrollo de herramientas orientadas a:

* Automatización de procesos.
* Procesamiento de datos.
* Validación y control de calidad.
* Integración de información.
* Desarrollo de aplicaciones en Python.

---

## 📌 Proyecto de automatización académica

**Primera Etapa → Segunda Etapa → Recuperatorios → Condiciones finales → Integración**

Este repositorio representa la **Segunda Etapa** del proceso.
