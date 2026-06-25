```python
n = input("Indica el valor n: ")
k = input("Indica el valor k: ")
for i in range(1, (int(k)+1)):
    print( n + " * " + str(i) + "=" + str(int(n)*i) )
```

    Indica el valor n:  5
    Indica el valor k:  12


    5 * 1=5
    5 * 2=10
    5 * 3=15
    5 * 4=20
    5 * 5=25
    5 * 6=30
    5 * 7=35
    5 * 8=40
    5 * 9=45
    5 * 10=50
    5 * 11=55
    5 * 12=60


### 


```python
n = input("Indica el valor n: ")
for i in range(int(n)):
    print( "*"*(i+1) )
```

    Indica el valor n:  6


    *
    **
    ***
    ****
    *****
    ******



```python
par = True
while par:
    n = int(input("Indica el valor n: "))
    par = (n % 2) == 0
    print(par)
for i in range(1, (n+1), 2):
    num_spaces = int((n - i) / 2)
    print( (" "*num_spaces) + "*"*i )
```

    Indica el valor n:  25


    False
                *
               ***
              *****
             *******
            *********
           ***********
          *************
         ***************
        *****************
       *******************
      *********************
     ***********************
    *************************



```python
int(5 / 2)
```




    2




```python
from random import *

puntos_cpu = 0
puntos_user = 0

while (puntos_cpu < 5) and (puntos_user < 5):
    rand = randint(0, 2)
    elec_cpu = 'piedra' if rand==0 else 'papel' if rand==1 else 'tijeras'
    elec_user = input("Elije piedra, papel o tijeras: ")
    # Determinamos quien ha ganado
    match (elec_user):
        case 'piedra':
            gana = ('cpu' if elec_cpu == 'papel' else
                    'user' if elec_cpu == 'tijeras' else
                    'empate')
        case 'papel':
            gana = ('cpu' if elec_cpu == 'tijeras' else
                    'user' if elec_cpu == 'piedra' else
                    'empate')
        case 'tijeras':
            gana = ('cpu' if elec_cpu == 'piedra' else
                    'user' if elec_cpu == 'papel' else
                    'empate')
    # Mostramos el resultado
    print("Tu elección: " + elec_user + "  - Mi elección: " + elec_cpu)
    if (gana == 'cpu'):
        puntos_cpu += 1
        print("He ganado esta mano.")
    elif (gana == 'user'):
        puntos_user += 1
        print("Has ganado esta mano.")
    else:
        print("Hemos empatado.")

print("PUNTUACIÓN FINAL: \nYo: " + str(puntos_cpu) + " puntos.  Tú:" + str(puntos_user) + " puntos.")

```

    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: tijeras
    Has ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: piedra
    Hemos empatado.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: papel
    He ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: papel
    He ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: papel
    He ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: tijeras
    Has ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: piedra
    Hemos empatado.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: tijeras
    Has ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: tijeras
    Has ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: papel
    He ganado esta mano.


    Elije piedra, papel o tijeras:  piedra


    Tu elección: piedra  - Mi elección: tijeras
    Has ganado esta mano.
    PUNTUACIÓN FINAL: 
    Yo: 4 puntos.  Tú:5 puntos.



```python
n = input("Dime el número de elementos a generar: ")
a = 1
print("1 - " + str(a))
b = 1
print("2 - " + str(b))
for i in range(3, int(n)+1):
    c = a + b
    print("3 - " + str(c))
    a = b
    b = c
    
```

    Dime el número de elementos a generar:  9


    1 - 1
    2 - 1
    3 - 2
    3 - 3
    3 - 5
    3 - 8
    3 - 13
    3 - 21
    3 - 34



```python

```
