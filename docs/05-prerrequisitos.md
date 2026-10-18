# Etapa D: prerrequisitos

Lista exacta de lo que debe estar listo **antes de la Fase 0**, y de lo que se necesita más adelante (marcado con la fase).
Versiones revisadas el 18 de octubre de 2026.

## 1. Cómo vamos a trabajar
- **El código lo escribo y lo ejecuto yo** en este entorno en la nube. Tú **no necesitas instalar herramientas de programación** ni usar la terminal.
- **Tu parte:**
  - crear las cuentas, desde el navegador de tu tablet o computador;
  - guardar las claves en la configuración del entorno (sección 4);
  - instalar la app de prueba en tus teléfonos;
  - probar con las listas de aceptación.
- **Equipos para probar:**

| Equipo | Para qué | ¿Cuándo? |
|---|---|---|
| 1 teléfono Android | App de conductor y de receptor | Desde la Fase 0 |
| 1 segundo teléfono (Android o iPhone) | Probar dos perfiles a la vez | Desde la Fase 3 |
| Tablet o computador con navegador | Panel del administrador | Desde la Fase 1 |
| iPhone | Probar la versión iOS | Cuando tengas la cuenta de Apple (recomendado antes de la Fase 4) |

En Android la app de prueba se instala con un enlace. En iPhone, Apple exige la cuenta de desarrollador ($99 al año) incluso para probar.

---

## 2. Cuentas

### Ahora (antes de la Fase 0)
| # | Cuenta | Plan | Qué crear | Qué guardar (sección 4) |
|---|---|---|---|---|
| 1 | **GitHub** | Ya la tienes | Nada | — |
| 2 | **Supabase** (supabase.com) | **Free** para desarrollo; Pro ($25) recién con usuarios reales | Una organización y un proyecto llamado `reparto-dev`, región **South America (São Paulo)**. Anota la contraseña de la base de datos en un lugar seguro, como un gestor de contraseñas. | `SUPABASE_ACCESS_TOKEN` (Account → Access Tokens), `SUPABASE_PROJECT_REF` (el código del proyecto en la URL), `SUPABASE_DB_PASSWORD` |
| 3 | **Expo** (expo.dev) | Free | Cuenta y un token de acceso (Account settings → Access tokens) | `EXPO_TOKEN` |
| 4 | **Sentry** (sentry.io) | Developer (gratis) | Organización y dos proyectos: `reparto-movil` (React Native) y `reparto-web` (Next.js) | `SENTRY_AUTH_TOKEN` |
| 5 | **Cloudflare** (cloudflare.com) | Free | Cuenta y un token de API con permiso "Workers" y "R2" | `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID` |

**Correos de prueba sin dominio:** mientras no haya nombre ni dominio, Supabase envía los códigos de inicio de sesión solo a los **miembros de tu organización** en Supabase. Para que funcionen tus cuentas de prueba (por ejemplo, un correo para el conductor y otro para el receptor), invítalos como miembros en *Organization → Team*. Así es gratis y no hay que pegar correos en el chat.

### Más adelante
| Cuenta | Fase | Plan | Qué guardar |
|---|---|---|---|
| **Proveedor de VPS** (Hetzner o DigitalOcean, se decide en la Fase 2) | 2 | ~$15–30 al mes | `VPS_API_TOKEN` |
| **Google Cloud**: solo la API Geocoding, con la clave restringida a esa API | 2 (opcional) | Pago por uso, ~10.000 consultas gratis al mes | `GOOGLE_GEOCODING_KEY` |
| **Apple Developer** | Antes de probar en iPhone | $99 al año | Lo configuramos juntos con EAS (no se pega nada) |
| **Anthropic Console** (console.anthropic.com), con límite de gasto mensual | 7 | Pago por uso | `ANTHROPIC_API_KEY` |
| **Stream** (getstream.io) | 9 | Pago por uso, con cupo gratis | `STREAM_API_KEY`, `STREAM_API_SECRET` |
| **Resend** | Cuando haya dominio | Free y después Pro ($20) | `RESEND_API_KEY` |
| **Dominio .cl** (nic.cl) | Cuando haya nombre | ~$12 al año | — |
| **Google Play Console** | Etapa F | $25, pago único | — |
| **Licencia Transistorsoft Starter** | Etapa F | $399, pago único | `TRANSISTORSOFT_LICENSE` |

