# mView-Tools

Toolchain experimental para generar archivos de HMI **mView** de Coolmay.

## Módulos

- `tag-generator/` — genera y valida archivos `.tag`.
- `scene-generator/` — lee, reconstruye y genera archivos de escenas `.sca`.
- `specs/` — formato declarativo pensado como interfaz estable para IA.

## Principio de diseño

La capa inteligente decide **qué HMI construir**. La capa binaria decide **cómo serializarla correctamente**.

No mezclar ambas responsabilidades:

1. IA/documentación → especificación HMI.
2. Validación de esquema.
3. Compilador TAG → `.tag`.
4. Compilador de escenas → `.sca`.
5. Validación estructural y round-trip.
6. Importación y verificación en mView.

Los formatos `.tag` y `.sca` fueron reconstruidos a partir de archivos reales exportados por mView. La documentación de cada formato vive junto a su compilador.
