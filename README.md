# 1º Parcial-SPD "Montacargas Hospital"


Matias Skenen

![image](![image](https://github.com/matiastaoskn/PARCIAL-SPD1/assets/93952537/595affb1-f87a-4114-bf52-f3020b48a78f))

## Componentes utilizados

- Arduino Uno
- Display de 7 segmentos
- Resistencias
- Botones
- LED verde y LED rojo

## Configuración de pines

El código utiliza los siguientes pines para conectar los componentes:

```
#define LED_ROJO 13
#define LED_VERDE 12

#define LED_A 7
#define LED_B 6
#define LED_C 5
#define LED_D 4
#define LED_E 3
#define LED_F 2
#define LED_G A4

#define botonSubir 11
#define botonBajar 10
#define botonDetener 9

int nivel = 0;
int piso;
int botonSubida;
int botonBajada;
int botonDetenido;

int montaCargaSUBIENDO = false;
int montaCargaBAJANDO = false;

int botonEmergencia = false;
int acumuladorEmergencia = 0;
```


## Bucle principal

En el bucle principal `loop`, se llama a la función `controladorMontacargas()` 


El programa contiene las siguientes funciones principales:

- `encenderNumero`: Esta función enciende los segmentos correspondientes para mostrar un número en el display.
- `manejadorDisplay`: Esta función selecciona qué número se debe mostrar en el display según el valor del contador.
- `manejadorMontaCargas`: Esta función es el bucle principal del programa. Controla la lógica de incrementar o decrementar el contador según los botones presionados, así como también la lógica de pausar el servicio.
- `incrementarContador`: Esta función incrementa el valor del contador y muestra el nuevo valor en el display.
- `decrementarContador`: Esta función decrementa el valor del contador y muestra el nuevo valor en el display.
- `movimiento`: Esta función activa un LED verde para indicar movimiento durante un periodo de tiempo.
- `servicioEnPausa`: Esta función muestra en el display el estado de pausa del servicio y enciende o apaga un LED rojo según sea necesario.


## Función `manejadorMontaCargas()`
```cpp
if(nivel == 0)
  {
    montacarga();
  }
  
  //Boton de emergencia, deterner.
  if(botonDetenido == 0)
  {
    acumuladorEmergencia += 1;
    delay(1000);
    Serial.println("Emergencia Activado");
  }
  
	// Comienzo de programa
  if(acumuladorEmergencia % 2 == 0)
  {
    if(botonSubida == 0 || botonBajada == 0)
    {
      if(botonBajada == 0)
      {
        nivel -= 1;
        prenderLeds(0, 0, 0, 0, 0, 0, 0, 3000);
        montacarga();
        mostrarPiso();
      }
      else
      {
        if(nivel >= 9)
        {
          piso = 9;
          prenderLeds(1, 1, 1, 1, 0, 1, 1, 3000);
          mostrarPiso();
        }
        else
        {
          prenderLuces(LED_VERDE);
          apagarLuces(LED_ROJO);
          nivel += 1;
          prenderLeds(0, 0, 0, 0, 0, 0, 0, 3000);
          montacarga();
          mostrarPiso();
        }

      }
    }
  }
```



