# 🌱 Smart Campus IoT
### Sistema inteligente de monitoreo ambiental para espacios educativos

**Proyecto escolar de Informática — 6.º año**

Smart Campus IoT es un proyecto basado en el Internet de las Cosas (IoT) que busca monitorear las condiciones ambientales de un espacio educativo mediante sensores conectados a un microcontrolador ESP32-C3. La información obtenida está destinada a facilitar la observación de variables ambientales y la identificación de condiciones que podrían afectar el confort dentro del aula.

El proyecto contempla la lectura de sensores, la visualización local de información, la comunicación mediante MQTT y el desarrollo de un panel web para consultar los datos recopilados.

> **Estado del proyecto:** desarrollo y pruebas. Algunas conexiones, lecturas de sensores y funciones de comunicación todavía requieren verificación.

---

## 📑 Índice

- [1. Descripción del proyecto](#-1-descripción-del-proyecto)
- [2. Problemática](#-2-problemática)
- [3. Objetivos](#-3-objetivos)
- [4. Alcance del proyecto](#-4-alcance-del-proyecto)
- [5. Componentes del sistema](#-5-componentes-del-sistema)
- [6. Arquitectura del sistema](#-6-arquitectura-del-sistema)
- [7. Variables monitoreadas](#-7-variables-monitoreadas)
- [8. Comunicación MQTT](#-8-comunicación-mqtt)
- [9. Estado de desarrollo y pruebas](#-9-estado-de-desarrollo-y-pruebas)
- [10. Estructura del repositorio](#-10-estructura-del-repositorio)
- [11. Instalación y puesta en marcha](#-11-instalación-y-puesta-en-marcha)
- [12. Seguridad informática](#-12-seguridad-informática)
- [13. Mejoras futuras](#-13-mejoras-futuras)
- [14. Equipo de trabajo](#-14-equipo-de-trabajo)
- [15. Documentación y evidencias](#-15-documentación-y-evidencias)
- [16. Licencia](#-16-licencia)

---

## 🔎 1. Descripción del proyecto

Smart Campus IoT propone desarrollar un sistema de monitoreo ambiental para espacios educativos utilizando tecnologías de IoT.

El sistema utiliza un microcontrolador ESP32-C3 como unidad principal, conectado a distintos sensores que permiten obtener información sobre variables como temperatura, humedad, iluminación, sonido, una lectura analógica relacionada con la calidad del aire (las cuales estas conforman el umbral del confort) y presencia.

La información se procesa para generar lecturas que puedan visualizarse localmente y, cuando la comunicación esté implementada y verificada, enviarse a través de MQTT para su consulta desde un panel web.

El proyecto integra conocimientos de programación, electrónica, redes, sistemas embebidos, comunicación entre dispositivos y desarrollo web.

## 🎯 2. Problemática

Las condiciones ambientales de un aula pueden influir en la comodidad y en las condiciones en las que se desarrollan las actividades educativas.

Sin un sistema de monitoreo, conocer estas condiciones puede depender de observaciones ocasionales o mediciones manuales.

Smart Campus IoT busca explorar una alternativa tecnológica que permita recopilar información ambiental mediante sensores y organizarla para facilitar su consulta.

El sistema tiene una finalidad educativa y de monitoreo. Sus mediciones no deben interpretarse como certificaciones profesionales de calidad del aire, niveles de ruido ni condiciones de seguridad.

## 🚀 3. Objetivos

### Objetivo general

Desarrollar un prototipo IoT capaz de monitorear variables ambientales de un espacio educativo mediante sensores conectados a un ESP32-C3, con posibilidad de visualizar y transmitir los datos obtenidos.

### Objetivos específicos

- Integrar diferentes sensores ambientales y de presencia.
- Programar el ESP32-C3 para adquirir y procesar las lecturas.
- Mostrar información mediante una pantalla LCD de 16 × 2.
- Establecer una conexión Wi-Fi para la comunicación del dispositivo.
- Implementar la publicación de datos mediante el protocolo MQTT.
- Desarrollar un panel web para visualizar la información recibida.
- Evaluar las lecturas obtenidas mediante pruebas individuales y de integración.
- Documentar las conexiones, los componentes, los resultados y las mejoras pendientes.
- Aplicar buenas prácticas de seguridad informática durante el desarrollo y la publicación del proyecto.

## 📌 4. Alcance del proyecto

### Funcionalidades previstas

- Lectura de temperatura y humedad.
- Medición de iluminación ambiental.
- Obtención de una lectura analógica relacionada con gases.
- Estimación del nivel de sonido a partir de muestras del micrófono.
- Detección de presencia mediante un sensor PIR.
- Visualización local mediante una pantalla LCD.
- Transmisión de variables a través de MQTT.
- Visualización de datos mediante un panel web.
- Clasificación orientativa de las condiciones de confort.

### Limitaciones

- El funcionamiento de cada sensor debe verificarse individualmente.
- Las lecturas dependen de la calibración, las condiciones ambientales y las características de los componentes.
- La lectura del MQ-135 no equivale directamente a una concentración exacta de contaminantes.
- El cálculo de sonido mediante muestras de audio no constituye una medición calibrada en decibelios.
- La clasificación de confort utiliza criterios que deben documentarse y validarse.
- La disponibilidad del panel web depende de que la comunicación y la recepción de datos estén correctamente implementadas.
- El prototipo no reemplaza instrumentos profesionales de medición ambiental.

---

## 🔧 5. Componentes del sistema

Los siguientes son los componentes identificados para el proyecto. La conexión física y el funcionamiento de cada uno deben confirmarse durante las pruebas.

| Componente | Función | Conexión prevista |
|---|---|---|
| ESP32-C3 Super Mini | Controlador principal y comunicación Wi-Fi | Unidad central |
| DHT22 | Medición de temperatura y humedad | GPIO 10 |
| BH1750 | Medición de iluminación ambiental | I²C: SDA GPIO 8, SCL GPIO 9 |
| MQ-135 | Lectura analógica relacionada con gases | AO: GPIO 0; DO: GPIO 7 |
| INMP441 | Captura de audio para estimar el nivel de sonido | I²S: SCK GPIO 4, WS GPIO 5, SD GPIO 6 |
| HC-SR501 | Detección de presencia mediante infrarrojos pasivos | OUT: GPIO 3 |
| LCD de 16 × 2 con interfaz I²C | Visualización local de información | I²C: SDA GPIO 8, SCL GPIO 9 |
| Batería | Alimentación del prototipo | Pendiente de documentar |
| Regulador reductor de tensión | Adaptación de la tensión de alimentación | Pendiente de documentar |

**Importante:** el BH1750 y la pantalla LCD comparten el bus I²C previsto. Ambos dispositivos deben tener direcciones compatibles y conexiones correctas para funcionar simultáneamente.

También se debe verificar que las tensiones de salida de los módulos sean compatibles con el ESP32-C3. Sus entradas GPIO no son tolerantes a 5 V. En particular, es necesario revisar las salidas del MQ-135, del PIR y las resistencias pull-up del bus I²C antes de realizar la conexión definitiva.

---

## 🏗️ 6. Arquitectura del sistema

La arquitectura prevista se organiza en cuatro etapas:

1. **Adquisición de datos:** los sensores obtienen información del entorno.
2. **Procesamiento:** el ESP32-C3 lee los sensores y prepara los valores.
3. **Comunicación:** el dispositivo utiliza Wi-Fi y MQTT para transmitir los datos.
4. **Visualización:** una pantalla LCD y un panel web permiten consultar la información, según las funcionalidades que se encuentren implementadas.

### Flujo general

```text
                 ENTORNO DEL AULA
                        |
                        v
             +----------------------+
             |   Sensores IoT       |
             |                      |
             | DHT22                |
             | BH1750               |
             | MQ-135               |
             | INMP441              |
             | HC-SR501             |
             +----------+-----------+
                        |
                        v
             +----------------------+
             |     ESP32-C3         |
             |                      |
             | Lectura de sensores  |
             | Procesamiento        |
             | Clasificación        |
             +-----+-----------+----+
                   |           |
                   v           v
             +-----------+  +----------------+
             | LCD 16x2  |  | Wi-Fi + MQTT   |
             | Local     |  | Comunicación   |
             +-----------+  +-------+--------+
                                     |
                                     v
                            +------------------+
                            | Broker MQTT      |
                            +--------+---------+
                                     |
                                     v
                            +------------------+
                            | Panel web        |
                            | Visualización    |
                            +------------------+
```

*El diagrama representa la arquitectura prevista, no una confirmación de que todas las conexiones y comunicaciones ya funcionan.*

---

## 📊 7. Variables monitoreadas

El sistema contempla las siguientes variables:

| Variable | Fuente | Interpretación |
|---|---|---|
| Temperatura | DHT22 | Temperatura ambiental, según la lectura del sensor |
| Humedad | DHT22 | Humedad relativa |
| Iluminación | BH1750 | Iluminancia ambiental, expresada habitualmente en lux |
| Gases | MQ-135 | Lectura analógica relacionada con la respuesta del sensor a determinados gases |
| Sonido | INMP441 | Estimación del nivel de señal de audio a partir de muestras digitales |
| Presencia | HC-SR501 | Estado de detección del sensor PIR |
| Confort | Procesamiento del sistema | Clasificación orientativa a partir de las variables disponibles |

### Estados previstos

Para la detección de presencia se contemplan los valores:

- `SI`: presencia detectada.
- `NO`: presencia no detectada.

Para la clasificación orientativa del confort se contemplan:

- `OK`
- `ACEPTABLE`
- `NO CONFORTABLE`
- `SIN DATOS`

Los umbrales utilizados para estas categorías deben documentarse y validarse. No deben presentarse como estándares científicos si no existe una fuente que los respalde.

---

## 📡 8. Comunicación MQTT

MQTT es un protocolo de mensajería utilizado para intercambiar información entre dispositivos y aplicaciones.

En este proyecto se prevé utilizarlo para publicar las variables obtenidas por el ESP32-C3 y permitir que otros clientes suscritos reciban los datos.

### Configuración conocida

| Parámetro | Valor |
|---|---|
| Broker | `192.168.101.94` |
| Puerto TCP | `1883` |
| Usuario configurado durante las pruebas | `alumno` |
| Grupo de temas | `6to_info/A/G4/` |

La dirección del broker corresponde a una red privada y puede dejar de ser accesible si cambia la red o la dirección IP del equipo que ejecuta el servicio.

**Seguridad:** no se deben publicar contraseñas ni credenciales reales en este repositorio. La configuración sensible debe mantenerse fuera del código público.

### Temas MQTT previstos

| Variable | Tema |
|---|---|
| Temperatura | `6to_info/A/G4/temperatura` |
| Humedad | `6to_info/A/G4/humedad` |
| Iluminación | `6to_info/A/G4/luz` |
| Sonido | `6to_info/A/G4/ruido` |
| Gases | `6to_info/A/G4/gases` |
| Presencia | `6to_info/A/G4/presencia` |
| Confort | `6to_info/A/G4/confort` |

Estos temas corresponden al esquema de publicación previsto y deben verificarse mediante pruebas de publicación y suscripción.

### MQTT en el panel web

Una página web que se conecte directamente al broker normalmente necesita un endpoint MQTT compatible con WebSocket, además de la configuración correspondiente del broker.

El puerto TCP `1883` no implica que la conexión WebSocket esté disponible. Antes de integrar el panel web, es necesario comprobar qué protocolo y puerto ofrece el broker.

---

## 🧪 9. Estado de desarrollo y pruebas

El proyecto se encuentra en etapa de desarrollo y verificación.

Durante las pruebas iniciales se observaron los siguientes resultados y pendientes:

| Elemento | Situación observada | Próximo paso |
|---|---|---|
| MQ-135 | Se observaron lecturas del ADC | Verificar estabilidad, alimentación y comportamiento ante distintas condiciones |
| INMP441 | Se realizaron pruebas de señal y cálculo aproximado RMS | Validar la captura I²S y documentar el método de estimación |
| HC-SR501 | Se observaron estados de detección | Comprobar sensibilidad, temporización y detección real |
| BH1750 | No se detectó correctamente en el bus I²C y se obtuvieron valores `NAN` | Revisar alimentación, cableado, dirección I²C y configuración del bus |
| LCD I²C | Encendió la retroiluminación, pero no mostró caracteres correctamente | Comprobar dirección I²C, contraste, cableado y biblioteca |
| DHT22 | Conexión prevista al GPIO 10 | Verificar lecturas válidas y estabilidad |
| Wi-Fi | Se presentaron dificultades de conexión | Revisar credenciales, señal y configuración de red |
| MQTT | No se confirmó la publicación completa de datos | Verificar conexión al broker y recepción de mensajes con un cliente suscriptor |
| Panel web | Integración pendiente de validación | Comprobar la recepción de datos y la conexión compatible con el broker |

Esta tabla documenta el estado conocido de las pruebas. No constituye una certificación de funcionamiento del sistema completo.

### Plan de validación

Se propone realizar las pruebas en este orden:

1. Verificar la alimentación y las conexiones eléctricas.
2. Probar cada sensor de manera independiente.
3. Comprobar la lectura de todos los sensores desde el ESP32-C3.
4. Resolver los problemas del bus I²C y validar la pantalla LCD.
5. Verificar la conexión Wi-Fi.
6. Probar la conexión y publicación MQTT.
7. Comprobar la recepción de mensajes mediante una suscripción.
8. Integrar el panel web y verificar su comunicación con el broker.
9. Realizar una prueba conjunta de funcionamiento.
10. Registrar resultados, errores, fotografías y cambios realizados.

Los resultados definitivos se incorporarán a la documentación cuando existan evidencias de las pruebas realizadas.

---

## 📁 10. Estructura del repositorio

La siguiente estructura es una propuesta inicial que puede adaptarse a los archivos reales del proyecto.

```text
smart-campus-iot/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── docs/
│   ├── 01-presentacion.md
│   ├── 02-problematica-y-objetivos.md
│   ├── 03-planificacion.md
│   ├── 04-arquitectura.md
│   ├── 05-diseno-hardware.md
│   ├── 06-diseno-aplicacion.md
│   ├── 07-presupuesto.md
│   ├── 08-pruebas.md
│   ├── 09-resultados-y-mejoras.md
│   └── 10-seguridad-informatica.md
│
├── firmware/
│   ├── README.md
│   └── src/
│       └── smart_campus.ino
│
├── dashboard/
│   ├── README.md
│   ├── index.html
│   ├── style.css
│   └── script.js
│
├── hardware/
│   ├── README.md
│   ├── lista-componentes.md
│   ├── diagrama-conexiones.png
│   └── fotos/
│
├── planificacion/
│   ├── carta-gantt.md
│   ├── tareas.md
│   └── entregables.md
│
└── evidencias/
    ├── pruebas/
    ├── montaje/
    └── capturas-dashboard/
```

**Nota:** esta estructura muestra la organización deseada. Los archivos deben crearse a medida que se desarrolla la documentación. Si el panel web todavía no está implementado, su carpeta debe considerarse pendiente.

---

## 💻 11. Instalación y puesta en marcha

Las instrucciones definitivas dependerán del código fuente, las bibliotecas utilizadas y la configuración real del broker.

### Requisitos previstos

- Un ESP32-C3 Super Mini.
- Los sensores y módulos indicados en la sección de componentes.
- Un entorno de desarrollo compatible con ESP32, como Arduino IDE.
- Las bibliotecas correspondientes a los sensores utilizados.
- Una red Wi-Fi accesible desde el dispositivo.
- Un broker MQTT accesible desde esa red.
- Un navegador web si se implementa el panel de visualización.

### Pasos generales

1. Clonar o descargar el repositorio.
2. Abrir el firmware en el entorno de desarrollo.
3. Instalar las bibliotecas necesarias.
4. Revisar las conexiones y los pines definidos en el código.
5. Configurar la red Wi-Fi y el broker sin incluir secretos en el repositorio.
6. Compilar el firmware y cargarlo en el ESP32-C3.
7. Abrir el monitor serie para comprobar las lecturas.
8. Verificar la conexión MQTT y los mensajes recibidos.
9. Configurar el panel web, si está implementado, y comprobar su conexión.

Estos pasos son orientativos. Para convertirlos en instrucciones reproducibles, se deben documentar las versiones, las bibliotecas y la configuración que se utilicen realmente.

---

## 🔐 12. Seguridad informática

La seguridad informática forma parte de los aspectos que deben considerarse durante el desarrollo del proyecto.

Se tendrán en cuenta las siguientes prácticas:

- No subir contraseñas de Wi-Fi al repositorio público.
- No publicar contraseñas del broker MQTT, tokens ni otros secretos.
- Utilizar archivos locales de configuración o variables de entorno cuando corresponda.
- Excluir archivos sensibles mediante `.gitignore`.
- Evitar exponer el broker MQTT directamente a Internet sin medidas de seguridad adecuadas.
- Limitar el acceso al broker y a sus temas según las posibilidades de configuración disponibles.
- Verificar las tensiones eléctricas antes de conectar los sensores al ESP32-C3.
- Documentar las limitaciones y los riesgos conocidos.
- Revisar los archivos antes de publicarlos en GitHub.

Un archivo `.gitignore` puede ayudar a evitar la publicación accidental de archivos locales, pero no reemplaza una configuración segura. Si una contraseña se publica por error, debe cambiarse: borrarla del último commit no garantiza que haya desaparecido del historial.

---

## 🛠️ 13. Mejoras futuras

Una vez verificado el funcionamiento básico, se podrán evaluar las siguientes mejoras:

- Corregir y estabilizar la lectura del BH1750.
- Conseguir una visualización correcta en la pantalla LCD.
- Mejorar el manejo de errores y la reconexión Wi-Fi.
- Validar la publicación y recepción de datos MQTT.
- Implementar un panel web con actualización de datos.
- Añadir indicadores visuales para las condiciones ambientales.
- Registrar mediciones para analizar su evolución.
- Documentar los criterios de clasificación de confort.
- Mejorar la calibración y la interpretación de las lecturas.
- Incorporar evidencias de pruebas y fotografías del montaje.
- Optimizar el consumo energético si se utiliza alimentación por batería.

Estas mejoras son propuestas y no funcionalidades confirmadas.

---

## 👥 14. Equipo de trabajo

**Institución educativa:** pendiente de completar.  
**Curso:** 6.º año.  
**Orientación:** Informática.  
**Docente responsable:** pendiente de completar.  
**Integrantes:** pendiente de completar.  
**Ciclo lectivo:** pendiente de completar.

Los datos institucionales y los nombres del equipo se agregarán cuando estén confirmados.

---

## 📚 15. Documentación y evidencias

En las carpetas correspondientes se incorporarán los materiales necesarios para comprender, reproducir y evaluar el proyecto:

- Diagramas de conexiones.
- Lista de componentes.
- Fotografías del montaje.
- Código fuente del firmware.
- Código del panel web, si corresponde.
- Planificación y carta Gantt.
- Registro de pruebas.
- Capturas de las lecturas y de los mensajes MQTT.
- Resultados obtenidos y mejoras propuestas.
- Documentación sobre seguridad informática.

Las evidencias deben corresponder a pruebas reales. Las imágenes, mediciones y capturas se agregarán a medida que estén disponibles.

---

## 📄 16. Licencia

La licencia del proyecto está pendiente de definición.

Antes de publicar el repositorio como un proyecto reutilizable, se deberá elegir una licencia apropiada y agregar el archivo `LICENSE` correspondiente.

---

**Smart Campus IoT — Proyecto escolar de monitoreo ambiental mediante tecnologías IoT.**
