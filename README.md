# Laboratorio-1
// Autores: Miguel Caro - Samuel Parra
## Primer Punto:  Usar Rufus y Ventoy en memorias separadas y en un readme describir:
1. Explicar el proceso de Booteo de la memoria usada en Rufus y la memoria usada en Ventoy.

Cuando usamos Rufus para crear una memoria booteable, lo que se hizo fue formatear la USB y grabar directamente la imagen ISO con un sistema de archivos como FAT32 o NTFS. Después, cuando encendimos el computador y seleccionamos arrancar desde la memoria, el BIOS leyó el bootloader que Rufus había grabado en el sector de arranque, y ese bootloader inició de inmediato la instalación del sistema operativo. La desventaja fue que solo pudimos tener una ISO en la memoria, así que si quisimos otra tuvimos que formatearla y volver a crearla. En cambio, cuando utilizamos Ventoy, este instaló su propio bootloader basado en GRUB y dividió la memoria en dos partes: una pequeña con Ventoy y otra grande donde copiamos libremente las ISOs. Así, al arrancar desde la USB, nos apareció un menú con todas las imágenes que habíamos copiado y simplemente elegimos cuál queríamos iniciar, sin necesidad de volver a formatear.

2. Revisar para qué sirve un bootloader en la memoria Booteable y qué es el GRUB.

Nosotros entendimos el bootloader como un programa muy pequeño que estaba en el sector de arranque de la memoria y que sirvió para iniciar el sistema operativo. Cuando prendimos el computador, el BIOS le entregaron el control al bootloader, y a partir de ahí este decidió cómo arrancar el sistema. En ese sentido, uno de los bootloaders más conocidos fue GRUB, que significaba GRand Unified Bootloader. Lo interesante de GRUB fue que nos permitió elegir entre varios sistemas operativos o varias imágenes al iniciar, además de ser compatible con distintos sistemas de archivos y darnos opciones de configuración más avanzadas.

3. Explorar qué son los sistemas de archivos compatibles y cuáles son, hacer una breve descripción.

Los sistemas de archivos son estructuras lógicas que permiten organizar, almacenar y gestionar la información en dispositivos de almacenamiento como discos duros, memorias USB o tarjetas SD. Cada sistema de archivos tiene sus propias reglas para manejar directorios, archivos, permisos y tamaños máximos, lo cual influye directamente en su compatibilidad con distintos sistemas operativos y en la forma en que se utilizan las memorias booteables.

En el contexto de la creación de memorias booteables, es fundamental elegir el sistema de archivos adecuado, ya que no todos son reconocidos por el BIOS, el UEFI o el sistema operativo que se desea instalar. A continuación, se describen los más importantes:

FAT32 (File Allocation Table 32): Es uno de los sistemas de archivos más antiguos y más usados debido a su gran compatibilidad. Puede ser leído y escrito por prácticamente todos los sistemas operativos (Windows, Linux, macOS, BIOS y UEFI). Sin embargo, tiene una limitación importante: no permite almacenar archivos de más de 4 GB ni particiones superiores a 2 TB.

NTFS (New Technology File System): Es el sistema de archivos por defecto en Windows. Soporta archivos grandes y ofrece características avanzadas como permisos, compresión y journaling (registro de cambios). Aunque es reconocido por BIOS y muchos sistemas Linux (con drivers), su compatibilidad con UEFI puede ser limitada.

exFAT (Extended File Allocation Table): Fue diseñado como una evolución de FAT32. Elimina la restricción del tamaño de archivo, permitiendo manejar archivos mayores a 4 GB. Es compatible con Windows, macOS y Linux (con soporte adicional), por lo que se utiliza ampliamente en memorias USB y tarjetas SD de gran capacidad.

ext4 (Fourth Extended Filesystem): Es el sistema de archivos estándar de la mayoría de las distribuciones de Linux. Permite manejar archivos muy grandes, es robusto y rápido. No obstante, Windows no lo reconoce de manera nativa, lo que limita su uso en memorias booteables destinadas a sistemas de Microsoft.

ISO9660/UDF (Universal Disk Format): Estos sistemas se usan principalmente en discos ópticos (CD, DVD y Blu-ray). Muchas imágenes ISO están basadas en ISO9660 o UDF, por lo que algunos bootloaders los soportan para simular el arranque como si proviniera de un disco físico.

