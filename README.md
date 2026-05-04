# Plan de Ahorro — Tracker compartido

App web para registrar depósitos de fin de semana y compartirlos en tiempo real con tu pareja.  
Se aloja **gratis** en GitHub Pages y usa **Firebase Firestore** para sincronizar los datos.

---

## Requisitos

- Cuenta en [GitHub](https://github.com) (gratis)
- Cuenta en [Firebase](https://firebase.google.com) (gratis, plan Spark)
- Un navegador — no necesitas instalar nada más

---

## Paso 1 — Crear el proyecto Firebase

1. Ve a [console.firebase.google.com](https://console.firebase.google.com)
2. Haz clic en **"Agregar proyecto"**
3. Ponle un nombre (ej. `plan-ahorro-familia`)
4. Desactiva Google Analytics (opcional) y haz clic en **"Crear proyecto"**

---

## Paso 2 — Activar Firestore

1. En el menú izquierdo ve a **Build → Firestore Database**
2. Haz clic en **"Crear base de datos"**
3. Selecciona **"Comenzar en modo de prueba"** (permite lectura y escritura por 30 días)
4. Elige la región más cercana (ej. `us-central1`) y haz clic en **"Listo"**

> ⚠️ Después de los 30 días de prueba, ve a la pestaña **Reglas** y pega esto para que siga funcionando:
> ```
> rules_version = '2';
> service cloud.firestore {
>   match /databases/{database}/documents {
>     match /{document=**} {
>       allow read, write: if true;
>     }
>   }
> }
> ```

---

## Paso 3 — Obtener las credenciales

1. En Firebase Console, haz clic en el ícono ⚙️ → **"Configuración del proyecto"**
2. Baja a la sección **"Tus apps"** y haz clic en el ícono `</>` (Web)
3. Registra la app con cualquier nombre (ej. `tracker-web`)
4. Copia el objeto `firebaseConfig` que aparece — se ve así:

```js
const firebaseConfig = {
  apiKey:            "AIzaSy...",
  authDomain:        "tu-proyecto.firebaseapp.com",
  projectId:         "tu-proyecto",
  storageBucket:     "tu-proyecto.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc..."
};
```

---

## Paso 4 — Editar index.html

Abre `index.html` y busca este bloque (está marcado con comentarios):

```js
/* ══════════════════════════════════════════════════════
   🔧 REEMPLAZA ESTE BLOQUE CON TUS CREDENCIALES FIREBASE
   ══════════════════════════════════════════════════════ */
const firebaseConfig = {
  apiKey:            "TU_API_KEY",
  ...
};
```

Reemplázalo con tus credenciales reales del Paso 3.

---

## Paso 5 — Publicar en GitHub Pages

1. Ve a [github.com](https://github.com) y crea un repositorio nuevo
   - Nombre: `plan-ahorro` (o el que quieras)
   - Visibilidad: **Public** (necesario para GitHub Pages gratis)
   - No agregues README ni .gitignore

2. Sube los archivos. Puedes hacerlo directamente desde el navegador:
   - En tu repositorio recién creado haz clic en **"uploading an existing file"**
   - Arrastra `index.html` y `README.md`
   - Haz clic en **"Commit changes"**

3. Activa GitHub Pages:
   - Ve a **Settings → Pages**
   - En "Source" selecciona **"Deploy from a branch"**
   - Branch: `main` | Folder: `/ (root)`
   - Haz clic en **Save**

4. Espera 1-2 minutos y tu app estará en:
   ```
   https://TU-USUARIO.github.io/plan-ahorro/
   ```

---

## Paso 6 — Compartir con tu pareja

1. Comparte la URL de GitHub Pages con tu pareja
2. Al entrar, **usen exactamente el mismo "Código del plan"** (ej. `familia-garcia-2025`)
3. Cada quien pone su nombre
4. Los depósitos se sincronizan automáticamente en tiempo real ✓

---

## Cómo usar la app

| Acción | Cómo |
|--------|------|
| Establecer meta mensual | Escribe la cantidad en el campo "Meta mensual" |
| Registrar un depósito | Toca cualquier sábado o domingo |
| Editar un depósito | Toca el día que ya tiene depósito |
| Borrar un depósito | Toca el día → botón "Borrar" |
| Cambiar de mes | Flechas ← → en la esquina superior |

---

## ¿Qué significan los colores?

- 🟢 **Verde** — Depósito registrado ese día
- 🔴 **Rojo** — Fin de semana sin depósito (pasado)
- ⬜ **Gris** — Día de semana (no aplica)
- 🔵 **Borde azul** — Hoy

---

## Estructura del proyecto

```
plan-ahorro/
├── index.html    ← toda la app (HTML + CSS + JS)
└── README.md     ← este archivo
```

---

## Privacidad y seguridad

- Los datos se guardan en tu propio proyecto Firebase (no en servidores de terceros)
- Solo quien tenga el "Código del plan" puede ver y editar los datos
- Para más seguridad puedes agregar autenticación Firebase en el futuro

---

## ¿Algo no funciona?

- **Pantalla en blanco / error de Firebase** → Verifica que pegaste bien el `firebaseConfig`
- **No se sincronizan los datos** → Asegúrate de usar el mismo "Código del plan" en ambos dispositivos
- **La URL no carga** → Espera 2-3 minutos después de activar GitHub Pages

