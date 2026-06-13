# DT 2026 — Director Técnico

Juego retro de manager de selecciones (homenaje al Championship Manager 93/94).
48 selecciones, planteles reales 2026, partidos en vivo minuto a minuto,
alargue y penales, puntuaciones 1-10, tres idiomas (ES/EN/PT) y modo claro/oscuro.

## Publicar en Vercel (gratis, ~10 minutos)

1. Crear cuenta gratuita en https://vercel.com (con email o GitHub).
2. Opción simple (sin GitHub): instalar Node.js (https://nodejs.org), abrir una
   terminal en esta carpeta y correr:
   ```
   npm install
   npx vercel
   ```
   Seguir las preguntas (Enter a todo). Te devuelve la URL pública.
3. Opción con GitHub: subir esta carpeta a un repositorio y en Vercel elegir
   "Import Project". Detecta Vite solo. Deploy y listo.

## Configurar tu link de donación

Abrí `src/DT2026.jsx` y al principio buscá:
```
const DONATE_URL="https://cafecito.app/TU-USUARIO";
```
Reemplazalo por tu link real de https://cafecito.app o https://buymeacoffee.com
(crear cuenta lleva 5 minutos). El botón aparece en la pantalla de título y
cuando alguien sale campeón.

## Probar localmente

```
npm install
npm run dev
```

## Nota legal

Proyecto gratuito de fans, sin publicidad, sin logos ni marcas oficiales.
Los nombres de jugadores se usan con fines informativos/estadísticos.
Si en el futuro quisieras monetizar con publicidad, conviene revisar el uso
de nombres reales (licencias FIFPro) — hablalo antes de activar ads.
