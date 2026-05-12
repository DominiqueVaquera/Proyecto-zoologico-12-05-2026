
Como administrador de bases de datos, aquí está el análisis de entidades para el sistema de gestión de un zoológico:Las entidades se agrupan en 5 módulos funcionales:
<img width="725" height="317" alt="image" src="https://github.com/user-attachments/assets/05c827c8-8bc2-460c-803d-2d168dd7c633" />


**Módulo de fauna** — el corazón del sistema. `ANIMAL` es la entidad central, vinculada a `ESPECIE` (con clasificación taxonómica y estado de conservación IUCN) y a `HABITAT`. La historia clínica de cada animal se registra en `HISTORIAL_MEDICO`.

**Módulo de instalaciones** — `HABITAT` agrupa los recintos, que a su vez se organizan en `ZONA` (ej. zona africana, zona acuática). Permite controlar capacidad, clima y superficie por recinto.

**Módulo de personal** — `EMPLEADO` con su `CARGO` (cuidador, veterinario, guía, etc.). Los `VETERINARIO` son una especialización implícita que puede normalizarse como subtipo o como flag en `EMPLEADO`.

**Módulo de visitantes** — `VISITANTE` realiza `VISITA` a una o varias zonas. Permite llevar taquilla, control de aforo y estadísticas de asistencia.

**Módulo de alimentación y suministros** — `ALIMENTACION` registra cada toma (qué animal, qué alimento, cuánto, quién lo hizo). `SUMINISTRO` y `PROVEEDOR` gestionan las entradas de insumos (alimento, medicamentos, equipos).

---

¿Quieres que profundice en algún módulo en particular, agregue entidades adicionales (como `EVENTO`, `REPRODUCCION` o `CUARENTENA`), o que genere el DDL SQL para alguna de estas tablas?
