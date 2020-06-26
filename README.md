## TUTORIAL PARA SIMULAR PROGRAMAS EN UN EQUIVALENTE DE ARDUINO UNO UTILIZANDO MULTISIM

<br>

**1. MARCO TEÓRICO**

<br>

**A.	ARDUINO UNO**

El Arduino UNO es una placa basada en un **MICROCONTROLADOR ATmega328**, cuya plataforma de creación electrónica es de código abierto, la cual está basada en hardware y software libre, flexible y fácil de utilizar para los creadores y desarrolladores. 
Los microcontroladores son circuitos integrados en los que se pueden grabar instrucciones, que se escriben con el lenguaje de programación que puedes utilizar en el entorno Arduino IDE. Estas instrucciones permiten crear programas que interactúan con los demás circuitos de la placa ya sea con software libre o en CÓDIGO ENSAMBLADOR.

Partes de una placa ARDUINO UNO

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a1.jpg)

**B.	MICROCONTROLADORES ATmega328 y  PIC16F84A.**

ATmega328 es un microcontrolador utilizado en el Arduino UNO, con una arquitectura RISC 8-bit que le permite ejecutar instrucciones en un solo ciclo de reloj, alcanzando una potencia de 1 MIPS. Los puertos soportan un máximo de 40 mA, a pesar que lo ideal es trabajar con 20 mA. 
 
 ![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a2.jpg)


El PIC16F84A es un microcontrolador gama media de 8 bits que físicamente consta de 18 pines, su memoria de programa es de tipo flash, lo que nos permitirá grabarlo hasta unas 10000 veces.
 Este tipo  micro controladores  son lo más parecido a un ARDUINO UNO, son capaces de desempeñar  las mismas funciones y a ambos se los puede trabajar en LENGUAJE ENSAMBLADOR.

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a3.jpg)


**C.	NI MULTISIM 14.0**

Es un programa que ha sido diseñado específicamente para profesores, estudiantes y profesionales del diseño de circuitos, hace que la creación de cualquier circuito eléctrico se convierta en un proceso sencillo, con la posibilidad de añadir cualquier elemento a los circuitos. Por tanto, si eres un estudiante y quieres tener acceso a uno de los mejores programas del sector para la creación de circuitos eléctricos, descarga e instala NI Multisim Student Edition en tu ordenador.


![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a7.jpg)


**¿Dónde puedo instalar NI MULTISIM 14.0?**


NI MULTISIM es compatible con las siguientes plataformas:

- Sistema Operativo Windows® 10 Windows® 8 / 8.1 Windows® 7, XP

- 128 MB MEMORIA RAM

- Tarjeta de Video Integral

- Tarjeta de Sonido 5.1

- 2000 Megas Espacio Disco Duro

- 	Procesador 2.3Ghz dual core

- Monitor VGA

- Conexión a Internet


**D.	MÓDULO ENSAMBLADOR EN MULTISIM**

El único lenguaje que entienden los micro controladores es el código de máquina formado por ceros y unos del sistema binario.

El lenguaje ensamblador expresa las instrucciones de una forma más natural al hombre a la vez que muy cercana al micro controlador, para simular el comportamiento de un micro controlador al ejecutar un programa sencillo las instrucciones del mismo lo debemos hacer en ensamblador. 

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a4.jpg)


**2.	DIAGRAMA ELÉCTRICO**

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a5.jpg)


**3.	LISTA DE COMPONENTES**

•	Computador con  Sistema Operativo Windows 8 ó 10

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a6.jpg)

•	Software de simulación NI Multisim 14.0			

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a7.jpg)

•	Módulo Ensamblador Multisim 14.0

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a8.jpg)

 
**4.	EXPLICACIÓN DEL CÓDIGO FUENTE**

<br>

**A.	CÓDIGO FUENTE**

<br>

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a9.jpg)


**- BLOQUE DE CONFIGURACIÓN DEL MICROCONTROLADOR**

En esta primera parte del código configuramos al microcontrolador asignado los pines de registro y los de ejecución.

<br>

**#include "p16f84a.inc"**

Es una librería que incluye las definiciones PIC16F84A para el que el módulo ensamblador MPASM reconozca los puertos del micro controlador.

**LIST P=16F04A**	

Incluye todas las rutinas para poder trabajar con el microcontrolador  	

**RADIX HEX**		

Convierte todas las instrucciones numéricas en hexadecimales

<br>
 
**- BLOQUE AUXILIAR**

<br>

En esta parte del código se definen las variables auxiliares que cumplen la función de realizar la validación de cada puerto del microcontrolador y de esta forma saber que puerto esta activo y cual no.

**AUXILIAR EQU 0X0C**  

Lbreria para controlar los pines del microcontrolador

***ORG 0**          

Es un vector cero o vector reset cada vez que se ejecuta el programa el contador se ubica aqui

**GOTO INICIO**	   

Vaya a una etiqueta inicio, o a la primeria ubicación del microcontrolar

**ORG 5**        

Es la posición de arranque del microcontrolador

<br>
 
**- BLOQUE DE INICIO**

En esta parte se especifica los pines de salida y los pines de entrada una vez definidos estos parámetros se direcciona nuevamente al banco de trababjo 

**INICIO  BSF STATUS, RP0**   

Registro estado del microcontrolador, es una instrucción en ensamblador que pone un 1 en el registro específico o registro de arranque, el microcontrolador cuenta con 8 bits de registro  

**MOVLW B'00001111'** 

Es un registro de trabajo para ejecutar todo el repertorio de instrucciones del microcontrolador

**MOVWF TRISB** 

