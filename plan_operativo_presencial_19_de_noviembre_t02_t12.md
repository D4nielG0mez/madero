# Plan Operativo Presencial – Implementación EDR
**Cliente:** Grupo Madero S.A.C.  
**Fecha:** Jueves 19 de noviembre de 2026  
**Modalidad:** 100 % Presencial (en sitio)  
**Alcance:** 27 endpoints (1 equipo piloto hoy / 26 equipos proyectados para despliegue manual el 20/11)  
**Estado del cronograma:** Propuesta v4 (ejecución secuencial estricta: `T02` a `T12`)

---

## 1. Resumen secuencial de actividades del día

| Orden | ID | Fase | Actividad | Entregable / Verificación clave | Regla / Bloqueador |
| :---: | :---: | :--- | :--- | :--- | :--- |
| 1 | `T02` | Fase 2 | Inventario de 27 endpoints | Matriz de 27 equipos únicos (SO/build, hardware, usuario, criticidad, AV actual, red y acceso) | **No almacenar contraseñas** |
| 2 | `T03` | Fase 2 | Inventario de aplicaciones | Listado de aplicaciones clave y de negocio por perfil de usuario | Requisito para exclusiones y pruebas |
| 3 | `T04` | Fase 2 | Servicios críticos y línea base | Catálogo de servicios críticos + casos de prueba antes/después | Base obligatoria para evaluar `T11` |
| 4 | `T05` | Fase 2 | Compatibilidad y licencias | Validación de SO, CPU/RAM, coexistencia con AV actual y conteo real de licencias | Incompatibilidad o falta de licencias detiene avance |
| 5 | `T06` | Fase 2 | Respaldos y rollback | Evidencia de respaldo recuperable + procedimiento de rollback aprobado | **BLOQUEADOR:** sin respaldo válido se detiene o escala |
| 6 | `T07` | Fase 3 | Impacto y elección de piloto | Alineamiento de permisos/consumo/reinicios + selección de 1 equipo representativo | Requiere conformidad del cliente |
| 7 | `T08` | Fase 3 | Paquete, política y transición | Paquete/política versionados + plan de transición de protección | Prohibido dejar equipos descubiertos |
| 8 | `T09` | Fase 3 | Matriz mínima de exclusiones | Exclusiones aprobadas por escrito (o constancia de "sin exclusiones") | Debe quedar firmada/aprobada antes de `T10` |
| 9 | `T10` | Fase 3 | **PUERTA GO** e instalación piloto | **GO escrito** + instalación del agente EDR en el equipo piloto | **NO instalar sin GO escrito previo** |
| 10 | `T11` | Fase 3 | Observación y pruebas piloto | Métricas de CPU/RAM, pruebas de negocio, prueba real de rollback y monitoreo de alertas | Requiere ventana suficiente de observación |
| 11 | `T12` | Fase 3 | Aceptación y capacidad 20/11 | Aprobación del piloto + cálculo real de capacidad para instalar 26 equipos sin AD mañana | Si no cabe observación o falta capacidad → **NO GO y reprogramar** |

---

## 2. Checklist operativo paso a paso

### Bloque A: Diagnóstico y levantamiento en sitio (`T02` – `T04`)
- [ ] **`T02` – Registrar los 27 endpoints únicos:**
  - [ ] Sistema operativo y compilación (*build*).
  - [ ] Procesador, memoria RAM y espacio libre en disco.
  - [ ] Usuario asignado, área y nivel de criticidad operativa.
  - [ ] Antivirus / protección actual instalada y estado.
  - [ ] Conectividad a red/internet y acceso administrativo local autorizado *(recordatorio: ingresar credenciales en sitio sin guardarlas en archivos ni notas)*.
- [ ] **`T03` – Documentar aplicaciones clave:**
  - [ ] Sistemas ERP/contables, ofimática, aplicativos locales, agentes bancarios o utilitarios críticos.
- [ ] **`T04` – Definir servicios críticos y pruebas de negocio:**
  - [ ] Listar servicios que no pueden interrumpirse.
  - [ ] Documentar el tiempo/comportamiento actual (**línea base previa**) para compararlo después de instalar el EDR.

