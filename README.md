# Contador de Impactos — prototipo v0

## Probarlo YA, sin instalar nada
Abrí `index.html` con doble clic en cualquier compu (Chrome/Edge/Safari).
Podés subir una de tus fotos del blanco y ver la detección funcionando.

## Probarlo en tu iPhone (esta semana, sin Mac)
El botón "Sacar foto" (`capture="environment"`) necesita que el sitio esté
servido por http/https — no funciona bien abriendo el archivo suelto desde
el iPhone. Opción más simple:

1. Instalá Node.js (link que te pasé).
2. Abrí una terminal en esta carpeta y corré:
   ```
   npx serve .
   ```
3. Te va a dar una URL tipo `http://192.168.x.x:3000` — abrila desde el
   Safari del iPhone (mismo Wi-Fi que la compu).
4. Listo, ya podés sacar la foto y ver la detección en el celular.

## Subirlo a internet (para no depender de tu compu prendida)
1. Creá cuenta en GitHub y en Vercel (podés loguearte en Vercel con GitHub).
2. Subís esta carpeta a un repositorio nuevo en GitHub.
3. En Vercel: "Add New Project" → elegís el repo → Deploy.
4. Te da una URL pública (tipo `tiro-app.vercel.app`) — abrila en el iPhone
   y desde ahí "Agregar a pantalla de inicio" para que se sienta como app.

## Qué hace este prototipo
- **Datos de sesión**: tirador (nombre), diana (banco de referencias) y
  distancia (10/15/20/25/30m) — se completan antes de sacar la foto.
- Elegir una diana del banco ajusta automáticamente el modo de detección
  y los sliders a valores ya calibrados (los mismos que validamos hoy
  con fotos reales) — se pueden seguir ajustando a mano después.
- Sacar/subir foto → detecta impactos → círculos tocables para corregir.
- **Guardado por ronda** (tirador + diana + distancia + fecha +
  coordenadas) en IndexedDB — queda en el teléfono, no sale a internet.
- **Comparación automática contra la ronda anterior**: busca la última
  ronda guardada con el *mismo tirador + misma diana + misma distancia*
  y compara por coordenadas — verde los impactos nuevos, gris los que
  ya estaban. Si cambiás cualquiera de esos tres datos, compara contra
  otra ronda (o ninguna, si es la primera vez con esa combinación).

## Banco de dianas (por ahora, 5 presets fijos en el código)
- ISSF 25m (con anillos + círculo negro) → modo Hough
- **ProTarget (con puntaje por anillos)** → modo Hough + cálculo de
  puntaje. Los anillos de este blanco están exactamente cada 10% del
  radio exterior (9,8,7...1 en pasos de 10%) — la fórmula de puntaje es
  `9 − floor(10 × distancia_al_centro / radio_exterior)`. Se calibra
  tocando el centro y el borde del anillo 1 en la foto (dos toques).
- Papel blanco liso → modo umbral
- Papel blanco con líneas finas → modo umbral, más estricto
- Personalizada → no toca los sliders, ajustás vos

## Limitación importante (por ahora)
La comparación entre rondas asume que las fotos se sacaron **desde la
misma posición/encuadre** — no hay todavía un paso de recorte a 4
esquinas que corrija diferencias de ángulo entre fotos. Con el
monóculo + trípode que estás por comprar, esto debería cumplirse
naturalmente. Si el encuadre cambia mucho entre rondas, la comparación
va a fallar (marcará como "nuevos" impactos viejos que se corrieron de
posición en el encuadre).

## Lo que falta (próximos pasos, en orden)
1. Selección manual de las 4 esquinas del papel (recorte/rectificación) —
   esto además arregla la limitación de la comparación entre rondas.
2. Métricas de grupo: centro y dispersión por ronda (¿mejoró o no?).
3. Guardar también la foto (no solo las coordenadas) para poder revisar
   rondas pasadas visualmente.
4. Exportar el historial (CSV o similar) para llevar registro fuera de
   la app.
5. Banco de dianas editable desde la interfaz (hoy son 4 presets fijos
   en el código) — por ejemplo, poder subir una foto de referencia de
   una diana nueva y guardarla con sus propios valores calibrados.
