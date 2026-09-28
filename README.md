# Pase de sala — Vercel + Firebase

Página estática (`index.html`) que usa Firebase para el login con Google y la base de datos.
Solo entran los usuarios que un administrador aprueba.

## Puesta en marcha

1. **Firebase**: en console.firebase.google.com creá un proyecto (sin Analytics).
2. **Authentication** → Comenzar → Método de acceso → **Google** → Habilitar.
3. **Firestore Database** → Crear base de datos → modo producción → región `southamerica-east1`.
   En la pestaña **Reglas**, pegá el contenido de `firestore.rules` y publicá.
4. **Configuración del proyecto** (engranaje) → Tus apps → Web `</>` → registrá la app y copiá el objeto
   `firebaseConfig`. Pegá `apiKey`, `authDomain`, `projectId` y `appId` en la constante `cfg` de `index.html`.
   (Esas claves son públicas por diseño: la seguridad la dan las reglas de Firestore.)
5. **Vercel**: subí esta carpeta a un repositorio de GitHub (con `index.html` en la raíz), en vercel.com
   → Add New → Project → importá el repositorio → Deploy. No hace falta configurar build.
6. En Firebase → Authentication → Configuración → **Dominios autorizados** → agregá el dominio de Vercel
   (por ejemplo `mi-app.vercel.app`) y tu dominio propio si lo tenés.
7. **Primer administrador**: abrí la app e ingresá con tu Gmail (quedás "pendiente"). En Firebase → Firestore →
   colección `usuarios` → tu documento → cambiá `estado` a `aprobado` y `rol` a `admin`. Recargá la app.

## Uso

- Quien ingrese por primera vez ve "Solicitud enviada".
- El administrador entra a **Usuarios** y toca **Dar acceso**, **Rechazar** o **Quitar acceso**.
  También puede hacer administrador a otra persona.
- Pacientes: la lista muestra solo los internados; el buscador incluye las altas.
