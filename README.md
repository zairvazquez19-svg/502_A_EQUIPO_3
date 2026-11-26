# 502_A_EQUIPO_3

INGENIERÍA DE SOFTWARE · Sistema de Seguimiento de Tutorías (UTM · campus OAX, PUE y VER, con datos ficticios)

Este sistema da seguimiento a la tutoría de los estudiantes de tres campus:

- importa estudiantes y antecedentes académicos desde CSV, con validación;
- asigna tutores;
- registra sesiones y acuerdos;
- identifica con reglas acordadas a quién **requiere atención**;
- genera reportes por campus y un resumen nacional.

Hay cuatro roles: estudiante, tutor, coordinación de campus y coordinación nacional.

## Qué se está haciendo ahora

| Etapa | Qué es | Estado |
|---|---|---|
| E1 · Requerimientos | SRS, evidencia de entrevistas, método y métricas, plan y minuta de alcance, más el prototipo v2. El cliente aprobó el alcance el 3 nov 2026. | Entregada |
| Prototipo v3 | Corrige los errores del v2, completa lo que faltaba frente al SRS y comprueba por sí mismo los 15 criterios de aceptación (CA-01 a CA-15). | **Listo para revisión del cliente** |
| E2 · Servidor | NestJS + PostgreSQL: cuentas de prueba, permisos en la API, importación transaccional, evidencia de accesos rechazados y persistencia tras reinicio. | Siguiente paso |
| E3 a E5 | Asignación y reglas · reportes y bitácora · pruebas de aceptación y documentación de uso. | Pendiente |

### Por qué se hizo un prototipo v3

El cliente aprobó el alcance, pero **no ha respondido** a la confirmación por escrito de los supuestos A a I (SRS, sección 3). Por eso el equipo tomó una **decisión ejecutiva**:

- **No detener el avance:** se completa el prototipo con los mismos criterios que el SRS (coherencia con lo confirmado, el menor alcance posible, protección de datos y reversibilidad).
- **No ampliar el alcance:** no se agregó ninguna función que no esté en el SRS. Cualquier idea nueva se registra como propuesta.
- **Dejar evidencia que se verifique sola:** el prototipo incluye una pestaña que ejecuta los 15 criterios de aceptación y muestra lo esperado frente a lo obtenido. Así el cliente puede comprobarlo sin recorrer todo el sistema.
- **Documentar el silencio del cliente:** una pestaña lista cada supuesto como «pendiente de confirmación por escrito».

## Registro de cambios

### 26 nov 2026 · Prototipo v3

El detalle completo está en [`CAMBIOS_v3.md`](02_Prototipos/v3_actual/CAMBIOS_v3.md). Ahí se indica, para cada cambio, dónde verlo en el prototipo, en qué función del código está y qué requisito atiende.

#### Errores del v2 que se corrigieron

| Error | Corrección |
|---|---|
| El archivo de estudiantes con errores producía **8** errores, no los **7** acordados (CA-01). | Se corrigió la fila de prueba que provocaba un error extra. |
| Coordinación de un campus veía la bitácora de **todas** las sedes. | Ahora cada sede ve solo su bitácora. |
| «Corregir» y «Confirmar cumplimiento» usaban ventanas emergentes, que no funcionan en algunos visores. | Ahora son formularios dentro de la página, con justificación o evidencia obligatoria. |

#### Lo que faltaba frente al SRS y se agregó

| Se agregó | Requisito |
|---|---|
| Importación de **antecedentes académicos** (paso 2), todo o nada | RF-IMP; CA-03, CA-04 |
| El estudiante puede **aportar información a un acuerdo** sin cambiar su estado | RF-ACU-03 |
| El tutor anterior ve **«Sin acceso»** al abrir un expediente que ya no le corresponde | RF-ASG-04; CA-06 |
| **Historial de asignaciones** de tutor (inicio, fin, motivo y quién asignó) | RF-ASG-02 a 04; CA-05 |
| **Filtros** de reportes por tutor, campus y periodo | RF-REP-01, 02 |
| Bitácora con autor original, valor anterior, valor nuevo y motivo | RF-AUD-03 |
| El periodo actual se **calcula** con la fecha y el catálogo, ya no se escribe a mano | RNF-08 |
| Datos de prueba para el acuerdo cumplido que aún no vence | CA-13 |

