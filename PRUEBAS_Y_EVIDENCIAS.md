# Pruebas y evidencias - Reto 15

## 1. Prueba de escritorio del caso 01

Entrada:

```text
3 5 5 15
5 15 30 10 25
25 10 5 20 30
10 20 15 5 35
```

Para la fila 1:

- `SF = 5 + 15 + 30 + 10 + 25 = 85`
- `M = 5`
- `M*L = 5*5 = 25`

| Columna | x | M*x-SF | ¿x >= U? | ¿Evento? | Impacto |
|---:|---:|---:|:---:|:---:|---:|
| 1 | 5  | -60 | No  | 0 | 0 |
| 2 | 15 | -10 | Sí  | 0 | 0 |
| 3 | 30 | 65  | Sí  | 1 | 66 |
| 4 | 10 | -35 | No  | 0 | 0 |
| 5 | 25 | 40  | Sí  | 1 | 41 |

Resultado de la fila 1:

- Eventos: 2
- Impacto total: `66 + 41 = 107`
- Racha máxima: 1
- Inicio de la primera racha máxima: columna 3

Resumen del caso completo:

```text
FILA 1 EVENTOS 2 IMPACTO 107 RACHA 1 INICIO 3
FILA 2 EVENTOS 2 IMPACTO 97 RACHA 1 INICIO 1
FILA 3 EVENTOS 1 IMPACTO 91 RACHA 1 INICIO 5
COLUMNAS 1 0 1 0 3
PRIORIDAD 1
COLUMNA 5
```

## 2. Resultado de las pruebas proporcionadas

El programa fue compilado con:

```text
gcc -std=c11 -Wall -Wextra 20260267.c -o reto
```

Resultado de la comparación automática contra los archivos `.out` recibidos:

```text
Caso 01: PASS
Caso 02: PASS
Caso 03: PASS
Caso 04: PASS
Caso 05: PASS
Caso 06: PASS
Caso 07: PASS
Caso 08: PASS
Caso 09: PASS con una entrada equivalente de dimensión cero
Caso 10: PASS
Caso 11: PASS
Caso 12: PASS
Caso 13: PASS
Caso 14: PASS
Caso 15: PASS
Caso 16: PASS
Caso 17: PASS
```

**Nota sobre el caso 09:** en los archivos enviados en el chat estaba el archivo de salida `caso_09.out`, pero no estaba el archivo original `caso_09.in`. Para comprobar esa validación se utilizó una entrada equivalente con una dimensión igual a cero:

```text
0 1 0 0
```

La salida obtenida fue:

```text
ERROR
```

## 3. Prueba propia 1 - racha consecutiva y columna empatada

Objetivo: comprobar una racha de dos eventos consecutivos y verificar que, cuando dos columnas tienen la misma cantidad de eventos, se seleccione la columna de menor número.

Entrada:

```text
2 4 5 20
10 20 30 40
25 25 25 25
```

Salida esperada:

```text
FILA 1 EVENTOS 2 IMPACTO 82 RACHA 2 INICIO 3
FILA 2 EVENTOS 0 IMPACTO 0 RACHA 0 INICIO 0
COLUMNAS 0 0 1 1
PRIORIDAD 1
COLUMNA 3
```

Justificación: la primera fila tiene eventos en las columnas 3 y 4, formando una racha de longitud 2. Las columnas 3 y 4 quedan empatadas con un evento cada una, por lo que debe seleccionarse la columna 3.

## 4. Prueba propia 2 - empate entre dos rachas máximas

Objetivo: comprobar que, cuando una fila tiene dos rachas máximas de igual longitud, se conserve la que comienza primero.

Entrada:

```text
1 7 0 0
0 10 10 0 10 10 0
```

Salida esperada:

```text
FILA 1 EVENTOS 4 IMPACTO 124 RACHA 2 INICIO 2
COLUMNAS 0 1 1 0 1 1 0
PRIORIDAD 1
COLUMNA 2
```

Justificación: existen dos rachas de longitud 2: columnas 2-3 y columnas 5-6. Como ambas tienen la misma longitud, se debe conservar la primera, cuyo inicio es la columna 2.
