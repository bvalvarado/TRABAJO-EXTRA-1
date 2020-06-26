**TUTORIAL PARA SIMULAR PROGRAMAS EN UN EQUIVALENTE DE ARDUINO UNO UTILIZANDO MULTISIM**


**A.	ARDUINO UNO**

El Arduino UNO es una placa basada en un **MICROCONTROLADOR ATmega328**, cuya plataforma de creación electrónica es de código abierto, la cual está basada en hardware y software libre, flexible y fácil de utilizar para los creadores y desarrolladores. 
Los microcontroladores son circuitos integrados en los que se pueden grabar instrucciones, que se escriben con el lenguaje de programación que puedes utilizar en el entorno Arduino IDE. Estas instrucciones permiten crear programas que interactúan con los demás circuitos de la placa ya sea con software libre o en CÓDIGO ENSAMBLADOR.

Partes de una placa ARDUINO UNO




**B.	MICROCONTROLADORES ATmega328 y  PIC16F84A.**

ATmega328 es un microcontrolador utilizado en el Arduino UNO, con una arquitectura RISC 8-bit que le permite ejecutar instrucciones en un solo ciclo de reloj, alcanzando una potencia de 1 MIPS. Los puertos soportan un máximo de 40 mA, a pesar que lo ideal es trabajar con 20 mA. 
 

El PIC16F84A es un microcontrolador gama media de 8 bits que físicamente consta de 18 pines, su memoria de programa es de tipo flash, lo que nos permitirá grabarlo hasta unas 10000 veces.
 Este tipo  micro controladores  son lo más parecido a un ARDUINO UNO, son capaces de desempeñar  las mismas funciones y a ambos se los puede trabajar en LENGUAJE ENSAMBLADOR.







**C.	NI MULTISIM 14.0**

Es un programa que ha sido diseñado específicamente para profesores, estudiantes y profesionales del diseño de circuitos, hace que la creación de cualquier circuito eléctrico se convierta en un proceso sencillo, con la posibilidad de añadir cualquier elemento a los circuitos. Por tanto, si eres un estudiante y quieres tener acceso a uno de los mejores programas del sector para la creación de circuitos eléctricos, descarga e instala NI Multisim Student Edition en tu ordenador.


**¿Dónde puedo instalar NI MULTISIM 14.0?**



NI MULTISIM es compatible con las siguientes plataformas:
o	Sistema Operativo Windows® 10 Windows® 8 / 8.1 Windows® 7, XP
o	128 MB MEMORIA RAM
o	Tarjeta de Video Integral
o	Tarjeta de Sonido 5.1
o	2000 Megas Espacio Disco Duro
o	Procesador 2.3Ghz dual core
o	Monitor VGA
o	Conexión a Internet


**D.	MÓDULO ENSAMBLADOR EN MULTISIM**

El único lenguaje que entienden los micro controladores es el código de máquina formado por ceros y unos del sistema binario.

El lenguaje ensamblador expresa las instrucciones de una forma más natural al hombre a la vez que muy cercana al micro controlador, para simular el comportamiento de un micro controlador al ejecutar un programa sencillo las instrucciones del mismo lo debemos hacer en ensamblador. 
















**2.	DIAGRAMA ELÉCTRICO***












**3.	LISTA DE COMPONENTES **

•	Computador con  Sistema Operativo Windows 8 ó 10







•	Software de simulación NI Multisim 14.0			






•	Módulo Ensamblador Multisim 14.0

 


**4.	EXPLICACIÓN DEL CÓDIGO FUENTE**

**A.	CÓDIGO FUENTE**

 

**#include "p16f84a.inc"**	Es una librería que incluye las definiciones PIC16F84A para el que el módulo ensamblador MPASM reconozca los puertos del micro controlador.

LIST P=16F04A
 	RADIX HEX

AUXILIAR EQU 0X0C
		ORG 0
		GOTO INICIO
		ORG 5

INICIO  BSF STATUS, RP0
		MOVLW B'00001111'
		MOVWF TRISB
		BCF STATUS, RP0

LEERPUERTO	MOVF PORTB,W
		ANDLW 0X0F
		MOVWF AUXILIAR
		COMF AUXILIAR,W
		ANDLW 0X0F
		MOVWF AUXILIAR
		SWAPF AUXILIAR,W
		MOVWF PORTB
		GOTO LEERPUERTO

	END
		LIST P=16F04A
		RADIX HEX

AUXILIAR EQU 0X0C

		ORG 0
		GOTO INICIO
		ORG 5

INICIO  BSF STATUS, RP0
		MOVLW B'00001111'
		MOVWF TRISB
		BCF STATUS, RP0

LEERPUERTO	MOVF PORTB,W
		ANDLW 0X0F
		MOVWF AUXILIAR
		COMF AUXILIAR,W
		ANDLW 0X0F
		MOVWF AUXILIAR
		SWAPF AUXILIAR,W
		MOVWF PORTB
		GOTO LEERPUERTO

	END

B.	EJECUCIÓN DEL PROYECTO 

1.	Primero abrimos el software de simulación NI Multisim 14.0, de la siguiente manera, damos clic derecho sobre el icono del programa y elegimos la opción:

Propiedades/compatibilidad/Nivel de privilegio/ejecutar como administrador/aplicar y aceptar



2.	Una vez ingresamos a nuestro espacio de trabajo podemos utilizar el scroll del mouse para desplazarnos con mayor facilidad y regular el zoom de la pantalla.
