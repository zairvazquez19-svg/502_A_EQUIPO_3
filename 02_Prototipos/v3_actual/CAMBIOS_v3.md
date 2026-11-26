# Prototipo v3 · Registro de cambios respecto al v2

**Sistema de Seguimiento de Tutorías · Fase 1 · 26 nov 2026**

- Archivo del prototipo: [`prototipo_v3.html`](prototipo_v3.html), en esta misma carpeta.
- Versión anterior: [`../v2_revisado_por_cliente/prototipo_v2.html`](../v2_revisado_por_cliente/prototipo_v2.html). Se conserva sin cambios.
- Requisitos de referencia: [`../../01_Requerimientos_Fase1/`](../../01_Requerimientos_Fase1/), en particular el SRS v1.3 y la Minuta.

## Decisión ejecutiva

El cliente aprobó el alcance el 3 de noviembre de 2026 (Minuta, sección 9), pero no ha confirmado por escrito los supuestos A–I. Para no detener el avance, el equipo aplicó los mismos criterios de la sección 3 del SRS: coherencia con lo confirmado, el menor alcance posible, protección de datos y reversibilidad.

Qué hace el v3:

- Cierra los huecos que había entre el prototipo v2 y el SRS.
- **Comprueba por sí mismo** los 15 criterios de aceptación.
- **No agrega funciones fuera del alcance aprobado.**

## Cómo ubicar cada cambio

Abre `prototipo_v3.html` en el navegador. Arriba elige el rol en **«Ver como»** y el usuario o campus en **«Usuario»**. Después entra a la pestaña que indica la tabla.

La columna **«Código»** da el nombre de la función dentro de `prototipo_v3.html`. Para encontrarla, busca ese nombre con Ctrl/Cmd + F.

| # | Cambio | Dónde verlo (rol → pestaña) | Código | Requisito |
|---|---|---|---|---|
| 1 | Importación de **antecedentes**, todo o nada. Valida promedio de 0 a 10 con punto decimal, materias enteras, cursadas ≥ 1, reprobadas entre 0 y cursadas, antecedente sin estudiante, duplicados y registros existentes. Muestra el total antes y después del intento. | Coordinación de campus (OAX) → **Importar CSV** → «Paso 2» | `validateAnt`, `importAnt`, `impView` | RF-IMP-01 a 08; CA-03, CA-04 |
| 2 | El archivo de estudiantes con errores ahora produce exactamente **7** errores (el v2 producía 8 porque la fila 4 usaba una matrícula ya existente). | Coordinación de campus (OAX) → **Importar CSV** → «Paso 1» → botón «Cargar …con_errores.csv» | constante `BAD` | CA-01; observación #1 de la minuta |
| 3 | El estudiante **aporta información a un acuerdo** sin cambiar su estado. | Estudiante (00260101 Carla) → **Mi expediente** → tabla «Acuerdos» → «Aportar» | `doAp` | RF-ACU-03 |
| 4 | El tutor puede **abrir un expediente por matrícula**. Si no tiene asignación activa ve «Sin acceso». | Tutor → **Mis estudiantes** → «Abrir expediente por matrícula» | `list`, `exp`, `canSee` | RF-ASG-04; CA-06 |
| 5 | **Historial de asignaciones** (tutor, inicio, fin, motivo, quién asignó). | Coordinación de campus → **Estudiantes** → clic en un estudiante → tabla «Historial de asignaciones» | `doAssign`, campo `hist` | RF-ASG-02 a 04; CA-05 |
| 6 | Acuerdo cumplido que aún no vence, para probar CA-13. | Coordinación de campus (OAX) → **Estudiantes** → Mario Gil Reyes → «Acuerdos» | datos iniciales `S` | IND-04; CA-13 |
| 7 | Carla Jiménez Ríos ahora empieza con Raúl Mendoza, para que el recorrido «tutor anterior / nueva tutora» coincida con CA-06 y CA-07. | Coordinación de campus (OAX) → **Estudiantes** → Carla → «Cambiar tutor» | datos iniciales `S` | CA-05 a CA-08 |
| 8 | **Filtros de reportes**: por tutor y periodo en campus; por campus y periodo en el nivel nacional. Se agregan acuerdos vencidos y cumplidos. | Coordinación de campus → **Reportes**; Coordinación nacional → **Resumen nacional** | `rep`, `repNac`, `actPer` | RF-REP-01, 02 |
| 9 | **Bitácora** con campus, autor original, antes, después y motivo. Cada sede ve solo lo suyo (en el v2 se veían todas por un error de filtro). | Coordinación de campus → **Bitácora** (cambia entre OAX y PUE para comparar) | `log`, `bit` | RF-AUD-03; permisos |
| 10 | Formularios en la página en lugar de ventanas emergentes, para corregir y para confirmar cumplimiento. La justificación y la evidencia son obligatorias. | Tutor → expediente → «Corregir» o «Confirmar cumplimiento»; Coordinación de campus → «Corregir» en registros del tutor anterior | `doCorr`, `doCum`, `uCorr` | RF-AUD-02, RF-ACU-02; RNF-07 |
| 11 | El periodo actual y el último concluido **se calculan** con la fecha y el catálogo. | Aviso amarillo en la parte superior | constantes `PER`, `CUR`, `LC` | RNF-08 |
| 12 | Nota que distingue «evaluación incompleta» de «aún no aplicable». | Expediente de Diego Morales (incompleta) y de Gabriela Ramos (no aplicable) | `exp`, `badges` | RN-06 a 08 |
| 13 | Pestaña **Verificación**: ejecuta CA-01 a CA-15 y muestra lo esperado frente a lo obtenido. | Cualquier rol → **Verificación** (o abrir `prototipo_v3.html#verificacion`) | `runCA`, `verView` | QA Metrics (Entrega 3) |
| 14 | Pestaña **Supuestos**: puntos A–I con la decisión de la minuta y el estado «pendiente de confirmación por escrito». | Cualquier rol → **Supuestos** | `SUP`, `DEC`, `supView` | SRS §3; Minuta §8 |

