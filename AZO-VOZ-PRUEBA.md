# AZO — voz natural juvenil (preparación, NO activada)

**Estado:** archivos preparados y guardados en GitHub. No se ha desplegado el nuevo Worker de Cloudflare ni se ha probado una sesión con la API. Ninguna generación de voz se ha cobrado desde estos cambios.

## Diseño aprobado

- Voz masculina juvenil, cercana a 20 años, cálida y conversacional.
- Español mexicano con un toque michoacano ligero; nada de caricaturas ni acentos sinaloenses/u oaxaqueños mezclados.
- Usar 'pues', 'híjole' y expresiones de Zacapu solo ocasionalmente.
- No pronunciar emojis ni URLs, y permitir interrupciones naturales cuando otra persona habla.
- Mostrar siempre a los usuarios que la voz es generada por IA.

## Archivos

- `taquix-worker.js`: prepara ruta POST `/voice-session` con credenciales efímeras mediante la Realtime API. Apagada por defecto.
- `azo-voz.html`: prueba de conversación con voz (WebRTC), botón explícito de inicio/fin, máximo 90 segundos por intento.
- `taquix.html`: mantiene el chat y la voz provisional del navegador. No requiere clave expuesta.

## Antes de activar (pendiente de permiso del dueño de la cuenta)

1. Solicitar autorización para usar la API de pago y configurar límites de presupuesto/facturación. Las sesiones Realtime consumen créditos.
2. Verificar acceso del proyecto de OpenAI a la API Realtime y una clave con los permisos necesarios. **Nunca publicar ni compartir la clave por chat, fotos o GitHub.**
3. Configurar protección contra bots, autenticación o acceso de prueba privado, y binding `TAQUIX_RATE_LIMITER` en Cloudflare. Un filtro CORS **no impide** que personas automaticen solicitudes; tampoco limita lo que dure una sesión después de emitido el token.
4. Reemplazar `worker.js` en el proyecto Cloudflare **azoapi** con el contenido completo de `taquix-worker.js`; desplegar manualmente.
5. Guardar `OPENAI_API_KEY` como *Secret* en Cloudflare, nunca como variable de texto público ni en el HTML.
6. Solo después de verificar seguridad y saldo, habilitar la variable `AZO_VOICE_ENABLED=yes` en Cloudflare.
7. Probar `azo-voz.html` en celular: inicio/fin, hablar y recibir respuestas, interrumpir al hablar, cierre a los 90 segundos, ausencia de cargos inesperados. Si la prueba falla, desactivar `AZO_VOICE_ENABLED`.
8. Revisar costos reales de las primeras pruebas y aprobar antes de enlazar voz natural en la página pública de AZO.

## Qué no está terminado

No hay despliegue probado en Cloudflare, autenticación de visitantes ni voz natural accesible al público. El chat de texto también mantiene pendiente su conexión al Worker mientras `API_ENDPOINT` siga vacío en `taquix.html`.

## Tecnología

- Modelo de voz preparado: `gpt-realtime-2.1-mini`, voz `cedar`. Es una propuesta para escuchar y ajustar; no garantiza que el acento michoacano sea perfecto.
- El navegador requiere HTTPS y permiso de micrófono.
- Documentación: https://developers.openai.com/api/docs/guides/voice-webrtc y https://developers.openai.com/api/reference/resources/realtime/subresources/client_secrets/methods/create
