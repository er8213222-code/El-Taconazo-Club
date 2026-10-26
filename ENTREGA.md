# El Taconazo Club — pasos imprescindibles antes de entregar

La web está visible en GitHub Pages, pero **tenerla publicada no equivale a tenerla lista para atender clientes**.

## 1. Protección de puntos en Firebase (obligatorio)
- Abrir Firebase Console → proyecto `el-taconazo-club` → Firestore Database → Reglas.
- Revisar la configuración actual. Preparé un archivo `firestore.rules` en este repositorio con una propuesta de reglas restringidas que coincide con los datos creados por `index.html`.
- **Antes de publicar las reglas**, probarlas en el simulador de Firebase o en un entorno de pruebas: un cliente debe poder leer solo su propia ficha y crearla con cero puntos; no debe poder sumar, canjear ni consultar otros clientes; la cuenta autorizada debe poder registrar compras y canjes.
- Las reglas de GitHub **no se aplican solas a Firebase**. Se deben revisar y publicar en la consola. No permitir `allow read, write: if true` ni `if request.auth != null` para toda la colección de clientes.

## 2. Acceso del negocio (obligatorio)
- Hoy el panel solo reconoce un UID fijo en `index.html`: `ADMIN_UID`. Las reglas propuestas contienen el mismo UID para respetar el acceso actual.
- Antes de la entrega, crear una **cuenta independiente del negocio** en Firebase Authentication. Que la contraseña quede en manos del dueño, no del desarrollador.
- Sustituir el UID anterior por el UID **de la cuenta del negocio** en `index.html` y en `firestore.rules`. Volver a publicar las reglas.
- Los empleados usarán esa cuenta compartida solo de manera provisional. No habrá trazabilidad por empleado hasta añadir cuentas individuales. Proteger esa contraseña y cambiarla cuando alguien deje el negocio.

## 3. Revisión final indispensable (una sola ronda)
- Crear cliente con un correo real, abrir su tarjeta y QR.
- Como encargado, registrar compra y comprobar la actualización desde la tarjeta del cliente.
- Canjear premio y confirmar que bajan los puntos disponibles pero no los acumulados.
- Intentar acceder a los datos de otra persona como cliente (debe ser rechazado).
- Retirar o identificar de forma segura las cuentas de prueba, con cuidado de no borrar fichas reales ni perjudicar puntos existentes.

## Opcionales después del lanzamiento
- Sonido específico al recibir puntos, avisos de WhatsApp con consentimiento y accesos individuales de empleados.

Enlace de la página: https://er8213222-code.github.io/El-Taconazo-Club/
