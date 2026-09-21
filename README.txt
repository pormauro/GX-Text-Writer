# GX Text Writer V3 - Ladder Keys

No usa LD/OUT textual. Usa teclas de GX Works:

- [NO M8001] -> F5 + M8001 + Enter
- [NC M200] -> F6 + M200 + Enter
- [COIL M200] -> F7 + M200 + Enter
- [APP MOV K10 D100] -> F8 + MOV K10 D100 + Enter

## Uso
1. Abrí GX Works en Ladder.
2. Hacé clic en una celda vacía.
3. Cargá Test simple.
4. Apretá F8 en el programa.
5. En 3 segundos volvé a hacer clic en GX.

Si GX corre como administrador, ejecutá este programa como administrador.

## Crear EXE
Ejecutá build_exe.bat. Queda en dist\GX_Text_Writer_V3.exe

## Regla obligatoria SET / RST

En el Ladder generado para este flujo, cada dispositivo destino puede aparecer como máximo:

- una sola vez con SET en todo el programa;
- una sola vez con RST en todo el programa.

Ejemplo válido:
- [APP SET M18] aparece una sola vez.
- [APP RST M18] aparece una sola vez.

Ejemplo inválido:
- dos o más [APP SET M18] en rungs distintos;
- dos o más [APP RST M18] en rungs distintos.

GX Text Writer V3 hace una validación previa y bloquea la escritura si detecta SET o RST duplicados para el mismo dispositivo.

Recomendación de arquitectura:
- un único escritor por M/Y;
- preferir máquina de estados con MOV/comparaciones;
- usar SET/RST sólo cuando realmente haga falta enclavar un bit;
- nunca resolver varias condiciones escribiendo el mismo SET/RST desde rungs diferentes.