---

## 3. Herramientas (las instalo yo en el entorno)
| Herramienta | Versión | Comando para verificar |
|---|---|---|
| Node.js | 24 LTS (24.22.0). Hoy el entorno tiene 22.22, que Expo también acepta. | `node -v` |
| pnpm, el gestor de paquetes del monorepo | 12.14 | `pnpm -v` |
| Supabase CLI | 2.121 | `npx supabase --version` y `npx supabase projects list` (comprueba el inicio de sesión) |
| EAS CLI (Expo) | 25.2 | `npx eas-cli --version` y `npx eas-cli whoami` (comprueba el inicio de sesión) |
| Docker, para correr Supabase local en las pruebas | 29.8 (ya instalado) | `docker --version` |
| Expo SDK | 58.0.14 (necesita Node 22.13 o superior) | `npx expo --version` |
| Next.js | 16.4.2 | `npx next --version` |
| Git | 2.43 (ya instalado) | `git --version` |

Ninguna CLI pide contraseña: inician sesión solas leyendo `SUPABASE_ACCESS_TOKEN` y `EXPO_TOKEN`.

---

## 4. Dónde van las claves (y por qué nunca en el chat)
1. Abre el menú del **entorno en la nube**, en la barra de título de esta sesión, y toca **Edit**.
2. En **Network secrets** (o **API credentials** / variables de entorno, según la versión de la app), agrega cada clave con **el nombre exacto** de la tabla de la sección 2.
3. Guarda. **Una sesión nueva toma las claves.** Todo el contexto del proyecto está en el repositorio, así que en la sesión nueva basta con decir "seguimos con la Fase 0".

En el código, las claves se leen de un archivo `.env` que está en `.gitignore`, así que nunca se sube a GitHub. La revisión automática bloquea cualquier clave que se cuele.

## 5. Acceso a internet del entorno
Hoy el entorno solo llega a npm, GitHub y Anthropic. En la misma pantalla (**Network access**), deja el nivel **Limited**, mantén marcado **Allow package managers** y agrega en **Allowed domains**:

```
supabase.com
api.supabase.com
supabase.co
expo.dev
api.expo.dev
u.expo.dev
sentry.io
ingest.sentry.io
cloudflare.com
api.cloudflare.com
r2.cloudflarestorage.com
download.geofabrik.de
build.protomaps.com
```
Si la pantalla acepta comodines, agrega también `*.supabase.co`, `*.expo.dev` y `*.ingest.sentry.io`, porque cada proyecto usa su propio subdominio.

Más adelante se agregan `getstream.io`, `stream-io-api.com`, `api.resend.com` y el proveedor de VPS.

Guía oficial: https://code.claude.com/docs/en/cloud-environments#network-access

---

## 6. Qué datos puedes pegar en el chat y cuáles nunca
| ✅ Sí puedes pegar | ❌ Nunca pegues |
|---|---|
| Nombres de proyectos y organizaciones | Tokens, claves de API, contraseñas, *service_role key* |
| Mensajes de error completos (revisa que no incluyan claves) | Datos reales de conductores o receptores: nombres, teléfonos, correos, direcciones, licencias |
| Capturas de pantalla de la app de prueba con datos ficticios | Capturas que muestren claves o datos reales |
| Tu llave SSH **pública** (`.pub`), si alguna vez se necesita | La llave SSH privada |

Para probar usaremos los datos ficticios del caso de Matías.

---

## 7. Lista para confirmar
Cuando todo esté hecho, respóndeme "listo" (en una sesión nueva si agregaste claves):
- [ ] Proyecto `reparto-dev` creado en Supabase, región São Paulo
- [ ] Correos de prueba invitados como miembros de la organización de Supabase
- [ ] Cuentas de Expo, Sentry y Cloudflare creadas
- [ ] Claves guardadas en el entorno con estos nombres: `SUPABASE_ACCESS_TOKEN`, `SUPABASE_PROJECT_REF`, `SUPABASE_DB_PASSWORD`, `EXPO_TOKEN`, `SENTRY_AUTH_TOKEN`, `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`
- [ ] Dominios permitidos agregados (sección 5)
- [ ] Teléfono Android a mano

Con eso verifico todo con los comandos de la sección 3 y empiezo la **Fase 0**.
