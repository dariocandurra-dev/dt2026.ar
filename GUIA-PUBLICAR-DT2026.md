# Guía para publicar DT 2026 — paso a paso

Hacé los pasos EN ORDEN. Cada bloque es independiente; terminá uno antes de
empezar el siguiente. No necesitás saber programar para ninguno.

---

## PASO 1 — Cafecito (2 minutos) ✅ el código ya está listo

El botón del juego YA apunta a `cafecito.app/dt2026`. Solo falta que esa
página exista:

1. Entrá a https://cafecito.app y registrate.
2. Cuando te pida tu nombre de usuario, escribí exactamente:  dt2026
3. Vinculá tu cuenta de Mercado Pago cuando te lo pida (botón "Conectar con
   Mercado Pago" → autorizar). Las donaciones caen ahí, y de Mercado Pago
   pasás la plata a tu banco con tu CBU/alias.

Listo. No tenés que tocar el código: ya quedó configurado.

---

## PASO 2 — Subir el código a GitHub (método arrastrar, SIN consola)

Tu repo: https://github.com/dariocandurra-dev/dt2026.ar

1. Descomprimí el archivo  dt2026-github.zip  en una carpeta de tu compu.
   Vas a ver: index.html, package.json, vite.config.js, README.md,
   .gitignore, y las carpetas  src  y  public.
2. Entrá a tu repo en el navegador (logueado a GitHub).
3. Buscá el link gris que dice "uploading an existing file"
   (o el botón "Add file" arriba a la derecha → "Upload files").
   IGNORÁ cualquier bloque de comandos negros que muestre la página.
4. Arrastrá TODOS los archivos y carpetas descomprimidos a la zona
   "Drag files here". Esperá la barra verde.
5. Abajo, en "Commit changes", escribí "primera version" y clic en el
   botón verde "Commit changes".

Si el arrastre de carpetas falla, subí primero los archivos sueltos
(index.html, package.json, etc.) y después repetí el paso entrando a
la carpeta src y subiendo sus 2 archivos ahí dentro.

POR QUÉ ASÍ: git por consola pide un "token" de autenticación que traba a
todo el mundo. El arrastre web no pide nada de eso.

---

## PASO 3 — Deploy en Vercel (5 minutos)

1. Entrá a https://vercel.com y registrate con "Continue with GitHub"
   (así quedan conectados solos).
2. Dashboard → "Add New..." → "Project".
3. Buscá el repo  dt2026.ar  en la lista → "Import".
4. NO toques ninguna configuración (Vercel detecta Vite solo) → "Deploy".
5. En ~1 minuto te da una URL tipo  dt2026-ar.vercel.app
   ESA URL YA FUNCIONA y ya la podés compartir en tus grupos.

Si más adelante cambiás algo del juego: volvés a subir el archivo nuevo a
GitHub (Paso 2) y Vercel redeploya solo. No hay que repetir el Paso 3.

---

## PASO 4 — Conectar tu dominio dt2026.ar (lo más enredado, por culpa de .ar)

IMPORTANTE: NIC.ar NO permite apuntar directo a Vercel (NIC solo maneja
"nameservers", y Vercel ya no soporta nameservers para .ar). La solución
estándar en Argentina es poner CLOUDFLARE gratis en el medio. Es gratis.

### 4.A — Crear cuenta en Cloudflare y agregar el dominio
1. Entrá a https://cloudflare.com → Sign Up (gratis).
2. "Add a site" → escribí:  dt2026.ar  → elegí el plan FREE.
3. Cloudflare intentará escanear los DNS y FALLARÁ (es normal en .ar).
   Buscá el link "Add DNS records manually" / "Continuar".

### 4.B — Cargar los registros que pide Vercel, dentro de Cloudflare
1. En Vercel: tu proyecto → Settings → Domains → Add → escribí  dt2026.ar
   → Add. Vercel te mostrará los registros que necesita. Anotá:
   - Un registro tipo  A  con nombre  @  apuntando a una IP
     (suele ser 76.76.21.21 — USÁ LA QUE TE MUESTRE VERCEL).
   - (Opcional) un  CNAME  para  www.
2. En Cloudflare → pestaña DNS → "Add record":
   - Type: A   |  Name: @   |  IPv4 address: (la IP que dio Vercel)
     |  Proxy status: poné "DNS only" (nube GRIS, no naranja).  Save.
   - (Opcional) Type: CNAME | Name: www | Target: cname.vercel-dns.com
     | Proxy: DNS only (nube gris). Save.

### 4.C — Copiar los nameservers de Cloudflare a NIC.ar
1. En Cloudflare, en la pantalla de configuración te da DOS nameservers,
   tipo:   xxx.ns.cloudflare.com   y   yyy.ns.cloudflare.com
   Copialos (anotá los dos exactos que te toquen a vos).
2. Entrá a https://nic.ar (ingreso con CUIT/CUIL y Clave Fiscal AFIP).
3. Lista de dominios → al lado de  dt2026.ar  → botón "Delegar".
4. "Agregar una nueva delegación"  (NO "Autodelegar" — esa es otra cosa).
5. Pegá el PRIMER nameserver de Cloudflare → Guardar (ícono disquete).
6. Repetí con el SEGUNDO nameserver → Guardar.
7. Clic en "Ejecutar cambios".

### 4.D — Esperar
La delegación puede tardar de unos minutos hasta 24-48 hs en propagarse.
Cuando esté lista:
- Cloudflare te manda un mail "your site is active".
- En Vercel, el dominio dt2026.ar pasa de "Invalid Configuration" a
  "Valid Configuration" (✓ verde).
- Abrí  https://dt2026.ar  en el navegador → debería cargar el juego.

Mientras tanto, podés compartir la URL  dt2026-ar.vercel.app  sin problema.

---

## Resumen del orden
1. Cafecito (usuario: dt2026)         → ya está en el código
2. GitHub (arrastrar el zip)          → 5 min
3. Vercel (import + deploy)           → 5 min, URL funcionando
4. Dominio (Cloudflare + NIC.ar)      → 15 min + espera de propagación

Si te trabás en algún paso puntual, anotá EN CUÁL y qué cartel ves en
pantalla — con eso es mucho más fácil destrabarlo.