#### Lo nuevo para la revisión del cliente

- **Pestaña «Verificación»:** ejecuta CA-01 a CA-15. Resultado: **15 de 15 cumplidos**.
- **Pestaña «Supuestos»:** puntos A a I con la decisión de la minuta y su estado pendiente.

### 26 nov 2026 · Reorganización del repositorio

Antes, los prototipos v2 y v3 estaban en la misma carpeta, con nombres casi iguales y sin índice.

| Antes | Ahora |
|---|---|
| `Entrega-Requerimientos_Sistema-Tutorias_Fase1/` | `01_Requerimientos_Fase1/` |
| `…/3_Metodo_y_Metricas_de_Calidad (1).pdf` | `01_Requerimientos_Fase1/3_Metodo_y_Metricas_de_Calidad.pdf` |
| `prototipos/Prototipo · Sistema de Seguimiento de Tutorías.html` (v2) | `02_Prototipos/v2_revisado_por_cliente/prototipo_v2.html` |
| `prototipos/Prototipo · Sistema de Seguimiento de Tutorías.md` (v2) | `02_Prototipos/v2_revisado_por_cliente/prototipo_v2.md` |
| `prototipos/Prototipo · … - Claude.pdf` (v2) | `02_Prototipos/v2_revisado_por_cliente/prototipo_v2_captura.pdf` |
| — | `02_Prototipos/v3_actual/prototipo_v3.html` y `CAMBIOS_v3.md` (nuevos) |

El contenido de los PDF entregados y del prototipo v2 **no cambió**; solo cambió su ubicación y su nombre. El historial de Git se conserva.

### 3 nov 2026 · Entrega E1

Se entregaron los documentos de requerimientos y el prototipo v2. El cliente revisó el prototipo, hizo 12 observaciones (Minuta, sección 6) y aprobó el alcance.

## Mapa del repositorio

```text
502_A_EQUIPO_3/
├── README.md                          ← este archivo
├── 01_Requerimientos_Fase1/           ← documentos entregados el 3 nov 2026 (no se modifican)
│   ├── 1_Evidencia_de_entrevistas.pdf
│   ├── 2_SRS_Sistema_de_Seguimiento_de_Tutorias.pdf
│   ├── 3_Metodo_y_Metricas_de_Calidad.pdf
│   ├── 4_Plan_de_Desarrollo.pdf
│   └── 5_Minuta_de_Alcance_Validada.pdf
└── 02_Prototipos/
    ├── README.md                      ← qué versión es cuál y cómo revisarla
    ├── v2_revisado_por_cliente/       ← versión revisada por el cliente (histórica)
    └── v3_actual/                     ← VERSIÓN VIGENTE
        ├── prototipo_v3.html          ← se abre en el navegador
        └── CAMBIOS_v3.md              ← qué cambió, dónde verlo y evidencia de los CA
```

## Por dónde empezar

| Si quieres… | Abre |
|---|---|
| Ver qué se pidió y qué se acordó con el cliente | [`01_Requerimientos_Fase1/2_SRS_…pdf`](01_Requerimientos_Fase1/2_SRS_Sistema_de_Seguimiento_de_Tutorias.pdf) y [`5_Minuta_…pdf`](01_Requerimientos_Fase1/5_Minuta_de_Alcance_Validada.pdf) |
| Probar el prototipo actual | [`02_Prototipos/v3_actual/prototipo_v3.html`](02_Prototipos/v3_actual/prototipo_v3.html): se abre con doble clic, sin instalar nada |
| Ver la comprobación de los 15 criterios | En el prototipo v3, pestaña **Verificación** |
| Saber qué cambió del v2 al v3 y dónde verlo | [`02_Prototipos/v3_actual/CAMBIOS_v3.md`](02_Prototipos/v3_actual/CAMBIOS_v3.md) |
| Ver lo que el cliente revisó | [`02_Prototipos/v2_revisado_por_cliente/`](02_Prototipos/v2_revisado_por_cliente/) |

> El prototipo es demostrativo: «Ver como» no es autenticación y los datos se reinician al recargar la página. La autenticación real y la persistencia llegan en E2.
