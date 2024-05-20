# Lectura de Archivo desde una Tarjeta SD con Arduino

Este programa demuestra cómo leer un archivo de texto desde una tarjeta SD utilizando un Arduino. Utiliza las bibliotecas `SPI` y `SD` para manejar la comunicación con la tarjeta SD y leer su contenido.

## Código

```cpp
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>

File myFile;

void setup() {
    Serial.begin(115200);
    Serial.print("Iniciando SD ...");

    if (!SD.begin(5)) {
        Serial.println("No se pudo inicializar");
        return;
    }

    Serial.println("inicializacion exitosa");
    myFile = SD.open("/archivo.txt"); // abrimos el archivo

    if (myFile) {
        Serial.println("archivo.txt:");
        while (myFile.available()) {
            Serial.write(myFile.read());
        }
        myFile.close(); // cerramos el archivo
    } else {
        Serial.println("Error al abrir el archivo");
    }
}

void loop() {
    // El loop principal no se utiliza en este ejemplo
}

##Objetivo
El objetivo de este programa es leer el contenido de un archivo de texto llamado archivo.txt desde una tarjeta SD y mostrar su contenido en el monitor serial.

##Funcionamiento

***Inicialización en setup():***

- Serial.begin(115200): Inicia la comunicación serial a una velocidad de 115200 baudios.
- Intenta inicializar la tarjeta SD llamando a SD.begin(5).
- Si la inicialización falla, imprime un mensaje de error y detiene el programa.
- Si la inicialización es exitosa, imprime un mensaje de éxito.
- Intenta abrir el archivo archivo.txt llamando a SD.open("/archivo.txt").
- Si el archivo se abre correctamente, lee su contenido y lo imprime en el monitor serial.
- Si no se puede abrir el archivo, imprime un mensaje de error.


***Lectura de Archivo:***

- while (myFile.available()): Lee byte a byte el contenido del archivo mientras haya datos disponibles.
- Serial.write(myFile.read()): Escribe cada byte leído del archivo en el monitor serial.
- myFile.close(): Cierra el archivo después de haber leído todo su contenido.
- Explicación de las Funciones Clave
- SD.begin(5): Inicializa la tarjeta SD. El argumento 5 especifica el pin de selección del chip (CS).
- SD.open("/archivo.txt"): Abre el archivo archivo.txt en la tarjeta SD para lectura.
- myFile.available(): Devuelve el número de bytes disponibles para leer desde el archivo.
- myFile.read(): Lee un byte desde el archivo.
- myFile.close(): Cierra el archivo.

***Uso Práctico***
Este programa es útil para aplicaciones que requieren leer datos almacenados en una tarjeta SD, como la lectura de configuraciones, registros de datos o cualquier tipo de almacenamiento de datos persistente. Es una base para proyectos que implican el uso de almacenamiento externo en tarjetas SD.

Este programa proporciona un ejemplo sencillo y efectivo de cómo interactuar con una tarjeta SD desde un Arduino, leyendo archivos de texto y mostrando su contenido a través del monitor serial.