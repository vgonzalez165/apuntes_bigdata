# UT00: El lenguaje de programación Python

## PR0004: Ejercicios con diccionarios

**NOTA**: entrega de por lo menos 10 ejercicios

### 1.- Buscar valor en un diccionario

Crea un diccionario de frutas y precios. Permite al usuario ingresar el nombre de una fruta y muestra su precio si existe en el diccionario, o un mensaje de que no está disponible en caso contrario.

---

### 2.- Contar elementos en un diccionario

Suponiendo un diccionario con al siguiente estructura, crea un programa que calcule cuántas categorías hay, cuántos productos tiene cada categoría y cuántos productos hay en total.

```bash
productos = {
    "Electrónica": ["Smartphone", "Laptop", "Tablet", "Auriculares", "Smartwatch"],
    "Hogar": ["Aspiradora", "Microondas", "Lámpara", "Sofá", "Cafetera"],
    "Ropa": ["Camisa", "Pantalones", "Chaqueta", "Zapatos", "Bufanda"],
    "Deportes": ["Pelota de fútbol", "Raqueta de tenis", "Bicicleta", "Pesas", "Cuerda de saltar"],
    "Juguetes": ["Muñeca", "Bloques de construcción", "Peluche", "Rompecabezas", "Coche de juguete"],
}
```

---

### 3.- Contador de frecuencias de palabras

Escribe un programa que tome una frase y use un diccionario para contar la frecuencia de cada palabra.

---

### 4.- Diccionario de listas

Supón un diccionario donde cada clave es una asignatura y el valor correspondiente una lista de estudiantes matriculados, tal como se muestra en el diccionario de ejemplo. Crea un programa que tenga un menú con tres opciones:
- Listar estudiantes matriculados en una asignatura
- Matricular un estudiante en una asignatura
- Dar de baja un estudiante de una asignatura.


```python
asignaturas = {
    "Matemáticas": ["Ana", "Carlos", "Luis", "María", "Jorge"],
    "Física": ["Elena", "Luis", "Juan", "Sofía"],
    "Programación": ["Ana", "Carlos", "Sofía", "Jorge", "Pedro"],
    "Historia": ["María", "Juan", "Elena", "Ana"],
    "Inglés": ["Carlos", "Sofía", "Jorge", "María"],
}
```

---

### 5.- Diccionario invertido

Escribe una función que tome un diccionario y devuelva otro con las claves y valores intercambiados (lo que antes eran valores ahora son claves, y viceversa). 

---

### 6.- Combinar dos diccionarios

Escribe un programa que tome dos diccionarios de productos y precios, y combine los productos comunes sumando sus precios, sin duplicar los elementos únicos.

---

### 7.- Filtrar claves y valores

Dado un diccionario de empleados y salarios, filtra e imprime solo los empleados con un salario mayor a un umbral definido.

---

### 8.- Anidación de diccionarios

Partiendo de un diccionario donde las claves son nombres de departamentos y los valores, diccionarios de empleados y sus puestos, tal como se ve en el código de ejemplo, crea un programa que permita realizar las siguientes funciones:
   - Mostrar el listado de todos los empleados de un departamento
   - Añadir un empleado a un departamento
   - Eliminar un empleado de un departamento

```python
departamentos = {
    "Recursos Humanos": {
        "Ana": "Gerente de Recursos Humanos",
        "Luis": "Especialista en Reclutamiento",
        "Elena": "Asistente de Recursos Humanos"
    },
    "Tecnología": {
        "Carlos": "Desarrollador Backend",
        "María": "Desarrolladora Frontend",
        "Pedro": "Administrador de Sistemas"
    },
    "Marketing": {
        "Sofía": "Directora de Marketing",
        "Jorge": "Especialista en SEO",
        "Laura": "Community Manager"
    },
    "Finanzas": {
        "Juan": "Analista Financiero",
        "Lucía": "Contadora",
        "Raúl": "Asesor Financiero"
    }
}
```

---

### 9.- Transformación de datos

Dado un diccionario con claves como nombres de estudiantes y valores como una lista de calificaciones, haz un programa que:
- Cree un nuevo diccionario que contenga el promedio de calificaciones para cada estudiante
- Crea otro diccionario que contengan la nota promedio en cada asignatura