Se mantienen los avisos permanentes: «Ver como» no es autenticación y los datos se reinician al recargar (observaciones #8 y #9).

## Evidencia de verificación (26 nov 2026)

Se ejecutó con Chrome headless abriendo `prototipo_v3.html#verificacion`. Resultado: **15 de 15 criterios cumplidos**.

| CA | Resultado obtenido |
|---|---|
| CA-01 | 7 errores en las filas 3 a 9; total 8 → 8 |
| CA-02 | 4 pendientes de asignación; la matrícula «00260105» conserva los ceros |
| CA-03 | 7 errores; antecedentes 13 → 13 |
| CA-04 | 4 antecedentes importados; Mario: evaluación incompleta |
| CA-05 | Inicio 2026-11-03; el motivo queda en la bitácora; 1 asignación activa |
| CA-06 | Carla no aparece en la lista del tutor anterior; el expediente muestra «Sin acceso» |
| CA-07 | La nueva tutora ve la sesión de Raúl Mendoza y no puede corregirla |
| CA-08 | Sin justificación se rechaza; con justificación se guarda; el registro de la tutora actual está bloqueado |
| CA-09 | Evaluación académica aún no aplicable |
| CA-10 | Evaluación incompleta; evolución 2025-1 → 2025-2: +0.6 |
| CA-11 | Se rechaza y pide registrar «no asistió» |
| CA-12 | Pendiente de programación; fecha 2026-10-20 |
| CA-13 | Cumplimiento «0 de 1 vencidos» (el acuerdo cumplido que no ha vencido se excluye) |
| CA-14 | 0 identificadores en el resumen; Sofía tiene 2 motivos y cuenta una sola vez |
| CA-15 | Evaluación incompleta |

Además se recorrieron los flujos con clics simulados:

- Importar con errores y después corregido, en los dos pasos.
- Asignar con y sin motivo.
- Registrar una asistencia futura (se rechaza).
- Confirmar un cumplimiento sin evidencia (se rechaza).
- Hacer una corrección propia.
- Abrir un expediente de otra sede (sale «Sin acceso»).
- Enviar un aporte del estudiante.
- Revisar el filtro de bitácora por sede.

## Propuestas nuevas (fuera de alcance)

Ninguna. Cualquier necesidad adicional se registrará aquí como propuesta, no como parte de lo acordado (Minuta, sección 5).

## Siguiente paso

Primer incremento con servidor (E2): NestJS, PostgreSQL, autenticación con cuentas de prueba, permisos en la API, importación transaccional, evidencia de accesos rechazados y persistencia tras reinicio.
