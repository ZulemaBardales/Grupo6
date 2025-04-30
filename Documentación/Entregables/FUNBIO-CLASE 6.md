# Motor GA12-N20

![Mi imagen](https://ibb.co/M5hNXc7j)

# Control de Dirección del Motor GA12-N20 con Arduino y L298N
En el primer ejemplo, podemos controlar el sentido gracias al arduino. 
El código hace que el motor gire en ambas direcciones durante un tiempo determinado y luego se detenga.
El motor alternará entre dos direcciones (horario y antihorario) durante 5 segundos en cada sentido y se detendrá por 1 segundo entre cambios de dirección.

### Declaracion de variables y pines
- IN1 (Pin 4): Controla la dirección del motor en un sentido.
- IN2 (Pin 5): Controla la dirección del motor en el sentido opuesto.

### Configuración inicial.
En la función setup(), los pines IN1 e IN2 se configuran como salidas para enviar señales al módulo L298N.

### Ciclo principal.
En la función loop(), el motor alterna entre dos direcciones:

1. Sentido Horario: IN1 en alto y IN2 en bajo.
2. Sentido Antihorario: IN1 en bajo y IN2 en alto.

El motor gira durante 5 segundos en cada dirección, y luego se detiene durante 1 segundo.

#
