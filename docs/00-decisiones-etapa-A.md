# Decisiones tomadas en la Etapa A

Respuestas del cliente a las preguntas de la Etapa A. Este archivo manda sobre el encargo original cuando hay diferencias.

## Acceso del receptor
- El **asistente de IA del administrador genera el código** de seguimiento de cada receptor.
- El administrador se lo envía al receptor **por privado** (por su cuenta, fuera de la app).
- Si el receptor **descarga la app**, la vinculación se hace dentro de la app (mismo número de teléfono).
- **No se usará WhatsApp** por ahora. Los avisos y mensajes viven dentro de la app y la web.

## Llamadas
- **Las llamadas entran en la primera versión.** Son llamadas **dentro de la app** (por internet, VoIP).
- Ningún perfil ve el número real del otro. El número se registra al crear la cuenta.

## Datos que se piden al registrarse
| Perfil | Obligatorio | Opcional |
|---|---|---|
| Conductor | Nombre completo, foto de licencia, correo, teléfono | Foto de documentos del camión |
| Administrador | Nombre de la empresa, nombre del administrador, teléfono de contacto | Foto |
| Receptor | Nombre completo, teléfono | — |

- Una empresa puede tener **más de un administrador**.
- Un conductor puede trabajar para **varias empresas**.

## Prioridad
- **El asistente de IA del administrador es lo más importante.** Debe poder comunicarse con cada conductor y cada receptor de la empresa.

## Plataformas
- **Android e iOS** desde el inicio.
- El cliente **tiene una empresa** para validar.

## Cobros
- Primera versión: el cobro se hace **fuera de la app**. La app solo lo registra.
- El receptor tiene una **sección de pago** donde puede:
  - subir una foto de la transferencia;
  - subir una foto del pago en efectivo entregado;
  - escribir un mensaje.
- **Pagar por transferencia dentro de la app** queda para evaluar en la Etapa C, por costo y regulación.

## Pendiente de confirmar
1. Monto máximo de costo mensual.
2. ¿El asistente de IA **responde solo** a los mensajes entrantes, o **propone** y el administrador aprueba? El prototipo muestra la segunda opción, que respeta la regla de que el asistente nunca escribe a un receptor sin que el administrador lo pida.
3. El inicio de sesión con teléfono más código implica enviar un SMS con el código. Ese SMS tiene un costo pequeño por mensaje, que se calcula en la Etapa C.
