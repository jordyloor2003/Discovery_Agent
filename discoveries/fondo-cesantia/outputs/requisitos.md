# Requisitos candidatos — fondo-cesantia

> Requisitos candidatos extraídos de la evidencia de `interviews/`. Todo
> requisito cita su archivo de entrevista y la persona o stakeholder que lo
> origina. La numeración es correlativa (R-01, R-02…). Los no funcionales
> se marcan como tales.

## Funcionales

- **[R-01]** Validar, antes de registrar un pago, que el préstamo esté
  vigente y que el monto ingresado sea válido.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA

- **[R-02]** Al registrar un pago, identificar las cuotas pendientes del
  préstamo y distribuirlas automáticamente.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA

- **[R-03]** Aplicar el dinero recibido comenzando por la cuota más antigua
  (vencida primero); nunca asumir que el pago corresponde a la cuota actual.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA ·
    coordinador-proyectos.md · Coordinador de proyectos

- **[R-04]** Tratar los pagos parciales manteniendo el saldo pendiente y
  acumulando pagos posteriores hasta completar la cuota; nunca marcar la
  cuota como pagada si el monto es inferior.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA

- **[R-05]** Cuando el pago supere el valor adeudado, generar un saldo a
  favor del cliente con trazabilidad completa: origen, montos usados y
  saldo remanente.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA

- **[R-06]** Permitir aplicar saldo a favor a futuras cuotas del mismo
  préstamo, conservando el historial de movimientos del saldo.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA

- **[R-07]** Registrar toda la información de trazabilidad de un pago:
  usuario que lo registró, fecha/hora, cuotas afectadas, monto aplicado
  por cuota, saldo a favor generado o consumido y, si aplica, reversos.
  - Tipo: funcional
  - Origen: coordinador-proyectos.md · Coordinador de proyectos ·
    analista-qa.md · Especialista QA

- **[R-08]** Soportar reversos de pagos con trazabilidad completa del
  movimiento original y del movimiento reversado.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA ·
    coordinador-proyectos.md · Coordinador de proyectos

- **[R-09]** No aceptar nuevos pagos sobre préstamos ya cancelados, salvo
  procesos excepcionales autorizados por supervisión.
  - Tipo: funcional
  - Origen: analista-qa.md · Especialista QA ·
    coordinador-proyectos.md · Coordinador de proyectos

- **[R-10]** Soportar procesos excepcionales autorizados manualmente:
  refinanciamientos, reestructuraciones, convenios especiales y
  tratamientos de mora definidos por el negocio.
  - Tipo: funcional
  - Origen: coordinador-proyectos.md · Coordinador de proyectos ·
    analista-qa.md · Especialista QA

- **[R-11]** Exponer la trazabilidad de pagos en una vista consultable por
  auditoría que muestre al menos: usuario, fecha, cuotas afectadas,
  monto aplicado y reversos asociados.
  - Tipo: funcional
  - Origen: coordinador-proyectos.md · Coordinador de proyectos

## No funcionales

- **[R-12]** Controlar la concurrencia y los dobles envíos para evitar
  pagos duplicados cuando el operador presiona "guardar" varias veces o
  dos usuarios operan sobre el mismo préstamo.
  - Tipo: no funcional (concurrencia / idempotencia)
  - Origen: analista-qa.md · Especialista QA

- **[R-13]** Mantener la consistencia del estado financiero del cliente y
  de los indicadores de cartera y contabilidad ante fallos del proceso de
  pagos; un fallo parcial no debe dejar cuotas, saldos o reportes en estado
  inconsistente.
  - Tipo: no funcional (consistencia transaccional)
  - Origen: analista-qa.md · Especialista QA ·
    coordinador-proyectos.md · Coordinador de proyectos

- **[R-14]** Garantizar que la información de auditoría permanezca
  disponible y consultable durante al menos el período requerido por el
  negocio (las consultas se realizan meses después del movimiento).
  - Tipo: no funcional (retención / auditabilidad)
  - Origen: coordinador-proyectos.md · Coordinador de proyectos

- **[R-15]** Mantener documentadas (o trazables) las reglas especiales
  del negocio (mora, refinanciamiento, reestructuración, convenios)
  que afectan al proceso de pagos, evitando que queden en conocimiento
  sólo del usuario operativo.
  - Tipo: no funcional (documentación / trazabilidad de reglas)
  - Origen: analista-qa.md · Especialista QA

- **[R-16]** Cubrir con pruebas automatizadas, al menos, los escenarios:
  pago exacto, pago parcial, pago excedente, aplicación de saldo a favor,
  reverso, múltiples cuotas vencidas y préstamo cancelado.
  - Tipo: no funcional (calidad / cobertura de pruebas)
  - Origen: analista-qa.md · Especialista QA