### Bloque B: Validación técnica, licencias y respaldos (`T05` – `T06`)
- [ ] **`T05` – Validar prerrequisitos técnicos:**
  - [ ] Confirmar compatibilidad del agente EDR con cada versión de SO encontrada.
  - [ ] Verificar holgura de CPU/RAM para evitar degradación operativa.
  - [ ] Definir coexistencia o reemplazo respecto al antivirus actual.
  - [ ] Confirmar disponibilidad de las **27 licencias reales** asignadas al proyecto.
- [ ] **`T06` – Verificar respaldo recuperable y aprobar rollback:**
  - [ ] Solicitar y revisar evidencia de respaldo recuperable proporcionada por el cliente.
  - [ ] Dejar constancia de que el alcance **no incluye implementar backups ni garantiza su recuperabilidad**.
  - [ ] Aprobar el procedimiento técnico de *rollback* (desinstalación/restauración).
  - [ ] **Control estricto:** Si no existe evidencia válida o hay bloqueos sin resolver, detener el avance y escalar formalmente.

### Bloque C: Preparación del piloto (`T07` – `T09`)
- [ ] **`T07` – Alinear expectativas y seleccionar piloto:**
  - [ ] Comunicar impacto esperado (permisos requeridos, consumo inicial de escaneo, posibles reinicios).
  - [ ] Seleccionar **1 equipo piloto representativo** del parque de 27 endpoints.
- [ ] **`T08` – Preparar despliegue técnico:**
  - [ ] Versionar el paquete instalador y la política base de EDR.
  - [ ] Definir la secuencia exacta de transición entre el antivirus actual y el nuevo EDR para evitar ventanas sin protección.
- [ ] **`T09` – Formalizar exclusiones:**
  - [ ] Elaborar y obtener **aprobación escrita** de la matriz mínima de exclusiones (rutas, procesos o aplicativos críticos), o registrar por escrito que no se requieren exclusiones.

### Bloque D: Puerta GO, ejecución y validación del piloto (`T10` – `T11`)
- [ ] **`T10` – Ejecutar Puerta de Control GO #2:**
  - [ ] Confirmar cierre de `T02` a `T09` sin bloqueadores críticos.
  - [ ] Obtener **GO escrito** del responsable autorizado.
  - [ ] Instalar el agente EDR únicamente en el equipo piloto designado y verificar reporte en consola.
- [ ] **`T11` – Observar comportamiento y probar continuidad:**
  - [ ] Medir consumo de CPU, RAM y disco tras la instalación.
  - [ ] Ejecutar las pruebas de negocio definidas en `T04` (aplicaciones y servicios críticos).
  - [ ] Ejecutar la **prueba controlada de rollback** para verificar reversibilidad.
  - [ ] Monitorear eventos, bloqueos y posibles falsos positivos durante la ventana acordada.

### Bloque E: Cierre del día y validación para mañana 20/11 (`T12`)
- [ ] **`T12` – Evaluar aceptación y capacidad operativa:**
  - [ ] Revisar resultados de `T11`: aprobar piloto solo si los casos críticos y la observación son conformes.
  - [ ] Medir el tiempo real de instalación manual por equipo (considerando que **no hay Active Directory**).
  - [ ] Calcular si el equipo técnico y la disponibilidad de usuarios alcanzan para desplegar **26 equipos manualmente el 20/11** por grupos controlados.
  - [ ] Emitir resultado formal del cierre de la Fase 3 para habilitar (o reprogramar) la Puerta GO `T21` de mañana.

---

## 3. Protocolo en caso de NO GO (obligatorio)
Si en `T06`, `T10` o `T12` no se cumplen las condiciones mínimas de seguridad, tiempo de observación o capacidad para el despliegue manual, se debe detener el avance y documentar por escrito:

1. **Punto de control afectado:** (`T06` / `T10` / `T12`)
2. **Causa raíz detallada:** *(ej. ausencia de respaldo válido, incompatibilidad crítica, falsos positivos bloqueantes, ventana insuficiente de observación o capacidad insuficiente para 26 equipos manuales).*
3. **Responsable de levantar la observación:** *(Cliente / Equipo implementador).*
4. **Condición exacta de reanudación y nueva fecha propuesta.**