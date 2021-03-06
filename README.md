## Midnight

![alt text](https://i.imgur.com/YmgZF5V.png "Stars")

Es un lenguaje imperativo, compilado, fuertemente tipado, con alcance estático y modelo de valor. Se enfoca en ofrecer varias alternativas para expresar las mismas estructuras y soluciones. Midnight es el lenguaje de programación donde el cielo es el límite.

## Estructura

El programa más simple (vacío) que se puede escribir es:  
```
Space
EndofSpace
```
La estructura de un programa es la siguiente:
```
Space
< Definiciones del UFO, Galaxy, Comet, Satellite >
< Instrucciones >
EndofSpace
```
Dentro, se pueden escribir instrucciones. El signo de secuaciación (Colocar una instrucción para que se ejecute a continuación de otra) es `;`. La última instrucción admite ser escrita con o sin `;`.
```
Space

planet n = 5;
print(n)

EndofSpace
```

## Identificadores
No puede ser una palabra reservada. Debe empezar con una letra ya sea mayúscula o minúscula seguida por cualquier cantidad de caracteres alfanuméricos o `_`.

## Tipos
Hay tipos escalares y tipos compuestos. Las variables pueden ser declaradas en cualquier parte del código siempre que no hayan sido declaradas previamente dentro del mismo alcance. Todos los tipos escalares tienen un valor por defecto predefinido. Las palabras clave para tipos simples se escriben en minúscula mientras que las de tipos compuestos van con la primera letra mayúscula.

### Escalares

- `moon` : Tiene 2 valores posibles: `new` o `full` (no, las otras fases no las tomamos en cuenta) representados por 0 y 1 respectivamente. Default: `new`.
- `planet` : Número entero de 32 bits en complemento a 2. Default: `0`.
- `cloud`: Número de punto flotante con precisión simple. Default: `0.0`.
- `star` : Caracter ASCII de 1 byte. Default: `'A'`. Admite los caracteres especiales `\n` `\t` `\\` `\"` `\'`.
- `cosmos` : el tipo tipo.
- `vacuum` : Tipo con valor único `vac`.

```
Space

moon b = full;
planet n = 10;
cloud x = 3.14159;
star a = 'z'

EndofSpace
```

### Compuestos

- `Constellation` : Cadena de caracteres.
- Apuntadores `~` : Apuntador a un espacio de memoria en el heap.
- `Cluster` : Arreglo de tamaño fijo.
- `Quasar` : Lista implementada con TBD.
- `Nebula` : Tabla de hash (cadenas de caracteres para las claves) implementada con TBD.
- `Galaxy` : Registros.
- `UFO` : Registros variantes.
- `Comet` : Función, "método" o procedimiento.
- `Satellite` : Iterador.

```
Space

Constellation s = "osa mayor";
~planet x = bigbang(planet);
[star]Cluster A = {'a','b','c','d'};
[planet]Quasar L = [1,2,3,4,5];
[planet]Nebula = {"Juan" : 25, "María" : 31, "Wilkerman" : 27}

EndofSpace
```
### Funciones de Conversión

 funciones para convertir algunos tipos a otros: como por ejemplo terraform(n) donde n es un Contellation y retorna un Planet con el contenido de Constellation:  
- `terraform` : De `Constellation` a `planet`.
- `recombine` : De `Constellation` a `cloud`.
- `vaporize` : De `planet` a `cloud`.
- `collapse` : De `cloud` a `planet`.
- `astral` : De cualquier tipo a `Constellation`.

```
Space
Constellation s = "1";
Planet n = 1;
print(n+terraform(s));
```

### Print y Read
Las funciones `print` y `read` escriben y leen de la consola respecticamente. `read` lee únicamente el tipo `Constellation` pero posteriormente puede convertirse a otros tipos.
```
Space

print("Introduzca un número");
Constellation input = read();
planet n = terraform(input);
print(2^n)

EndofSpace
```

### Cluster
Los `Cluster` pueden definirse por extensión (colocando cada elemento) o inicializarse con un entero que de su tamaño (en cuyo caso tiene el valor por defecto en todas las posiciones.
```
Space

[planet]Cluster A = {0,1,2,3,4};
[planet]Cluster B = Cluster(5) planet;
orbit i around range(0,5) {
  B[i] = i;
}

EndofSpace
```

### Quasar
Los `Quasar` (listas) se pueden definir por extensión. Se les puede insertar un elemento utilizando `.add(x,n)` donde x es el elemento a insertar y n la posición para insertarlo en la lista, podemos utilizar `.add(x)` para agregar el elemento al final de la lista. `.pop(x,n)`|`.pop(x)` es análogo para eliminar (y la expresión se evalúa al elemento removido). Para acceder al elemento `i` del `Quasar` `Q` se utiliza `Q[i]` (igual que un arreglo).
```
Space

[planet]Quasar A = [0,1,2,3,4];
A.add(5);
A.pop(2)

EndofSpace
```

### Nebula
`Nebula`es una tabla de hash o diccionario. Las claves son de tipo `Constellation` y se les puede insertar elementos. La sintaxis para las operaciones de insertar, eliminar y acceder son análogas a las de `Quasar` pero utilizando claves de tipo `Constellation` en lugar de índices de tipo `planet`.
```
Space
[planet]Nebula N = {"perro" : 33, "gato" : 55};
N["vaca"] = 77
EndofSpace
```

### Slices
Tanto `Quasar` como `Cluster` admiten slices. La notación es `[inicio..fin]` donde `inicio` y `fin` son índices y `fin` no está incluído, es decir el intervalo `[inicio,fin)`. Si es de la forma `[..fin]` entonces se empieza desde el índice 0 (el primero). Si es de la forma `[inicio..]` entonces se empieza desde el índice 0 (el primero).
```
Space
[planet]Quasar A = [51,0,1,2,3,4,79];
[planet]Quasar B = A[1..6]
EndofSpace
```

### Scale
Los tipos`Quasar`, `Cluster`, `Nebula`, `Constellation` admiten el uso de la función `scale()` que da la longitud (o cantidad de elementos que contiene).
```
Space
[planet]Quasar A = [0,1,2,3,4];
planet x = scale(A)
EndofSpace
```

### Apuntadores
El signo `~` se coloca antes de un tipo para indicar que es un apuntador a ese tipo. Por ejemplo, una variable de tipo `~planet` es un apuntador a una de tipo `planet`. La función `bigbang` recibe un tipo y retorna un apuntador a ese tipo. `~` también sirve para desreferenciar. `blackhole` es el apuntador nulo, equivalente al `null` de otros lenguajes.
```
Space
~planet z = bigbang(planet);
planet x = ~z;
z = blackhole;
EndofSpace
```

### Galaxy
Un `Galaxy` es un registro que agrupa varios tipos en uno.
```
Space
Galaxy Perro{
    Constellation nombre;
    planet edad;
    Constellation raza
}
Galaxy Perro firulais;
firulais.nombre = "Firulais";
firulais.edad = 9;
firulais.raza = "dálmata"
EndofSpace
```

### UFO
Un `UFO` es un registro variante que crea una disyunción de tipos.
```
Space
UFO numero { 
    planet int; 
    cloud float
}
UFO numero n;
n.int = 42;
n.float = 2.72
EndofSpace
```

## Control de flujo

### Selección
Utiliza los esquemas `if`-`else if`-`else` típicos. Además se incluye `unless` que es equivalente a un "if not".
```
Space
moon m = full;
if (m) {
    print("perro");
}
else if (1==1) {
    print("gato");
}
else {
    print("vaca");
}
unless (m) {
    print("sapo");
}
EndofSpace
```

### Repetición Indeterminada
`orbit while` itera hasta que se deje de cumplir una condición (que el tipo de una expresión `moon` pase a ser `new`) mientras que `orbit until` itera hasta que se cumpla la condición dada. `orbit(;;;)` es análogo a un for tipo C.
```
Space
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

orbit(planet k=0 ; k < 6 ; k+=1) {
    print(k)
}
EndofSpace
```

### Repetición Determinada
La notación para la repetición determinada es `orbit i around X` donde i es la variable de la repetición y X un `Quasar`, o `Satellite` sobre el cual se desea iterar. También está `orbit i around range(begin, end, step)` que admite entre 1 y 3 argumentos enteros (en caso de dar menos de 3, se comporta igual que los slices). Las variables de iteración pueden ser modificadas por el programador pero se les automáticamente asigna el valor siguiente al final de cada iteración, garantizado así que sea determinada (similar a Python).
```
Space
[cloud]Quasar L = [0.1, 0.15, 0.2, 0.25, 0.3]
orbit i around L {
    print(i);
}
orbit i around range(0,5) {
    print(i);
}
EndofSpace
```

### break y continue
Estando dentro de un ciclo (o dentro de varios ciclos anidados) se puede utilizar la instrucción especial `break n`, donde n es un `planet` > 0, para detener los n ciclo anidados más internos y continuar la ejecución afuera del más externo de los ciclos detenidos. Si se omite `n` se tratará como `break 1`. `continue` es similar pero en lugar de terminar el ciclo completo, termina solo la iteración actual.
```
Space
[[planet]Cluster]Cluster M = {{1,2,3},{4,5,6},{7,8,9}};
orbit i around range(3) {
    orbit j around range(3) {
        if M[i][j] == 7 {
            print(i);
            print(j);
            break 2
        }
    }
}
EndofSpace
```

### Subrutinas
Midnight tiene subrutinas (`Comet`) de segunda clase, lo que quiere decir que se pueden guardar en una variable y pasar como parámetro pero no retornarlas en una función. Un procedimiento es una función que retorna `vac` (en caso de colocarse un `return` solo, se interpreta como como `return vac` y en caso de no haber return, la subrutina siempre retorna `vac`). Para indicar que se quiere pasar un parámetro por referencia en lugar de por valor se debe poner un `@`.
```
Space
Comet halley(planet n) -> vacuum {
    print("Este es un procedimiento");
    print(n);
}

Comet twice(planet n) -> planet {
    print("Esta es una Función");
    return 2*n;
}

(planet -> planet) Comet f = twice;
planet z = f(2);
EndofSpace

Comet double(planet @n) -> blackhole {
    n *= 2
}
```

### Iteradores
Los  `Satellite` son similares a las subrutinas pero utilizan la palabra clave `yield` en lugar de return. Esto permite que el iterador "recuerde" en que línea se quedó y continúe desde ahí cuando se llame otra vez. No admiten recursión ni directa ni indirecta.
```
Space
Satellite Primos() -> planet {
    [planet]Quasar L = [];
    planet p = 2;
    orbit while(full) {
        moon esprimo = full;
        orbit q around L {
            if (p%q == 0) {
                esprimo = new;
                break;
            }
        }
        if (esprimo) {
            yield p;
            L.add(p);
        }
        p += 1;
    }
}

[planet]Satelline generador_primos = Primos();
print("esto no va a parar jaja salu2");
orbit p around generador_primos {
    print(p);
}
EndofSpace
```

## Operadores
`==`: igualdad.  
`¬=`: desigualdad.  
`=`: asignación.  

### Operadores aritméticos
`+`: adición.  
`-`: substrancción.  
`*`: producto.  
`^`: potencia.  
`/`: división.  
`//`: división entera.  
`%`: resto de la división entera.  
`+=`, `-=`, `*=`, `^=`, `/=`, `//=`, `%=`: aplicar y asignar. Ejemplo: `i += 1` es lo mismo que `i = i+1`.  
`>`: mayor que.  
`<`: menor que.  
`>=`: mayor o igual.  
`<=`: menor o igual.

### Operadores lógicos
`&&`: and con cortocircuito.  
`&`: and sin cortocircuito.  
`||`: or con cortocircuito.  
`|`: or sin cortocircuito.  
`¬`: negación.  

## Extras
Estas son ideas de características para añadirle al lenguaje si da tiempo:  
- Quitar las restricciones de los iteradores.
- Funciones de primera clase.
- Polimosfismo paramétrico.
- Listas por comprensión.
