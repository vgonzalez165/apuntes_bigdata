# UT00: El lenguaje de programación Python

## PR0001: Ejercicios básicos en Python

**NOTA**: entrega de por lo menos 10 ejercicios

### 1. Lectura de un número válido

Crea un programa que solicite un número por pantalla al usuario y siga pidiéndolo hasta que el usuario introduzca un número válido.


### 2. Tabla de multiplicar

Crea un programa que solicite un número `n` y un valor `k` y que muestre por la terminal los primeros `k` elementos de la tabla de multiplicar de `n`. 

- **Ejemplo**: Para `n=5` y `k=12` mostraría:
```
5 * 1 = 5
5 * 2 = 10
5 * 3 = 15
...
5 * 12 = 60
```


### 3. Triángulo de asteriscos
Crea un programa que solicite un número al usuario y dibuje un triángulo con asteriscos cuya base sea el número introducido.

- **Ejemplo**: si el número introducido es `5` el resultado será:

```
*
**
***
****
*****
```


### 4. Pirámide de asteriscos

Modifica el programa anterior para que en lugar de crear un triángulo cree una pirámide. Si el usuario introduce un número par se lo volverá a pedir hasta que introduzca un número par.

- **Ejemplo**: si el número introducido es `9` el resultado será:

```
    *
   ***
  *****
 *******
*********
```


### 5. Número mayor y menor 

Crea un programa que pida al usuario que introduzca 5 números y luego le diga cuál es el mayor y el menor de todos ellos de la forma: `El número mayor es <mayor> y el menor es <menor>`


### 6. Conversión de unidades 

Crea un programa que convierta entre diferentes unidades de longitud (milímetros, centímetros, metros y kilómetros). El usuario introducirá primero la cantidad, luego la unidad de medida en que está y finalmente la unidad de medida a la que se va a convertir.


### 7. Acierta el número

Crea un programa que genere un número aleatorio entre 0 y 100 y el usuario tenga que adivinarlo. Cada vez que el usuario introduzca un número el programa le dirá si el número es más alto o más bajo.

Para generar un número aleatorio puedes utilizar la función `randint(a, b)` que devuelve un entero aleatorio entre `a` y `b`. Para poder utilizar esta función antes tienes que importar la librería con la orden `from random import *`


### 8. Piedra, papel o tijeras

Crea un programa que implemente el clásico juego de [piedra, papel, tijeras, lagarto y spock](https://frikadas.es/piedra-papel-tijera-lagarto-spock/).

Las normas de este juego son:
- Piedra aplasta a lagarto
- Lagarto envenena a Spock
- Spock rompe las tijeras
- Tijeras decapitan al lagarto
- Lagarto come al papel
- Papek desautoriza a Spock
- Spock vaporiza la piedra
- Piedra rompe a tijeras
- Tijeras cortan papel
- Papel envuelve a piedra

En el enlace anterior puedes ver un diagrama donde tal vez veas mejor las relaciones entre las diferentes elecciones.

Ganará el primero que gane 5 manos.



### 9.- Secuencia de Fibonacci

Crea un programa que genere los primeros `n` números de la secuencia de Fibonacci. Recuerda que la secuencia de Fibonacci es:

```
fib(0) = 1
fib(1) = 1
fib(n) = fib(n-2) + fib(n-1)
```


### 10. Números primos

Crea un programa que solicite un número al usuario y le diga si es primo o no.
Un número primo solo es divisible por 1 y por sí mismo.


### 11. Factorial de un número

Crea un programa que pida un número entero `n` y calcule su factorial.
Recuerda que el factorial de un número `n` (denotado como `n!`) se define como:

```
n! = 1 * 2 * 3 * ... * n
```

* **Ejemplo**: `5! = 120`.



### 12. Contador de vocales y consonantes

Crea un programa que solicite al usuario una cadena de texto y muestre cuántas vocales y cuántas consonantes contiene.



### 13. Invertir una cadena

Crea un programa que pida al usuario una cadena de texto y muestre la misma cadena invertida.

* **Ejemplo**: `"python"` → `"nohtyp"`.


### 14. Palíndromos

Crea un programa que solicite al usuario una palabra y determine si es un palíndromo (se lee igual al derecho y al revés).

* **Ejemplo**: `"oso"` → palíndromo.
* **Ejemplo**: `"casa"` → no es palíndromo.



### 15. Números pares e impares

Crea un programa que pida al usuario un número entero positivo `n` y muestre todos los números pares e impares entre `1` y `n`.



### 16. Suma de dígitos

Crea un programa que pida al usuario un número entero y calcule la suma de todos sus dígitos.

* **Ejemplo**: `327 → 3 + 2 + 7 = 12`.



### 17. Calculadora simple

Crea un programa que pida al usuario dos números y una operación (suma, resta, multiplicación o división) y muestre el resultado.



### 18. Conversión de temperaturas

Crea un programa que convierta entre grados Celsius, Fahrenheit y Kelvin.
El usuario introducirá primero la cantidad y la unidad de origen, y después la unidad de destino.



### 19. Generador de contraseñas

Crea un programa que genere una contraseña aleatoria de una longitud que indique el usuario.
La contraseña debe incluir letras mayúsculas, minúsculas, números y símbolos especiales.



### 20. Ordenar lista de números

Crea un programa que pida al usuario una lista de números separados por comas y muestre la lista ordenada de menor a mayor.


[Volver al índice](./../bda.md)
