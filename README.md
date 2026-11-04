# crm.anabasis.mx

CRM interno de Anabasis: seguimiento comercial de leads, prospectos y oportunidades (Prospecto → Oportunidad → Negociación → Cierre), bitácora de contactos e indicadores.

## Arquitectura
- Un solo archivo `index.html`: React 18, Babel Standalone, Tailwind y supabase-js, todos con versión fija (no quitar las versiones: una versión sin fijar ya rompió el CRM una vez).
- Datos y acceso: Supabase (PostgreSQL), tabla `records` con columna JSONB `data`. Inicio de sesión con correo y contraseña de Supabase Auth.
- La llave `anon` de Supabase está en el HTML; es pública por diseño. **La seguridad depende de que la tabla tenga RLS activado con políticas solo para usuarios autenticados.**

## Seguridad (revisar)
- Supabase › Table Editor › `records`: debe decir "RLS enabled" y tener políticas para el rol `authenticated`, ninguna para `anon`.
- Supabase › Authentication: desactivar registro público ("Allow new users to sign up") para que solo existan las cuentas que ustedes crean.
- La página lleva `noindex, nofollow` para no aparecer en buscadores.

## Publicación
- GitHub Pages: Settings › Pages › Deploy from a branch › `main` / `(root)`; Custom domain `crm.anabasis.mx`; Enforce HTTPS.
- DNS (Cloudflare, zona anabasis.mx): registro `CNAME` `crm` → `anabasismx.github.io`.
