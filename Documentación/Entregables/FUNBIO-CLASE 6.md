# Motor GA12-N20

![33de9920-c7e9-479c-9225-b2bccb4ec758](https://github.com/user-attachments/assets/ce74e97b-7860-4d53-ba3f-d0fb04bf25d1)


## Control de Dirección del Motor GA12-N20 con Arduino y L298N
En el primer ejemplo, podemos controlar el sentido gracias al arduino. 
El código hace que el motor gire en ambas direcciones durante un tiempo determinado y luego se detenga.
El motor alternará entre dos direcciones (horario y antihorario) durante 5 segundos en cada sentido y se detendrá por 1 segundo entre cambios de dirección.

### Declaración de variables y pines
- IN1 (Pin 4): Controla la dirección del motor en un sentido.
- IN2 (Pin 5): Controla la dirección del motor en el sentido opuesto.

### Configuración inicial.
En la función setup(), los pines IN1 e IN2 se configuran como salidas para enviar señales al módulo L298N.

### Ciclo principal.
En la función loop(), el motor alterna entre dos direcciones:

1. Sentido Horario: IN1 en alto y IN2 en bajo.
2. Sentido Antihorario: IN1 en bajo y IN2 en alto.

El motor gira durante 5 segundos en cada dirección, y luego se detiene durante 1 segundo.

Vídeo del ejemplo: https://drive.google.com/file/d/18-9rKbZD-BaE5GWGU8yZY33rjeTv7_24/view?usp=sharing

## Control de Velocidad del Motor GA12-N20 con Potenciómetro y Arduino

En este ejemplo, nos permite controlar la velocidad de un motorreductor DC tipo GA12-N20 utilizando un potenciómetro conectado a una entrada analógica de Arduino.
El propósito de este código es ajustar la velocidad de un motor de corriente continua en función de la posición de un potenciómetro. La lectura analógica del potenciómetro se convierte en una señal PWM que controla la velocidad del motor, y el valor se muestra en el monitor serial.

### Declaración de variables y pines
- ENA (Pin 3): Pin PWM para controlar la velocidad del motor.
- IN1 (Pin 4): Controla la dirección del motor en un sentido.
- IN2 (Pin 5): Controla la dirección del motor en el sentido opuesto.
- POT (Pin A0): Pin analógico para leer la posición del potenciómetro.

### Configuración inicial.
En la función setup(), se configuran los pines como salidas para controlar la dirección y velocidad del motor, y se inicializa la comunicación serial para mostrar los datos. Además, se establece la dirección del motor a sentido horario al principio.

### Ciclo principal.
En la función loop(), se lee el valor del potenciómetro, se convierte a un valor PWM (de 0 a 255) y se aplica al pin ENA para ajustar la velocidad del motor. También se muestran los valores en el monitor serial.

Vídeo del ejemplo: https://drive.google.com/file/d/1qzxMIo_lx5PQPwi4nMcTK-50JEh6y9a_/view?usp=sharing

## Feedback Háptico con FSR y Motor Vibrador
El  proyecto utiliza un sensor FSR para generar una señal de vibración proporcional a la presión aplicada sobre el sensor. A medida que se aplica más fuerza, la intensidad del motor vibrador aumenta mediante una señal PWM. 

### Declaración de Variables y Pines

- pinFSR (A0): Pin analógico para leer la señal del sensor FSR.
- pinMotor (Pin 3): Pin PWM para controlar la intensidad del motor vibrador.
- umbral (50): Umbral mínimo de lectura del FSR para activar la vibración.
- promedioN (10): Número de muestras para realizar un promedio simple y reducir el ruido.

### Configuración Inicial
En la función setup(), se configuran los pines y se inicializa la comunicación serial para poder monitorear los datos de entrada y salida. Además, se inicializa el buffer con valores cero para el cálculo del promedio.

### Ciclo principal
En la función loop(), el sistema realiza lo siguiente:

1. Leer valor del FSR: Se obtiene una nueva lectura del sensor FSR y se guarda en un buffer para calcular el promedio.
2. Promediar las lecturas: Se calcula el promedio de las últimas 10 lecturas para suavizar los datos.
3. Evaluar presión: Si la lectura filtrada supera el umbral, se convierte en una señal PWM para controlar la vibración del motor.
 - Se aplica un mapeo cuadrático para hacer el sistema más sensible a bajas presiones.
 - El valor PWM se ajusta entre 0 y 255.

Finalmente, se aplica el valor PWM al motor y se muestran los datos en el monitor serial.

![408126d9-ca06-4326-ba41-70fdbf50cba2](https://github.com/user-attachments/assets/d0dd4a3a-d906-4e4f-9718-61ccd1711e0c)
![280c12b4-9ac0-483e-b4d3-8f9f827d2c94](https://github.com/user-attachments/assets/e11e4ed0-8655-4000-b1b7-83ac5956f37e)

# Servomotor DS3235

![fa6c8d85-cf57-4238-921a-f03f1022dc17](https://github.com/user-attachments/assets/a6adb088-97e5-443f-b540-e71f5c0ef590)

## Control del Servomotor DS3235 mediante Potenciómetro y PWM

Este ejemplo nos permite controlar la posición angular de un servomotor DS3235 utilizando un potenciómetro conectado a un pin analógico de un Arduino. La señal leída del potenciómetro se convierte directamente en una señal PWM, la cual se envía al servomotor mediante la función writeMicroseconds(). Además, el ángulo estimado del servomotor se calcula y se visualiza en el monitor serial.

### Declaración de Variables y Pines

- miServo: Objeto de la librería Servo para controlar el servomotor.
- ADC_MIN y ADC_MAX: Valores mínimos y máximos de la lectura analógica del potenciómetro (0 a 1023).
- PULSO_MIN y PULSO_MAX: Los valores de PWM en microsegundos para controlar el servomotor (500 µs para 0° y 2400 µs para ~265°).
- ANGULO_MAX: El ángulo máximo estimado del servomotor (~265°).

### Configuración Inicial
En la función setup(), se conecta el servomotor al pin 3 y se inicializa la comunicación serial para mostrar los valores en el monitor serial.

### Ciclo Principal (loop())
En la función loop(), el sistema realiza lo siguiente:

1. Leer valor del potenciómetro: Se obtiene una lectura del potenciómetro en formato ADC (0-1023).
2. Convertir ADC a PWM: Se convierte el valor ADC a un valor PWM en microsegundos (500 µs a 2400 µs) usando la función map().
3. Controlar el servomotor: Se envía el valor PWM al servomotor usando la función writeMicroseconds().
4. Calcular ángulo estimado: Se calcula el ángulo estimado basado en el valor PWM.
5. Mostrar en el monitor serial: Se muestran los valores del ADC, PWM y el ángulo estimado.

![b7feb399-6b6f-48e8-92ca-39a5530063f1](https://github.com/user-attachments/assets/6829af0d-d1ba-4ddf-b68a-4e8619317c10)

## Control de Posición del Servomotor DS3235 con Arduino
Este ejemplo permite controlar la posición angular de un servomotor de alto torque DS3235 utilizando la función writeMicroseconds() de la librería Servo. Se programan cuatro posiciones representativas (0°, 90°, 180° y 270°) con valores de pulso personalizados, adecuados para servos con mayor rango que los SG90 estándar. Este tipo de actuadores es útil en aplicaciones como ortesis robóticas o dispositivos de asistencia mecánica en rehabilitación.

### Declaración de Variables y Pines
- miServo: Objeto de la librería Servo para controlar el servomotor.
- El servomotor está conectado al pin 3 de Arduino

### Configuración Inicial
En la función setup(), se conecta el servomotor al pin 3.

### Ciclo Principal
En la función loop(), el servomotor se mueve a las siguientes posiciones con un retardo de 5 segundos entre cada una:

0°: 500 microsegundos
90°: 1180 microsegundos
180°: 1800 microsegundos
270°: 2400 microsegundos

![a6a3981d-28d8-421c-b5c8-c34cd9a3ce78](https://github.com/user-attachments/assets/7fea07de-8c52-490c-9e05-2d154c154b8c)

## Guante de Control para Prótesis Robótica con Sensor Flex y Servomotor
Este proyecto demuestra cómo controlar un servomotor DS3235 utilizando un sensor flex colocado en un dedo de un guante, simulando el control de una articulación robótica tipo prótesis. Al flexionar el dedo, el sensor genera una señal analógica que se convierte en una señal PWM proporcional, haciendo que el servomotor imite el movimiento. Este sistema se basa en principios de biodiseño y en la interacción entre la electrónica y los actuadores.

### Declaración de Variables y Pines
- servoProtesis: Objeto de la librería Servo para controlar el servomotor.
- PULSO_MIN y PULSO_MAX: Los valores de PWM en microsegundos que corresponden a los ángulos 0° y 265° respectivamente.
- ANGULO_MAX: El ángulo máximo estimado del servomotor (~265°).
- pinFlex: El pin A0 al que está conectado el sensor flex.

### Configuración Inicial (setup())
En la función setup(), se conecta el servomotor al pin 3 de Arduino y se inicializa la comunicación serial para mostrar los valores en el monitor serial.

### Ciclo Principal
En la función loop(), el sistema realiza lo siguiente:

1. Leer el valor del sensor flex: Se obtiene una lectura analógica del sensor flex conectado a A0.
2. Convertir el valor ADC a PWM: El valor leído se convierte en un valor PWM utilizando la función map() para que se ajuste a los límites definidos de PULSO_MIN y PULSO_MAX.
3. Calcular el ángulo estimado: El ángulo estimado del servomotor se calcula para visualización en el monitor serial.
4. Enviar el valor PWM al servomotor: El valor PWM se envía al servomotor mediante la función writeMicroseconds().
5. Mostrar los valores en el monitor serial: Se imprimen en el monitor serial los valores del ADC, el PWM y el ángulo estimado.

 ![16c69f52-d26b-4c14-85f2-f53774894d10](https://github.com/user-attachments/assets/a69d1191-aba2-49e5-b5fc-024316e60503)

