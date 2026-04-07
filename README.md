# NocheERP

Sistema de gestión integral para boliches y eventos nocturnos.
**Stack**: HTML + CSS + JS vanilla · Supabase · GitHub Pages

---

## Deploy en GitHub Pages — paso a paso

### 1. Clonar / descomprimir y configurar

Descomprimí el ZIP y entrá a la carpeta:
```bash
cd nochoerp
```

Creá el archivo `config.js` con tus credenciales de Supabase:
```js
// config.js  ← este archivo NO se sube al repo
window.__SUPABASE_URL__      = 'https://TU_PROYECTO.supabase.co'
window.__SUPABASE_ANON_KEY__ = 'eyJhbGciOi...'
```

> Las credenciales las encontrás en:
> Supabase Dashboard → Project Settings → API → Project URL y anon key

---

### 2. Subir a GitHub

```bash
git init
git add .
git commit -m "NocheERP v1.0"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/nochoerp.git
git push -u origin main
```

> `config.js` está en `.gitignore` — no se sube automáticamente.

---

### 3. Activar GitHub Pages

1. Ir al repo en github.com
2. **Settings** → **Pages** (menú izquierdo)
3. Source: `Deploy from a branch`
4. Branch: `main` / `/ (root)`
5. **Save**

En ~2 minutos la app queda disponible en:
```
https://TU_USUARIO.github.io/nochoerp/
```

---

### 4. Configurar Supabase

En el SQL Editor de tu proyecto Supabase, ejecutar en orden:
1. `nochoerp_supabase_schema.sql` — schema completo
2. El trigger de auth (ver `nochoerp_auth_roles.html`)

Habilitar Realtime en:
- Table Editor → `eventos` → Enable Realtime
- Repetir para: `rendiciones`, `alertas`, `caja_movimientos`

---

### 5. Crear primer usuario admin

En Supabase → Authentication → Users → **Invite user** (con tu email).

Una vez que te registrás, ejecutar en SQL Editor:
```sql
UPDATE perfiles SET rol = 'admin' WHERE email = 'tu@email.com';
```

---

### 6. Actualizar la app en el futuro

Cada vez que hagas cambios:
```bash
git add .
git commit -m "descripción del cambio"
git push
```
GitHub Pages se actualiza automáticamente en ~1 minuto.

---

## Estructura del proyecto

```
nochoerp/
├── .gitignore          # Excluye config.js del repo
├── _config.yml         # Deshabilita Jekyll en GitHub Pages
├── config.js           # ← CREAR LOCALMENTE, no commitear
├── README.md
├── index.html          # Dashboard principal
├── login.html          # Pantalla de login
├── css/
│   └── app.css         # Estilos globales
├── js/
│   └── app.js          # Auth, sidebar, helpers
└── pages/
    ├── rendicion.html  # Módulo completo con Supabase
    ├── eventos.html
    ├── egresos.html
    ├── liquidacion.html
    ├── cashflow.html
    ├── cajas.html
    ├── cheques.html
    ├── reportes.html
    └── admin.html
```

---

## URLs de la app

| Página | URL |
|--------|-----|
| Login | `github.io/nochoerp/login.html` |
| Dashboard | `github.io/nochoerp/` |
| Rendición | `github.io/nochoerp/pages/rendicion.html` |
| Eventos | `github.io/nochoerp/pages/eventos.html` |
| Liquidación | `github.io/nochoerp/pages/liquidacion.html` |

---

## Dominio personalizado (opcional)

Si tenés un dominio propio (ej: `erp.misound.com.ar`):

1. En GitHub → Settings → Pages → Custom domain → ingresar el dominio
2. En tu DNS (Cloudflare):
   - Agregar un registro `CNAME` apuntando a `TU_USUARIO.github.io`
3. GitHub configura HTTPS automáticamente

---

## Checklist antes de usar en producción

```
[ ] config.js creado con tus keys reales de Supabase
[ ] Schema SQL ejecutado sin errores
[ ] Trigger de auth creado
[ ] Usuario admin creado y con rol = 'admin' en SQL
[ ] Realtime habilitado en las 4 tablas
[ ] GitHub Pages activado y accesible
[ ] Login funciona
[ ] Crear primer evento y puntos de venta
[ ] Probar rendición completa
```
