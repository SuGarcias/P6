# PRACTICA 6 : Buses de comunicación II (SPI)



## 6.1: _LECTURA/ESCRITURA DE MEMORIA SD_

### SPI en ESP32:
| SPI  | MOSI    | MISO    | CLK     | CS      |
| ---- | ------- | ------- | ------- | ------- |
| VSPI | GPIO 23 | GPIO 19 | GPIO 18 | GPIO 5  |
| HSPI | GPIO 13 | GPIO 12 | GPIO 14 | GPIO 15 |

- CÓDIGO:
  
```cpp
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>
File myFile;
void setup()
{
  Serial.begin(9600);
  Serial.print("Iniciando SD ...");
  if (!SD.begin(4)) 
  {
  Serial.println("No se pudo inicializar");
  return;
  }
  Serial.println("inicializacion exitosa");
  myFile = SD.open("archivo.txt");//abrimos el archivo
  if (myFile) 
  {
      Serial.println("archivo.txt:");
      while (myFile.available()) 
      {
        Serial.write(myFile.read());
      }
      myFile.close(); //cerramos el archivo
  } 
  else
  {
    Serial.println("Error al abrir el archivo");
  }
}
void loop()
{

}

```

- SALIDA POR PUERTO SERIE:


Muestra el contenido del archivo que se ha creado 'archivo.txt'.

- FUNCIONAMIENTO:

Primeramente incluimos las librerias de Arduino, la de SPI y la de SD. También creamos una variable de tipo File llamada 'MyFile'

```CPP
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>
File myFile;
```

Ahora en el SetUp inicializamos el Serial y la SD con el .begin, el Serial ponemos el monitor speed a 9600. Para la SD, hacemos una condición if, de que si no se pude hacer el .begin de la SD, que se imprima por el monitor 'No se pudo inicializar', en cambio, si se ha podido realizar bién el .begin, muestra 'inicialización exitosa'.
Después, asignamos a la variable MyFile el archivo de dentro de la SD llamado 'archivo.txt' con la función SD.open().
Hacemos un bucle para que mientras se esté dentro del 'archivo.txt', si Myfile.avialable(), entonces que se escriba por el Serial lo que se lee en el Myfile, es decir, se va a mostra por el monitor lo que hay dentro del 'archivo.txt' que se guarda dentro de la variable MyFile.

```cpp
void setup()
{
  Serial.begin(9600);
  Serial.print("Iniciando SD ...");
  if (!SD.begin(4)) 
  {
  Serial.println("No se pudo inicializar");
  return;
  }
  Serial.println("inicializacion exitosa");
  myFile = SD.open("archivo.txt");//abrimos el archivo
  if (myFile) 
  {
      Serial.println("archivo.txt:");
      while (myFile.available()) 
      {
        Serial.write(myFile.read());
      }
      myFile.close(); //cerramos el archivo
  } 
  else
  {
    Serial.println("Error al abrir el archivo");
  }
}
```
El loop está vacío.
```cpp
void loop()
{

}
```