Se mueve todas las instrucciones a la memoria aleatoria del microcontrolador para ser configurada y después ejecutada en el banco 0

**BCF STATUS, RP0** 

Con esta instrucción se trabaja en el banco 1 de la memoria de datos

<br>

**- BLOQUE LEER PUERTO**

Una vez ejecutadas todas las instrucciones asignadas a las variables auxiliares se vuelve a direccionar todo el proceso al banco 0 o banco de trabajo

<br>

**LEERPUERTO	MOVF PORTB,W** 

Con esta instrucción se leen todas las entradas

**ANDLW 0X0F** 

Con esta linea de ejecución le indicamos al microcontrolador que para que se prenda el led tiene que existir un voltaje y estar el interruptor activado

**MOVWF AUXILIAR** 

Variable auxiliar funciona como una conexion entre los bancos de trabajo

**COMF AUXILIAR,W** 

Esta variable trabaja de forma que donde el auxiliar tenga un 1 cambia a 0 , con esta intrucion realizamos el escaneo de los pines para saber cual esta activo y cual apagado

**ANDLW 0X0F** 

Con esta linea de ejecución le indicamos al microcontrolador que para que se prenda el led tiene que existir un voltaje y estar el interruptor activado

**MOVWF AUXILIAR** 

Se direcciona la variable auxiliar al banco de trabajo para su ejecución

**SWAPF AUXILIAR,W** 

Se direcciona la variable auxiliar al banco de trabajo para su ejecución

**MOVWF PORTB** 

Se direcciona la variable auxiliar al banco de trabajo para su ejecución

**GOTO LEERPUERTO**

Despues de hacer todas las validaciones con esta instruccion se prende el led si ingresa un voltaje al puerto Y el interruptor está encendido.
 
**END** 

Finaliza el proceso

<br>

**B.	EJECUCIÓN DEL PROYECTO** 

1.	Primero abrimos el software de simulación NI Multisim 14.0, de la siguiente manera, damos clic derecho sobre el icono del programa y elegimos la opción:

Propiedades/compatibilidad/Nivel de privilegio/ejecutar como administrador/aplicar y aceptar

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a10.jpg)

2.	Una vez ingresamos a nuestro espacio de trabajo podemos utilizar el scroll del mouse para desplazarnos con mayor facilidad y regular el zoom de la pantalla.

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a11.jpg)


3.	Para colocar un micro controlador PIC, nos ubicamos en la barra de herramientas en la parte superior y le damos clic en el botón MCU.

Aparece una nueva ventana, seleccionamos la opción PIC16F84A le damos clic en aceptar después clic en el lugar de la pantalla donde queremos que aparezca el elemento.

 ![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a12.jpg)

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a13.jpg)

4.	En la nueva ventana que aparece colocamos el nombre de nuestro proyecto, y le damos clic en siguiente.
 
![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a14.jpg)


5.	En la ventana que aparece nos ubicamos en la pestaña Lenguaje de programación, elegimos Ensamblador y en nombre del proyecto escribimos nuevamente el nombre de nuestro trabajo y le damos clic en siguiente.
 
![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a15.jpg)


6.	Sin modificar ningún otro parámetro le damos clic en Terminar, observamos que el elemento aparece en la pantalla de simulación y  se genera una pestaña con el “nombre main.asm”.

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a16.jpg)


7.	En la ventana que aparece se debe pegar o escribir el código de ensamblador realizado en el inciso “4. A” de este documento, una vez ingresado el código volvemos a la pestaña anterior.
 
![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a17.jpg)


8.	Para agregar los diferentes componentes de nuestro circuito presionamos las teclas:
Ctrl + W

Una vez en la ventana de componentes nos desplazamos hacia la parte izquierda en la pestaña de “Grupo:” seleccionamos “Basic”. 

 ![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a18.jpg)

  
9.	Una vez en la ventana “Basic” seleccionamos los elementos necesarios según el diagrama eléctrico, le damos clic en aceptar y clic en la pantalla donde queremos que aparezca el componente.
 
![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a19.jpg)
 

10.	Si necesitamos cambiar el valor ya sea de una resistencia o de una fuente de tensión, damos doble clic sobre el elemento, escribimos el valor y clic en aceptar. Por ejemplo:
100 ohmios = “100”
1000 ohmios= “1000” ó “1k”
 
![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a20.jpg)


11.	Una vez que seleccionamos todos los elementos necesarios para el circuito realizamos las conexiones respectivas dando clic en el punto en el terminal de un elemento y llevando el puntero al terminal del otro elemento. 

Para las conexiones utilizamos el Diagrama Eléctrico del inciso 2.

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a21.jpg)


12.	Como paso final le damos clic en el botón Iniciar Simulación, podemos observar que si encendemos un interruptor se va a encender el led respectivo.

![](https://github.com/bvalvarado/TRABAJO-EXTRA-1/blob/master/Img/a22.jpg)

 
**5.	BIBLIOGRAFÍA**

•	https://www.xataka.com/basics/que-arduino-como-funciona-que-puedes-hacer-uno

•	http://www.iescamp.es/miarduino/2016/01/21/placa-arduino-uno/

•	https://naylampmechatronics.com/microcontroladores/111-atmega328.html

•	https://arduinobot.pbworks.com/f/Manual+Programacion+Arduino.pdf

•	http://sherlin.xbot.es/microcontroladores/microcontroladores-de-gama-media/4-microcontrolador-pic-16f84

•	https://www.ni.com/es-cr/shop/electronic-test-instrumentation/application-software-for-electronic-testand-instrumentation-category/what-is-multisim.html

