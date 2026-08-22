# Tiro App — Fase 2: Responsive iOS + Android

Base: Fase 1 validada en producción.

## Objetivo
Adaptar la presentación para iPhone, Android, tablets y escritorio manteniendo una única aplicación web.

## Regla
No se modificó la funcionalidad:
- no se modificó JavaScript;
- no se modificó OpenCV;
- no se modificó Supabase;
- no se modificó IndexedDB;
- no se modificaron IDs ni event listeners.

Los cambios de esta fase son de CSS/layout y comportamiento visual responsive.

## Incluye
- Safe areas para iPhone/notch/Dynamic Island.
- `100dvh` para viewport móvil moderno.
- Controles táctiles de tamaño cómodo.
- Adaptación para teléfonos pequeños.
- Adaptación para landscape.
- Canvas preparado para conservar resolución real y desplazarse cuando corresponda.
- Mejor comportamiento en tablets y desktop.
- Preferencia de reducción de movimiento.

## Próximo paso
Validar en iPhone y Android. Si esta fase queda aprobada, continuar con el reemplazo sistemático de emojis por los SVG propios de `assets/icons/`.
