# Conectar TAQUIX con OpenAI (sin mostrar tu clave)

TAQUIX tiene su interfaz en `taquix.html` y el servidor preparado en `taquix-worker.js`.

1. Obtén una clave API desde https://platform.openai.com/api-keys. La API se factura por separado de ChatGPT; revisa la facturación y establece límites de gasto en https://platform.openai.com/settings/organization/limits.
2. Abre https://dash.cloudflare.com/, entra en **Workers & Pages**, crea un Worker llamado `taquix-api` y abre **Edit code**.
3. Copia todo el contenido de `taquix-worker.js` del repositorio y reemplaza el código del Worker. Pulsa **Deploy**.
4. En Cloudflare, abre el Worker > **Settings** > **Variables and Secrets** > **Add**. Elige **Secret**, escribe el nombre exacto `OPENAI_API_KEY`, pega tu clave API en el campo Value, y pulsa **Deploy**.
5. Copia únicamente la URL pública del Worker (algo como `https://taquix-api.TU-CUENTA.workers.dev`) y compártela en ChatGPT. Nunca envíes la clave API; solo la URL.
6. Se configurará la dirección `.../chat` en `taquix.html` para activar respuestas de IA real. Mientras tanto seguirá respondiendo con información verificada local.

**Antes de compartir el enlace al público:** configura protección contra abuso y límites de peticiones en Cloudflare, y un límite de gasto en OpenAI. El filtro de origen por sí solo NO evita solicitudes automatizadas.

**Privacidad:** el historial visible se guarda solamente en el navegador del usuario, y se puede borrar con el menú de TAQUIX. Cuando la IA esté activa, las preguntas y contexto reciente se enviarán al Worker y a OpenAI para generar respuestas. No solicites contraseñas ni datos de pago.
