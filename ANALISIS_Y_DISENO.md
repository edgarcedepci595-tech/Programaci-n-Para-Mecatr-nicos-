# Análisis y diseño - Reto 15

**Estudiante:** Edgar Yosmar Carrero Peguero  
**Matrícula:** 2026-0267  
**Reto:** Comedor: demanda superior al promedio propio

## 1. Problema a resolver

El programa recibe una matriz de raciones servidas. Cada fila representa un comedor o entidad y cada columna representa un día. Para cada posición se debe determinar si genera un evento comparando el valor con el promedio de su propia fila sin realizar divisiones ni redondeos.

La condición exacta del evento es:

`M*x - SF >= M*L && x >= U`

Donde:
- `M`: cantidad de columnas.
- `x`: valor actual de la matriz.
- `SF`: suma de la fila actual.
- `L`: diferencia mínima sobre el promedio.
- `U`: límite mínimo que también debe cumplir el valor.

Si la posición genera evento, su impacto es:

`M*x - SF + 1`

## 2. Entradas

Primera línea:

`N M L U`

Después se leen `N` filas con `M` enteros cada una.

## 3. Restricciones y validaciones

- `1 <= N <= 30`
- `1 <= M <= 30`
- `0 <= L <= U <= 1000`
- Cada valor de la matriz debe estar entre `0` y `1000`.
- Si una restricción falla, la única salida debe ser `ERROR`.
- Las dimensiones se validan antes de leer la matriz.

## 4. Salidas

Para cada fila se imprime:

`FILA i EVENTOS e IMPACTO s RACHA r INICIO b`

Después:

`COLUMNAS c1 c2 ... cM`

`PRIORIDAD f`

`COLUMNA k`

Los índices impresos comienzan en 1. Si no existe ningún evento en toda la matriz, `PRIORIDAD` y `COLUMNA` valen 0.

## 5. Variables y arreglos principales

- `matriz[30][30]`: almacena los datos originales.
- `eventosFila[30]`: cantidad de eventos de cada fila.
- `impactoFila[30]`: suma de impactos por fila.
- `rachaMax[30]`: longitud de la mayor racha de eventos de cada fila.
- `inicioRacha[30]`: posición inicial de la mayor racha.
- `eventosColumna[30]`: cantidad de eventos por columna.
- `SF`: suma de la fila actual.
- `rachaActual`: longitud de la racha que se está recorriendo.
- `inicioActual`: inicio de la racha actual.
- `totalEventos`: cantidad total de eventos de toda la matriz.
- `filaPrioritaria`: índice de la fila que gana los criterios de prioridad.
- `columnaDestacada`: índice de la columna con más eventos.

Se usa `long` para las sumas e impactos y `int` para dimensiones, índices, valores y conteos.

## 6. Pseudocódigo general

```text
INICIO
    Leer N, M, L, U

    Si N o M están fuera de 1..30
        Imprimir ERROR
        Terminar
    FinSi

    Si L < 0, U < 0, L > U o U > 1000
        Imprimir ERROR
        Terminar
    FinSi

    Para cada fila i
        Para cada columna j
            Leer matriz[i][j]
            Si el valor está fuera de 0..1000
                Imprimir ERROR
                Terminar
            FinSi
        FinPara
    FinPara

    Inicializar vectores de resumen en 0
    totalEventos = 0

    Para cada fila i
        SF = suma de todos los valores de la fila i
        rachaActual = 0
        inicioActual = 0

        Para cada columna j
            x = matriz[i][j]

            Si M*x - SF >= M*L Y x >= U
                impacto = M*x - SF + 1

                eventosFila[i]++
                impactoFila[i] += impacto
                eventosColumna[j]++
                totalEventos++

                Si rachaActual == 0
                    inicioActual = j + 1
                FinSi

                rachaActual++

                Si rachaActual > rachaMax[i]
                    rachaMax[i] = rachaActual
                    inicioRacha[i] = inicioActual
                FinSi
            SiNo
                rachaActual = 0
            FinSi
        FinPara
    FinPara

    Si totalEventos > 0
        Elegir fila prioritaria por:
            1. mayor racha
            2. mayor impacto total
            3. mayor cantidad de eventos
            4. menor número de fila

        Elegir columna destacada por:
            1. mayor cantidad de eventos
            2. menor número de columna
    FinSi

    Imprimir los resúmenes de todas las filas
    Imprimir el vector COLUMNAS

    Si totalEventos == 0
        Imprimir PRIORIDAD 0
        Imprimir COLUMNA 0
    SiNo
        Imprimir la fila prioritaria usando índice desde 1
        Imprimir la columna destacada usando índice desde 1
    FinSi
FIN
```

## 7. Manejo de rachas y empates

Las rachas se recorren horizontalmente. Cada evento incrementa `rachaActual`. Cuando aparece una posición sin evento, `rachaActual` vuelve a 0.

La mayor racha solo se reemplaza cuando la nueva longitud es estrictamente mayor. De esta forma, si dos rachas tienen la misma longitud máxima, se conserva automáticamente la que comenzó primero.

Para la fila prioritaria se recorre desde la fila 1 hacia la última. Solo se cambia de fila cuando una fila posterior mejora alguno de los criterios de desempate. Si todos los criterios quedan iguales, se conserva la fila de menor número.

Para las columnas se aplica la misma idea: solo se cambia si una columna posterior tiene estrictamente más eventos, por lo que un empate conserva la columna de menor número.
