# Arquitectura

1. n8n se ejecuta cada minuto para las notificaciones individuales y en los cortes configurados para Monitoreo.
2. BigQuery obtiene únicamente visitas finalizadas y usuarios activos configurados.
3. El workflow agrupa los seriales por `visitID` y arma un mensaje por visita y destinatario.
4. Telegram entrega el mensaje al `Chat_ID` configurado.
5. BigQuery registra el envío en la tabla de auditoría para impedir reenvíos.

## Ramas

- **Escolta:** recibe su visita individual.
- **Monitoreo:** recibe los consolidados de 13:00 y 19:00; después de las 19:00 recibe novedades individuales.


---

# Operación y mantenimiento

## Validaciones diarias

- Confirmar que el workflow esté activo en n8n.
- Revisar ejecuciones con error y el nodo que las originó.
- Validar que `usuarios_notificaciones` tenga usuario, rol, estado activo y `Chat_ID`.
- Verificar la tabla `gelsa-datarutas-prod.formularios.log_notificaciones_telegram` ante cualquier sospecha de duplicidad.

## Duplicados

La clave de auditoría es `visitID|Chat_ID`. El registro se realiza después de que Telegram confirma el envío. Si un envío se repite, revisar el nodo **Repositorio Mensajes Enviados** y las ejecuciones asociadas.
