# Notificaciones Movilidad

Automatización n8n que consulta visitas finalizadas en BigQuery y entrega notificaciones operativas por Telegram.

## Estructura

- `workflows/`: exportación saneada del workflow de n8n.
- `docs/`: arquitectura, operación y seguridad.
- `changelog/`: ajustes aplicados y su validación.

## Seguridad

No se almacenan tokens, API keys, credenciales ni Chat ID en este repositorio. Las credenciales se configuran directamente en n8n.
