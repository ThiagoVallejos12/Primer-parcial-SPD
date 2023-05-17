# _Primer parcial SPD_

Nombre y apellido: Thiago Vallejos

Division: J

# Ascensor

![Captura de pantalla (96)](https://github.com/ThiagoVallejos12/Primer-parcial-SPD/assets/108820694/581d557b-d473-42b2-9640-2e14e2c02d8e)

## Descripción del proyecto

Este proyecto es un sistema que simula un ascensor.

En el proyecto se utiliza:

-1 Placa arduino.

-1 Breadboard.

-1 Display 7 segmentos.

-3 Botones.

-2 Leds.

-10 Resistencias.

## Como funciona

Se informa constantemente mediante el display 7 segmentos, en que piso se encuentra el ascensor(Piso mas bajo: 0. Piso mas alto: 9).

Hay 3 botones: Uno para subir, otro para bajar y otro para frenar el ascensor.

Al pulsar el boton de subir, subira un piso. Lo mismo con el de bajar.

Al pulsar el boton de frenar, el ascensor hara una parada de emergencia, sin importar si esta en movimiento o no.

En caso de que el ascensor este en movimiento, se encendera el led verde.

En caso de que el ascensor este frenado, se encendera el led rojo.

## Defines, declaración de funciones y declaración de variables.
```c++
#define	A 2
#define B 3
#define C 4
#define D 5
#define E 6
#define F 7
#define G 8
#define PUNT 9
#define ledRojo 10
#define ledVerde 11
#define botonSubir A0
#define botonFrenar A1
#define botonBajar A2
void encenderDisplay7(int dA, int dB, int dC, int dD, int dE, int dF, int dG, int numero);
void detectarbotonfrenar(int botonfrenado, int led1, int led2, int punto);
int contarpulsacionboton(int botonup,int botondown, int botonstop, int contador, int punt);
int estadoboton;
int contadorboton = 0;
```

## Setup
```c++
for(int i = 2; i<12; i++)
  {
  	pinMode(i, OUTPUT);
  }
Serial.begin(9600);
pinMode(botonSubir, INPUT_PULLUP);
pinMode(botonBajar, INPUT_PULLUP);
pinMode(botonFrenar, INPUT_PULLUP);
```

## Código principal
Se iguala la variable "contadorboton" a la función "contarpulsacionboton", que recibe como parámetro: botonSubir, botonBajar, botonFrenar, contadorboton, ledRojo, ledVerde.

Esta funcion retorna un dato de tipo entero, el cual representa el piso en el que se encuentra el ascensor.

Luego se ejecuta la función "encenderDisplay7". La cual recibe por parametro los valores de los 7 segmentos, y la variable "contadorboton"
```c++
contadorboton = contarpulsacionboton(botonSubir, botonBajar, botonFrenar, contadorboton, ledRojo, ledVerde, PUNT);
encenderDisplay7(A,B,C,D,E,F,G,contadorboton);
```

## Codigo de funciones.
### *"encenderDisplay7"*

Esta funcián recibe por parámetros los datos de los 7 segmentos del display, y un numero que va a ser el que el segmento tiene que representar.

Dependiendo del numero que se reciba, va a ser el que se va a mostrar en el display.

No retorna nada.

```c++
void encenderDisplay7(int dA, int dB, int dC, int dD, int dE, int dF, int dG, int numero)
{
  switch (numero)
  {
    case -1:
    	digitalWrite(dA, 0);
    	digitalWrite(dB, 0);
    	digitalWrite(dC, 0);
    	digitalWrite(dD, 0);
    	digitalWrite(dE, 0);
    	digitalWrite(dF, 0);
    	digitalWrite(dG, 1);
    break;
    case 0:
    	digitalWrite(dA, 1);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 1);
    	digitalWrite(dE, 1);
    	digitalWrite(dF, 1);
    	digitalWrite(dG, 0);
    break;
    case 1:
    	digitalWrite(dA, 0);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 0);
    	digitalWrite(dE, 0);
    	digitalWrite(dF, 0);
    	digitalWrite(dG, 0);
    break;
    case 2:
      digitalWrite(dA, 1);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 0);
    	digitalWrite(dD, 1);
    	digitalWrite(dE, 1);
    	digitalWrite(dF, 0);
    	digitalWrite(dG, 1);
    break;
    case 3:
      digitalWrite(dA, 1);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 1);
    	digitalWrite(dE, 0);
    	digitalWrite(dF, 0);
    	digitalWrite(dG, 1);
    break;
    case 4:
      digitalWrite(dA, 0);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 0);
    	digitalWrite(dE, 0);
    	digitalWrite(dF, 1);
    	digitalWrite(dG, 1);
    break;
    case 5:
    	digitalWrite(dA, 1);
    	digitalWrite(dB, 0);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 1);
    	digitalWrite(dE, 0);
    	digitalWrite(dF, 1);
    	digitalWrite(dG, 1);
    break;
    case 6:
    	digitalWrite(dA, 0);
    	digitalWrite(dB, 0);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 1);
    	digitalWrite(dE, 1);
    	digitalWrite(dF, 1);
    	digitalWrite(dG, 1);
    break;
    case 7:
    	digitalWrite(dA, 1);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 0);
    	digitalWrite(dE, 0);
    	digitalWrite(dF, 0);
    	digitalWrite(dG, 0);
    break;
    case 8:
    	digitalWrite(dA, 1);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 1);
    	digitalWrite(dE, 1);
    	digitalWrite(dF, 1);
    	digitalWrite(dG, 1);
    break;
    case 9:
    	digitalWrite(dA, 1);
    	digitalWrite(dB, 1);
    	digitalWrite(dC, 1);
    	digitalWrite(dD, 0);
    	digitalWrite(dE, 0);
    	digitalWrite(dF, 1);
    	digitalWrite(dG, 1);
    break;
  }
}
```

### *"detectarbotonfrenar"*
Esta función recibe por parámetros: botonfrenado, leduno, leddos, punto.

Lo que hace es verificar si el boton de frenado se pulsa. En caso de ser pulsado, se ejecuta un while. De esta manera se logra que el ascensor frene.

Dentro del while, se informa una vez por consola que el ascensor esta detenido. Se apaga el led que indica que el ascensor esta en movimiento, y se enciende el que indica

que el ascensor esta detenido. Tambien, en el display se enciende el punto.

Este while va a dejar de ejecutarse unicamente cuando el boton vuelva a ser pulsado.

```c++
void detectarbotonfrenar(int botonfrenado, int leduno, int leddos, int punto)
{
  int flagMensaje = 1;
  int ultimoestadobotonstop;
  int estadobotonstop;
  int flagbotonstop;
  estadobotonstop = digitalRead(botonfrenado);
  if (estadobotonstop != ultimoestadobotonstop)
  {
    while (estadobotonstop == LOW)
    {
      if (flagMensaje == 1)
      {
        Serial.println("MONTACARGAS DETENIDO");
        flagMensaje = 0;
      }
      digitalWrite(leduno, 0);
      digitalWrite(punto, 1);
      digitalWrite(leddos, 1);
      delay(100);
      flagbotonstop = digitalRead(botonfrenado);
      if (flagbotonstop == LOW)
      {
        break;
      }
    }
    digitalWrite(leddos, 0);
  }
  ultimoestadobotonstop = estadobotonstop;
}
```

### *"contarpulsacionboton"*
Como mencioné anteriormente, esta función recibe por parámetros: botonSubir, botonBajar, botonFrenar, contadorboton, ledRojo, ledVerde. y retorna un dato de tipo entero,

que va a representar al piso en el que se encuentra el ascensor.

Esta función evalúa en todo momento si, el boton de subir o el de bajar es pulsado.

En caso de que se pulse el boton de subir o bajar, se ejecuta un for, el cual, cada 100ms, reutilizara la funcion creada anteriormente *"detectarbotonfrenar"* 

con el fin de detectar si el boton de frenar es presionado mientras el ascensor sube o baja de nivel. El for va a ejecutarse mientras que el contador i, 

el cual inicia en 0, y suma 100 por cada 100ms que hay de delay, se mantenga por debajo de los 3000(3 segundos).

Luego de esto, dependiendo si se pulso el boton de subir, o de bajar, a la variable *contador* se le va a sumar 1 o restar 1.

Finalmente, la funcion retorna el valor de la variable *contador*.
```c++
int contarpulsacionboton(int botonup,int botondown,int botonstop, int contador, int led1, int led2, int punt)
{
  int ultimoestadobotonup;
  int ultimoestadobotondown;
  int estadobotonup;
  int estadobotondown;
  Serial.println(contador);
  estadobotonup = digitalRead(botonup);
  estadobotondown = digitalRead(botondown);
  detectarbotonfrenar(botonstop, led1, led2, punt);
  if (estadobotonup != ultimoestadobotonup || estadobotondown != ultimoestadobotondown)
  {
    if (estadobotonup == LOW && contador < 9)
    {
      for (int i = 0; i <= 2900; i += 100)
      {
        digitalWrite(led1, 1);
        detectarbotonfrenar(botonstop, led1, led2, punt);
        delay(100);
      }
      contador++;
      digitalWrite(led1, 0);
    }
    if (estadobotondown == LOW && contador > 0)
    {   
      for (int i = 0; i <= 2900; i += 100)
      {
        digitalWrite(led1, 1);
        detectarbotonfrenar(botonstop, led1, led2, punt);
        delay(100);
      }
      contador--;
      digitalWrite(led1, 0);
    }
    delay(100);
  }
  ultimoestadobotonup = estadobotonup;
  ultimoestadobotondown = estadobotondown;
  return contador;
}
```

## :eight_pointed_black_star: Proyecto en tinkercad
[Primer parcial](https://www.tinkercad.com/things/4P5avjdLAza)
