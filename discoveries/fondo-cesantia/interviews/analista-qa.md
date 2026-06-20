---
fuente: entrevista
rol_entrevistado: especialista QA
primera_persona: true
anonimizada: true
fecha: 2026-06-20
---

# Entrevista - especialista QA

> Notas crudas de la conversación. Anonimizada: sin nombres de personas,
> empresas ni cifras confidenciales. El dolor de negocio se conserva tal
> como fue expresado.

**Entrevistador:** Quiero entender mejor el proceso de aplicación de pagos de préstamos porque es uno de los módulos donde más cambios realizamos. Desde tu experiencia realizando pruebas, ¿cómo debería funcionar el proceso ideal?

**E. (especialista QA):** El proceso inicia cuando el operador registra un pago realizado por el cliente. Lo primero que debe validar el sistema es que el préstamo se encuentre vigente y que el monto ingresado sea válido. Una vez registrado el pago, el sistema debe identificar cuáles son las cuotas pendientes y determinar cómo distribuir el dinero recibido.

**Entrevistador:** ¿La aplicación siempre se realiza sobre la siguiente cuota pendiente?

**E. (especialista QA):** No necesariamente. La regla general es que primero se cubran las cuotas vencidas. Si existen varias cuotas pendientes, el sistema debe aplicar el dinero comenzando por la más antigua. Esto es importante porque muchos errores ocurren cuando los desarrolladores asumen que siempre se paga la cuota actual.

**Entrevistador:** ¿Qué escenarios suelen generar más defectos?

**E. (especialista QA):** Los pagos parciales. Cuando una cuota tiene un valor de cien dólares y el cliente paga cincuenta, la cuota no debe considerarse pagada. El sistema debe mantener el saldo pendiente y acumular los pagos posteriores. Hemos encontrado defectos donde la cuota cambia incorrectamente de estado o donde el saldo pendiente desaparece.

**Entrevistador:** ¿Qué ocurre cuando el cliente paga más de lo que debe?

**E. (especialista QA):** Se genera un saldo a favor. Ese saldo debe quedar registrado para futuras aplicaciones. Una de las validaciones que siempre realizamos es verificar que el saldo a favor conserve trazabilidad. Debemos poder identificar cuándo se generó, cuánto se utilizó posteriormente y cuál es el saldo restante.

**Entrevistador:** ¿Han encontrado problemas relacionados con concurrencia o acciones repetidas del usuario?

**E. (especialista QA):** Sí. Ocurre más de lo que parece. Por ejemplo, cuando un operador presiona varias veces el botón de guardar porque percibe lentitud en el sistema. Si no existen controles adecuados pueden registrarse pagos duplicados. También hemos visto problemas cuando dos usuarios trabajan simultáneamente sobre el mismo préstamo.

**Entrevistador:** ¿Qué validaciones consideras obligatorias antes de liberar cualquier cambio relacionado con pagos?

**E. (especialista QA):** Siempre validamos pagos exactos, pagos parciales, pagos excedentes, aplicación de saldo a favor, reversos y préstamos con varias cuotas vencidas. También revisamos escenarios donde el préstamo ya está cancelado porque no debería aceptar nuevos pagos salvo procesos excepcionales autorizados.

**Entrevistador:** ¿Existen reglas que normalmente no aparecen documentadas?

**E. (especialista QA):** Sí. Algunas entidades financieras tienen acuerdos particulares. En ciertos casos existen tratamientos especiales para mora, refinanciamientos o reestructuraciones. Muchas veces estas reglas se conocen porque surgieron de incidentes anteriores o porque los usuarios operativos las aplican diariamente, pero no necesariamente están descritas en los requerimientos.

**Entrevistador:** Desde el punto de vista de calidad, ¿cuál es el riesgo más grande en este proceso?

**E. (especialista QA):** Que el estado financiero del cliente quede inconsistente. Un error en la aplicación de pagos puede provocar cuotas incorrectas, saldos erróneos, reportes financieros inconsistentes y reclamos de clientes. Por eso consideramos este módulo uno de los más sensibles dentro del sistema.
