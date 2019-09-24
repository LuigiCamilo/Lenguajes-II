## Midnight

![alt text](https://i.imgur.com/YmgZF5V.png "Stars")

Es un lenguaje imperativo, compilado, fuertemente tipado, con alcance estático. Se enfoca en ofrecer varias alternativas para expresar las mismas estructuras y soluciones. Midnight es el lenguaje de programación donde el cielo es el límite.

## Estructura

El programa más simple (vacío) que se puede escribir es:  
```
[]
```
Dentro, se pueden escribir instrucciones. El signo de secuenciación (Colocar una instrucción para que se ejecute a continuación de otra) es `;`.
```
[
int n = 5;
print(n)
]
```

## Tipos

Hay tipos escalares y compuestos. Las variables pueden ser declaradas en cualquier parte del código siempre que no hayan sido declaradas previamente dentro del mismo alcance. Todos los tipos escalares tienen un valor por defecto. Las palabras clave para tipos simple se escriben en minúscula mientras que las de tipos compuestos van con la primera letra mayúscula.

### Escalares

- `moon` : Tiene 2 valores posibles: `new` o `full` (no, las otras fases no las tomamos en cuenta) representados por 0 y 1 respectivamente. Default: `new`.
- `planet` : Número entero de 32 bits en complemento a 2. Default: `0`.
- `cloud`: Número de punto flotante con precisión simple. Default: `0.0`.
- `star` : Caracter ASCII de 1 byte. Default: `'A'`.
- `blackhole` : Tipo con valor único `blackhole`.
- `cosmos` : el tipo tipo.

```
[
moon b = full;
planet n = 10;
cloud x = 3.14159;
star a = 'z';
]
```

### Compuestos

- `Constellation` : Cadena de caracteres.
- Apuntadores `~` : Apuntador a un espacio de memoria en el heap. <- (sujeto a cambios)
- `Cluster` : Arreglo de tamaño fijo.
- `Quasar` : Lista implementada con TBD.
- `Nebula` : Tabla de hash (cadenas de caracteres para las claves) implementada con TBD.
- `Galaxy` : Registros.
- `UFO` : Registros variantes.
- `Comet` : Función, "método" o procedimiento.
### Extras:
- `Satellite` : Iterador.

```
[
Constellation s = "osa mayor";
~planet x = bigbang(scale(planet));
[star]Cluster A = ('a','b','c','d');
[planet]Quasar L = [1,2,3,4,5];
[planet]Nebula = {"Juan" : 25, "María" : 31, "Wilkerman" : 27}
]
```

### Cluster
Los `Cluster` pueden definirse por extensión (colocando cada elemento) o inicializarse con un entero que de su tamaño (en cuyo caso tiene el valor por defecto en todas las posiciones.
```
[
[planet]Cluster A = (0,1,2,3,4);
[planet]Cluster B = Array(5) of int;
orbit i around range(0,5) {
  B[i] = i;
}
]
```

### Quasar
Los `Quasar` (listas) se pueden definir por extensión o por comprensión. Se les puede insertar un elemento utilizando `.add(x,n)` donde x es el elemento a insertar y n la posición para insertarlo en la lista. `.pop(x,n)` es análogo para eliminar (y la expresión se evalúa al elemento removido). Para acceder al elemento `i` del `Quasar` `Q` se utiliza `Q[i]` (igual que un arreglo).
```
[
[planet]Quasar A = [0,1,2,3,4];
[planet]Quasar B = [2*i with orbit i around range(4)];
B.add(4)
]
```

### Nebula
`Nebula`es una tabla de hash o diccionario. Las claves son de tipo `Constellation` y se les puede insertar elementos. La sintaxis para las operaciones de insertar, eliminar y acceder son análogas a las de `Quasar` pero utilizando claves de tipo `Constellation` en lugar de índices de tipo `planet`.
```
[
[planet]Nebula N = {"perro" : 33, "gato" : 55};
N["vaca"] = 77
]
```

### Slices
Tanto `Quasar` como `Cluster` admiten slices. La notación es `[inicio..fin]` donde `inicio` y `fin` son índices y `fin` no está incluído, es decir el intervalo `[inicio,fin)`. Si es de la forma `[..fin]` entonces se empieza desde el índice 0 (el primero). Si es de la forma `[inicio..]` entonces se empieza desde el índice 0 (el primero).
```
[
[planet]Quasar A = [51,0,1,2,3,4,79];
[planet]Quasar B = A[1..6]
]
```

### Scale
Los tipos`Quasar`, `Cluster`, `Nebula`, `Constellation` admiten el uso de la función `scale()` que da la longitud (o cantidad de elementos que contiene). El tipo `cosmos` también la admite pero en lugar de retornar la longitud, retorna la cantidad de memoria que ocupa ese tipo.
```
[
[planet]Quasar A = [0,1,2,3,4];
planet x = scale(A)
]
```

### Apuntadores
El signo `~` se coloca antes de un tipo para indicar que es un apuntador a ese tipo. Por ejemplo, una variable de tipo `~planet` es un apuntador a una de tipo `planet`. La función `bigbang` permite reservar memoria en el heap. `~` también sirve para desreferenciar.
```
[
~planet z = bigbang(scale(planet));
planet x = ~z;
]
```

### Galaxy
Un `Galaxy` es un registro que agrupa varios tipos en uno.
```
[
Galaxy Perro{
    Constellation nombre;
    planet edad;
    Constellation raza
} firulais;
firulais.nombre = "Firulais";
firulais.edad = 9;
firulais.raza = "dálmata"
]
```

### UFO
Un `UFO` es un registro variante que crea una disyunción de tipos.
```
[
UFO numero { int ; float }
UFO numero n = 5;
UFO numero x = 2.72;
]
```

## Control de flujo

### Selección


### Repetición Indeterminada
`orbit while` itera hasta que se deje de cumplir una condición (que el tipo de una expresión `moon` pase a ser `new`) mientras que `orbit until` itera hasta que se cumpla la condición dada. `orbit(;;;)` es análogo a un for tipo C.
```
[
planet i = 0;
orbit while (i < 6) {
    print(i);
    i++
}

planet j = 0;
orbit until (j >= 6) {
    print(j);
    j++
}

orbit(int k=0 ; k < 6 ; k++) {
    print(k)
}
]
```
