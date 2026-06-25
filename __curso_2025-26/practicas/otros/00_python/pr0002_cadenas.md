# UT00: El lenguaje de programación Python

## PR0002: Ejercicios de cadenas

**NOTA**: entrega de por lo menos 10 ejercicios

### 1. Contar vocales y consonantes

Escribe una función que reciba una cadena y cuente cuántas vocales y consonantes contiene.


### 2. Invertir una cadena

Crea un programa que invierta una cadena.


### 3. Verificar palíndromo

Escribe un programa que verifique si una cadena es un **palíndromo** (se lee igual de izquierda a derecha y de derecha a izquierda).



### 4. Contar palabras (*)

Crea una función que cuente cuántas palabras hay en una cadena, suponiendo que las palabras están separadas por espacios.


### 5. Eliminar caracteres repetidos (*)

Escribe una función que elimine los caracteres duplicados en una cadena, manteniendo solo la primera aparición de cada uno.



### 6. Mayúsculas y minúsculas

Escribe un programa que convierta las letras minúsculas de una cadena en mayúsculas y viceversa.



### 7. Invertir palabras de una cadena

Escribe un programa que invierta el orden de las palabras de una cadena, manteniendo las palabras originales intactas.



### 8. Anagrama

Crea un programa que verifique si dos cadenas son **anagramas**. Se considera que dos palabras son anagramas si tienen las mismas letras en diferente orden, por ejemplo, *lácteo* y *coleta*.



### 9. Frecuencia de caracteres

Crea una función que reciba una cadena y devuelva un diccionario con la frecuencia de cada carácter.



### 10. Quitar caracteres alfanuméricos

Escribe un programa que elimine todos los caracteres no alfanuméricos (como signos de puntuación) de una cadena.



### 11. Transformar a camelCase

Escribe un programa que transforme una cadena de palabras separadas por espacios o guiones en formato camelCase (la primera letra de cada palabra, excepto la primera, debe ser mayúscula y no debe haber espacios ni guiones).



### 12. Codificación RLE (Run-Length Enconding)

Escribe una función que implemente la codificación por longitud de ejecución (RLE), que consiste en comprimir una cadena representando las secuencias consecutivas de caracteres iguales con el carácter seguido de la cantidad de repeticiones.

Por ejemplo, la cadena `aaron` la reemplazaría por `a2r1o1n1`. Por simplicidad, puedes asumir que un carácter no se va a repetir más de 9 veces consecutivas.



### 13. Decodificar RLE

Crea una función que decodifique una cadena que ha sido comprimida usando el método RLE.



### 14. Formateo de cadenas con plantillas

Escribe un programa que tome una plantilla de cadena y un diccionario, y reemplace los marcadores en la plantilla por los valores correspondientes en el diccionario.

**Ejemplo**: la cadena `"Hola, {nombre}"` con el diccionario `{"nombre": "Victor"}` debería devolver `"Hola, Victor"`



### 15. Comparar cadenas por valor ASCII

Escribe una función que compare dos cadenas sumando el valor ASCII de cada carácter y devuelva cuál tiene un mayor valor total. Para este ejercicio ten en cuenta que la función integrada `ord()` devuelve el valor ASCII de un carácter


### 16. Contar la longitud de palabra más larga

Escribe un programa que reciba una cadena y devuelva la longitud de la palabra más larga


### 17. Formatear número con separador de miles

Escribe una función que tome un número de forma de cadena y le agregue separadores de miles.

**Ejemplo**: `"123456756"` debería convertirse en `"123.456.789"`.



### 18. Rotar caracteres de una cadena

Escribe una función que rote una cadena hacia la izquierda un número dado de veces.

**Ejemplo**: `"abcdef"` rotado 2 veces convierte la cadena en `"cdefab"`.



### 19. Eliminar espacios extra

Escribe un programa que elimine los espacios repetidos en una cadena, dejando solo un espacio entre cada palabra.

* **Ejemplo**: `"Hola    mundo   Python"` → `"Hola mundo Python"`.



### 20. Reemplazar vocales

Crea una función que reemplace todas las vocales de una cadena por un carácter dado.

* **Ejemplo**: `"hola mundo", "*" → "h*l* m*nd*"`.



### 21. Subcadenas

Escribe un programa que reciba una cadena y una subcadena y cuente cuántas veces aparece la subcadena en la cadena principal.



### 22. Primer carácter no repetido

Crea una función que encuentre el primer carácter que no se repite en una cadena.

* **Ejemplo**: `"aabccde"` → `"b"`.



### 23. Eliminar vocales

Escribe un programa que elimine todas las vocales de una cadena y devuelva el resultado.



### 24. Sufijos y prefijos

Crea un programa que pida una palabra y muestre todos los **prefijos** y **sufijos** posibles de esa palabra.

* **Ejemplo**: `"sol"` → prefijos: `s, so, sol`; sufijos: `l, ol, sol`.



### 25. Contar letras mayúsculas

Escribe una función que cuente cuántas letras mayúsculas contiene una cadena.



### 26. Insertar carácter cada n posiciones

Crea un programa que inserte un carácter dado cada `n` posiciones en una cadena.

* **Ejemplo**: `"Python", "*", 2` → `"P*y*t*h*o*n"`.



### 27. Encontrar palabra más frecuente

Escribe un programa que encuentre la palabra que más veces aparece en una cadena.



### 28. Eliminar dígitos de una cadena

Crea una función que elimine todos los números de una cadena de texto.

* **Ejemplo**: `"Py3th0n 2025"` → `"Python "`.



### 29. Verificar prefijo y sufijo

Escribe un programa que verifique si una cadena empieza con un prefijo dado o termina con un sufijo dado.



### 30. Cifrado César

Crea un programa que implemente el **cifrado César**. El usuario introducirá una cadena y un número de desplazamiento, y el programa devolverá la cadena cifrada.

* **Ejemplo**: `"abc", 3` → `"def"`.



### 31. Decodificar Cifrado César

Crea un programa que descifre una cadena que ha sido codificada con el Cifrado César, conociendo el número de desplazamiento.

[Volver al índice](./../bda.md)