4. Investigar sobre la estructura de particiones, qué es, los tipos y describirlos.
   
La estructura de particiones hace referencia a la forma en que se divide un disco duro, una memoria USB o cualquier dispositivo de almacenamiento en secciones llamadas particiones. Cada partición funciona como una unidad independiente que puede tener su propio sistema de archivos, lo que permite instalar sistemas operativos diferentes, organizar mejor los datos o reservar espacio para funciones específicas.

El proceso de particionado es esencial porque es el que permite al sistema operativo reconocer, administrar y utilizar de manera eficiente el dispositivo de almacenamiento. Además, las particiones determinan cómo se accede al espacio del disco y qué tan flexible será en el futuro para añadir o modificar información.

### Tipos de estructuras de particiones

A lo largo de la historia de la informática se han utilizado diferentes esquemas de particionado. Los más importantes son:

 **MBR (Master Boot Record)**
- Es el esquema de particiones más antiguo, introducido en 1983.
- Utiliza los primeros 512 bytes del disco para almacenar el cargador de arranque y la tabla de particiones.
- Solo permite un máximo de 4 particiones primarias, o 3 primarias y una extendida (que a su vez puede contener particiones lógicas).
- Tiene la limitación de no poder administrar discos de más de 2 TB.
- Es ampliamente compatible con sistemas BIOS tradicionales.

 **GPT (GUID Partition Table)**
- Es el esquema más moderno, definido como parte de la especificación UEFI.
- Usa identificadores únicos globales (GUID) para cada partición.
- Permite un número prácticamente ilimitado de particiones (aunque los sistemas operativos suelen limitarlo a 128).
- Puede manejar discos mucho más grandes, incluso superiores a 9 ZB (zettabytes).
- Incluye redundancia en la información de particiones, almacenando una copia de la tabla al inicio y otra al final del disco, lo que ofrece mayor seguridad ante errores.
- Es el estándar actual en sistemas operativos modernos como Windows 10/11 y distribuciones de Linux con soporte UEFI.

#### Tipos de particiones dentro de MBR
- Partición primaria: es la partición básica desde la cual puede arrancar un sistema operativo. Se pueden tener hasta cuatro.
- Partición extendida: es una partición especial que no almacena datos directamente, sino que sirve como “contenedor” de otras particiones llamadas lógicas.
- Particiones lógicas: se crean dentro de la extendida y permiten superar la limitación de solo cuatro particiones.

En GPT, por su diseño avanzado, no es necesario usar extendidas ni lógicas: todas las particiones tienen el mismo nivel jerárquico.
   
## Segundo Punto: Descargar la imagen de Ubuntu y la imagen de Windows.
1. Anexar la imagen de Ubuntu en la memoria con Rufus, describir en el readme el proceso.
   ![Imagen de WhatsApp 2025-08-27 a las 18 59 36_82e3179b](https://github.com/user-attachments/assets/292d19a7-2b3d-42b1-9012-65928dcfc9e6)








3. Anexar la imagen de Ubuntu y Windows en la memoria con Ventoy, describir en el readme el proceso.
## Tercer Punto: Usar la memoria booteable con Rufus o Ventoy y generar la partición en el pc para instalar Ubuntu.
1. Describir y mostrar pantallazos de la instalación paso a paso de ubuntu con el proceso de participación del pc.
   ![Imagen de WhatsApp 2025-08-27 a las 19 02 21_e9ac981d](https://github.com/user-attachments/assets/7439412b-05ee-4bb4-8c26-5d8770065e4e)
![Imagen de WhatsApp 2025-08-27 a las 19 00 50_4e23d7f8](https://github.com/user-attachments/assets/fea2c478-1c4e-4657-92bf-fef1a8c479ce)
![Imagen de WhatsApp 2025-08-27 a las 19 00 57_553b0471](https://github.com/user-attachments/assets/b29ed10f-f65b-40d2-8ec9-4453762e0633)
![Imagen de WhatsApp 2025-08-27 a las 19 04 19_f7322321](https://github.com/user-attachments/assets/a1379b63-0b32-43bf-8e17-d34717a6e214)
