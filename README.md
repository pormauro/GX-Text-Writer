# GX-Text-Writer + GXW-Tools + mView-Tools

Repositorio de herramientas para automatizar el flujo Mitsubishi/Coolmay desde una especificación validable hasta los artefactos nativos.

- **GX-Text-Writer/**: escritura asistida de Ladder en GX Works2/3.
- **GXW-Tools/**: lectura, auditoría, modificación y round-trip de proyectos GX Works2 `.gxw` (Ladder ordinario y Device Comments/tabla de nombres por dispositivo).
- **mView-Tools/**: generación, lectura, modificación y validación de archivos de HMI mView (`.tag`, `.sca` y `.vxf`).

## Objetivo

La IA trabaja sobre una representación declarativa legible; los compiladores determinísticos son responsables de la serialización binaria, tamaños, hashes, CRC y validación.

```text
documentación / requisitos
        ↓
        IA
        ↓
 ┌───────────────────────────┬───────────────────────────┐
 │ PLC spec / Ladder         │ HMI Project Spec         │
 │ + tabla de dispositivos   │ JSON validado            │
 └─────────────┬─────────────┴─────────────┬─────────────┘
               ↓                           ↓
      GX-Text-Writer / GXW-Tools     mView-Tools
               ↓                           ↓
         proyecto .gxw          .tag / .sca / .vxf
               ↓                           ↓
      validación / round-trip       validación binaria
               ↓                           ↓
             GX Works2                    mView
```

La IA **no debe escribir binarios a ciegas**. Debe producir una especificación verificable; las rutinas de este repo son las responsables de compilar, reconstruir y validar los artefactos finales.

## GXW

La baseline de la estampadora permitió cerrar offline el flujo:

```text
.gxw
 -> CFB/OLE exterior
 -> _hdb CFB anidado
 -> history.xml / recursos lógicos
 -> *.Program.pou / *.res
 -> Ladder interpretable
 -> edición
 -> reconstrucción de ambas capas
 -> validación de tamaño + MD5 + recursos no modificados
```

La tabla que el proyecto usa como nombres legibles de dispositivos (`B1`, `STATE`, `EV1_P1`, etc.) está en `COMMENT.qcd` como **Device Comments**. Los verdaderos Global/Local Labels (`Global1.gh`, `*.Labels.lh`) son otra estructura y están vacíos en esta baseline.

## VXF

Los proyectos completos de mView usan un contenedor `vxpm + zlib`. Las
mutaciones de escenas deben reconstruir también el bloque superior
`0x10000004` (size + CRC16/MODBUS). No hacerlo puede disparar el mensaje
engañoso de mView `HMI models are not supported, can't open!`.

La rutina segura está en `mView-Tools/vxf-editor/vxf_core.py`.

Ver:

- [`GXW-Tools/README.md`](GXW-Tools/README.md)
- [`GXW-Tools/FORMAT_LABELS.md`](GXW-Tools/FORMAT_LABELS.md)
- [`mView-Tools/README.md`](mView-Tools/README.md)
- [`mView-Tools/vxf-editor/README.md`](mView-Tools/vxf-editor/README.md)
- [`mView-Tools/vxf-editor/FORMAT_VXF.md`](mView-Tools/vxf-editor/FORMAT_VXF.md)
- [`mView-Tools/AI_ARCHITECTURE.md`](mView-Tools/AI_ARCHITECTURE.md)
