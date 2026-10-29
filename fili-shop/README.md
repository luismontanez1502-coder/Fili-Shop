# FILI SHOP — tienda digital independiente

Tienda React + Vite con backend Express, Stripe Checkout y notificaciones por Resend. No requiere ChatGPT para funcionar.

## Instalación
1. Instala Node.js 20 o superior.
2. Ejecuta `npm install`.
3. Copia `.env.example` a `.env` y completa tus claves. **Nunca compartas las claves privadas.**
4. Desarrollo visual: `npm run dev` (http://localhost:5173). El carrito se muestra, pero el pago necesita el backend.
5. Producción: `npm run build` y `npm run server`. El backend sirve el sitio compilado desde `dist` y escucha en el puerto 3001.
6. Publica en un hosting Node.js con HTTPS, dominio propio y variables de entorno configuradas.
7. En Stripe, configura un webhook a `https://tu-dominio.com/api/webhook` para `checkout.session.completed` y `checkout.session.async_payment_succeeded`; copia su secreto a `STRIPE_WEBHOOK_SECRET`.
8. Verifica tu dominio en Resend y usa una dirección `FROM_EMAIL` de ese dominio. Los emails se envían tras la confirmación de pago mediante webhook.
9. Haz una compra de prueba con Stripe en modo test y confirma recepción de ambos correos antes de activar pagos reales.

## Importante antes de vender
- Los seis productos y precios son **ejemplos**, no productos reales cargados. Cámbialos en `src/main.jsx` y `server/index.js` (el backend es la fuente de precios).
- **La entrega de archivos es manual**: el cliente recibe confirmación por email, no un enlace de descarga. Para entrega automática, agrega almacenamiento privado, permisos de descarga y enlaces temporales.
- El panel de administración todavía no está implementado. Se modifican los productos en código.
- Los pedidos se registran localmente en `server/private/orders.jsonl`. En hosting efímero o múltiples instancias se necesita una base de datos persistente para evitar pérdida/duplicados. El marcador local de pedidos enviados tampoco es transaccional: para producción, utiliza base de datos con idempotencia y cola de envíos.
- No se incluyen impuestos, política de reembolso, privacidad, términos, ni gestión de licencias: debes adaptarlos a tu negocio antes de lanzar.
- Los correos de cliente y propietario dependen de que Resend esté configurado correctamente. La confirmación de Stripe no equivale a entrega de archivos.