```python
estudiantes = {
    "Ana": {"Matemáticas": 8.5, "Física": 9.0, "Programación": 7.8},
    "Carlos": {"Matemáticas": 9.2, "Física": 8.8, "Programación": 9.4},
    "Luis": {"Matemáticas": 7.6, "Física": 8.0, "Programación": 8.5},
    "María": {"Matemáticas": 9.5, "Física": 10.0, "Programación": 9.8},
    "Jorge": {"Matemáticas": 8.8, "Física": 8.4, "Programación": 7.9},
    "Sofía": {"Matemáticas": 9.1, "Física": 8.9, "Programación": 9.3}
}
```

---

### 10.- Diccionario de cuadrados

Crea una función que devuelva un diccionario que tenga como claves los números del 1 a `n` (siendo `n` un valor pasado como parámetro a la función) y como valores sus cuadrados.

---

### 11.- Contar caracteres

Escribe un programa que tome una cadena y use un diccionario para contar cuántas veces aparece cada carácter.

---

### 12.- Fusionar listas en un diccionario

Dadas dos listas del mismo tamaño, una de claves y otra de valores, crea un diccionario combinándolas.

* **Ejemplo**:
  `claves = ["a","b","c"]`, `valores = [1,2,3]` → `{"a":1, "b":2, "c":3}`

---

### 13.- Eliminar claves específicas

Dado un diccionario de estudiantes y sus notas, elimina todas las entradas con una nota inferior a 5.

---

### 14.- Palabra más frecuente

Crea un programa que lea un texto y devuelva la palabra que más veces aparece usando un diccionario de frecuencias.

---

### 15.- Diccionario de traducciones

Crea un programa que tenga un diccionario con traducciones de palabras en inglés a español y permita al usuario traducir una palabra.

---

### 16.- Valores únicos

Dado un diccionario, crea una función que devuelva una lista con todos los valores únicos que contiene (sin repetidos).

---

### 17.- Diccionario de listas invertido

Dado un diccionario donde los valores son listas de elementos, crea uno nuevo donde cada elemento de las listas sea una clave y sus valores sean las claves originales donde aparecía.

---

### 18.- Diccionario de números pares e impares

Escribe un programa que genere un diccionario con dos claves: `"pares"` y `"impares"`. Cada una tendrá como valor una lista con los números pares o impares del 1 al 20.

---

### 19.- Sumar valores

Dado un diccionario con productos y precios, calcula el precio total de todos los productos.

---

### 20.- Diccionario de longitudes

Escribe un programa que tome una lista de palabras y cree un diccionario donde cada palabra sea una clave y su valor la longitud de la palabra.

---

### 21.- Invertir mayúsculas y minúsculas en claves

Dado un diccionario con claves tipo string, crea otro donde las claves estén con las letras invertidas (mayúsculas ↔ minúsculas).

---

### 22.- Agrupar palabras por primera letra

Crea un programa que dado un listado de palabras, cree un diccionario agrupándolas por la primera letra.

---

### 23.- Diccionario de posiciones en lista

Dada una lista de números, genera un diccionario donde cada número sea una clave y su valor sea una lista con las posiciones en las que aparece.

* **Ejemplo**: `[2,3,2,4]` → `{2:[0,2], 3:[1], 4:[3]}`

---

### 24.- Diccionario con suma acumulada

Dada una lista de números, construye un diccionario donde las claves sean los índices y los valores la suma acumulada hasta ese índice.

* **Ejemplo**: `[2,4,6]` → `{0:2, 1:6, 2:12}`

---

### 25.- Ordenar diccionario por valores

Escribe un programa que ordene un diccionario de menor a mayor según sus valores y muestre el resultado.

---

### 26.- Diccionario de frecuencia de pares

Dada una lista de tuplas con pares (clave, valor), construye un diccionario que cuente cuántas veces aparece cada par.

* **Ejemplo**: `[("a",1), ("b",2), ("a",1), ("a",2)]` → `{("a",1):2, ("b",2):1, ("a",2):1}`


[Volver al índice](./../bda.md)