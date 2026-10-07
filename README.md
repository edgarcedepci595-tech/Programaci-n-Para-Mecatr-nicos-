# Reto 15 - Comedor: demanda superior al promedio propio

**Estudiante:** Edgar Yosmar Carrero Peguero  
**Matrícula:** 2026-0267  
**Sección:** Miércoles  
**Práctica:** Parcial no. 1  
**Fecha:** 06/10/2026

Repositorio de la práctica:  
https://github.com/edgarcedepci595-tech/Programaci-n-Para-Mecatr-nicos-.git

## Contenido

- `20260267.c`: programa principal en C.
- `ANALISIS_Y_DISENO.md`: análisis, variables, restricciones y pseudocódigo.
- `PRUEBAS_Y_EVIDENCIAS.md`: prueba de escritorio, resultados y dos pruebas propias.
- `GUIA_EXPLICACION_ORAL.md`: guía para explicar el programa.
- `pruebas/`: casos de prueba proporcionados por el profesor que fueron recibidos.
- `pruebas_propias/`: dos casos creados para complementar la evidencia.

## Compilación

```bash
gcc -std=c11 -Wall -Wextra 20260267.c -o reto
```

## Ejecución de un caso

```bash
./reto < pruebas/caso_01.in
```

La salida del programa no contiene preguntas ni mensajes adicionales, porque debe coincidir exactamente con los archivos `.out`.

## Nota sobre caso 09

En los archivos recibidos estaba `caso_09.out`, pero no el `caso_09.in` original. Para verificar la validación de dimensión cero se creó `pruebas/caso_09_equivalente.in` con una entrada equivalente. No se presenta como el archivo original del profesor.
