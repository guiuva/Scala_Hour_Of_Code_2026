#  Taller Introductorio de Scala para Big Data

Organizado por el **Grupo Universitario de Informática (GUI)**.

* **Ponente:** Manuel Méndez Calvo ([manuel.men.calvo@gmail.com](mailto:manuel.men.calvo@gmail.com))
* **Fecha:** 24/11/2026
* **Duración estimada:** 1,5 horas
* **Modalidad:** Práctica con portátil propio

---

## 📖 Descripción y público objetivo

Este es un taller introductorio a **Scala**, un lenguaje multiparadigma con un fuerte enfoque en la **programación funcional**, ampliamente utilizado en el ecosistema de procesamiento distribuido y Big Data.

* **¿A quién va dirigido?** A cualquier persona que cuente con **conocimientos básicos de programación** y quiera aprender las bases del lenguaje.
* **Continuidad:** Este taller sienta las bases necesarias y es el paso previo ideal para aprovechar al máximo el *Taller introductorio de Spark Scala*.

---

##  Requisitos previos e instalación

Para seguir el taller necesitaremos tener instalado **Java (JDK)**, el entorno de desarrollo **IntelliJ IDEA** y el soporte para **Scala**. Además, incluimos los pasos para dejar configurado **Apache Spark** mediante SBT por si quieres trastear por tu cuenta o asistir al siguiente taller.

### 1. Instalar JDK (versión 11 o 17)
Asegúrate de tener instalado el JDK 11 o 17. Puedes comprobar qué versión tienes ejecutando en tu terminal:

```bash
java -version
```

Si no lo tienes instalado o tienes una versión distinta, descarga e instala **JDK 11** o **JDK 17** (por ejemplo, desde [Adoptium Temurin](https://adoptium.net/)).

### 2. Instalar IntelliJ IDEA
Descarga e instala IntelliJ IDEA desde la [página oficial de JetBrains](https://www.jetbrains.com/idea/download/).
> **Nota:** Al instalarlo dispondrás de una prueba gratuita de 30 días de la edición completa; una vez finalizada, puedes seguir utilizándolo de forma gratuita con las funcionalidades básicas (suficientes para el taller).

### 3. Instalar el plugin de Scala
1. Abre **IntelliJ IDEA**.
2. Ve a **File > Settings** (o `IntelliJ IDEA > Settings` en macOS).
3. Entra en el apartado **Plugins** y busca **"Scala"** en la pestaña *Marketplace*.
4. Haz clic en **Install** y **reinicia IntelliJ** cuando termine la instalación.

### 4. Crear el proyecto con SBT
1. En IntelliJ, selecciona **New Project**.
2. Elige **Scala** en el menú izquierdo y ponle el nombre que quieras al proyecto.
3. En **Build System**, selecciona **SBT**.
4. En **JDK**, selecciona la versión **11** o **17**.
5. En **Scala**, selecciona preferiblemente la versión **`2.12.18`**.
6. Haz clic en **Create**.

---

## ⚡ Configuración opcional (Recomendada para el taller de Spark)

Si quieres dejar tu entorno listo para probar Apache Spark desde ya (o para venir al taller avanzado), sigue estos dos pasos adicionales:

### 5. Añadir dependencias en `build.sbt`
En el panel izquierdo de IntelliJ, abre el archivo `build.sbt` y sustituye su contenido por el siguiente:

```scala
name := "taller-spark-scala"
version := "0.1"
scalaVersion := "2.12.18"

val sparkVersion = "3.5.0" // Valdría cualquier otra a partir de la 3. Lo dejo a vuestra elección

libraryDependencies ++= Seq(
  "org.apache.spark" %% "spark-core" % sparkVersion,
  "org.apache.spark" %% "spark-sql" % sparkVersion
)
```

Tras guardar el archivo, aparecerá un **icono flotante de SBT** en la esquina superior derecha del editor; púlsalo para recargar los cambios y descargar las librerías automáticamente.

### 6. Prueba de funcionamiento ("Hello World")
1. Navega en el panel izquierdo hasta `src > main > scala`.
2. Haz clic derecho sobre `scala`, selecciona **New > Package** y llámalo `com.taller` (o el nombre que prefieras).
3. Haz clic derecho sobre el paquete creado, selecciona **New > Scala Class**, elige el tipo **Object** y llámalo `MainSpark`.
4. Pega el siguiente código y ejecútalo para comprobar que todo funciona:

```scala
package com.taller

import org.apache.spark.sql.SparkSession

object MainSpark {
  def main(args: Array[String]): Unit = {
    // Crear una sesión de Spark ejecutándose en local
    val spark = SparkSession.builder()
      .appName("Test Spark Taller")
      .master("local[*]")
      .getOrCreate()

    println("Hello World")
    println(" ¡SPARK SE HA INICIALIZADO CORRECTAMENTE! ")
    println(s" Versión de Spark: ${spark.version}")
    println("========================================")

    // Pequeña prueba creando un DataFrame con datos dummy
    val datos = Seq(("Ana", 28), ("Carlos", 34), ("Elena", 45))
    import spark.implicits._
    val df = datos.toDF("Nombre", "Edad")

    df.show()

    spark.stop()
  }
}
```

---

## 📬 Contacto y dudas

Si tienes algún problema con la instalación antes del taller, puedes escribir a **Manuel Méndez Calvo**: [manuel.men.calvo@gmail.com](mailto:manuel.men.calvo@gmail.com).
