# GX-Text-Writer + mView-Tools

Repositorio de herramientas para automatizar dos partes del flujo Mitsubishi/Coolmay:

- **GX-Text-Writer/**: escritura asistida de Ladder en GX Works2/3.
- **mView-Tools/**: generación, lectura y validación de archivos de HMI mView.

## Objetivo

La dirección del proyecto es que una IA pueda trabajar sobre una especificación declarativa y que compiladores determinísticos generen los artefactos finales:

```text
documentación / requisitos
        ↓
        IA
        ↓
HMI Project Spec (JSON validado)
        ↓
 ┌───────────────────┬────────────────────┐
 │ Tag compiler      │ Scene compiler     │
 │ .tag              │ .sca               │
 └───────────────────┴────────────────────┘
        ↓
 validación binaria / round-trip
        ↓
 importación en mView
```

La IA **no debe escribir binarios directamente**. Debe producir una especificación validable; las rutinas de este repo son las responsables de serialización, tamaños, CRC y compatibilidad.

Ver [mView-Tools/README.md](mView-Tools/README.md) y [mView-Tools/AI_ARCHITECTURE.md](mView-Tools/AI_ARCHITECTURE.md).
