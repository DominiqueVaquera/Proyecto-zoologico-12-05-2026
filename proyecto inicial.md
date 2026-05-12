
# Como administrador de bases de datos, aquí está el análisis de entidades para el sistema de gestión de un zoológico: 
## Las entidades se agrupan en 5 módulos funcionales:
<img width="725" height="317" alt="image" src="https://github.com/user-attachments/assets/05c827c8-8bc2-460c-803d-2d168dd7c633" />


**Módulo de fauna** — el corazón del sistema. `ANIMAL` es la entidad central, vinculada a `ESPECIE` (con clasificación taxonómica y estado de conservación IUCN) y a `HABITAT`. La historia clínica de cada animal se registra en `HISTORIAL_MEDICO`.

**Módulo de instalaciones** — `HABITAT` agrupa los recintos, que a su vez se organizan en `ZONA` (ej. zona africana, zona acuática). Permite controlar capacidad, clima y superficie por recinto.

**Módulo de personal** — `EMPLEADO` con su `CARGO` (cuidador, veterinario, guía, etc.). Los `VETERINARIO` son una especialización implícita que puede normalizarse como subtipo o como flag en `EMPLEADO`.

**Módulo de visitantes** — `VISITANTE` realiza `VISITA` a una o varias zonas. Permite llevar taquilla, control de aforo y estadísticas de asistencia.

**Módulo de alimentación y suministros** — `ALIMENTACION` registra cada toma (qué animal, qué alimento, cuánto, quién lo hizo). `SUMINISTRO` y `PROVEEDOR` gestionan las entradas de insumos (alimento, medicamentos, equipos).

---

¿Quieres que profundice en algún módulo en particular, agregue entidades adicionales (como `EVENTO`, `REPRODUCCION` o `CUARENTENA`), o que genere el DDL SQL para alguna de estas tablas?

<img width="1112" height="523" alt="image" src="https://github.com/user-attachments/assets/ce92a0d4-eeea-4140-a95a-20dad51a03e5" />
<img width="1099" height="493" alt="image" src="https://github.com/user-attachments/assets/c5299a16-468f-467d-87ad-48ddc195f531" />
<img width="1100" height="542" alt="image" src="https://github.com/user-attachments/assets/51f1cd91-f562-4c94-8ee2-4237984ccc40" />
<img width="918" height="545" alt="image" src="https://github.com/user-attachments/assets/1ca45ebe-3fb2-4860-b409-4ed421c08bc7" />
<img width="1111" height="537" alt="image" src="https://github.com/user-attachments/assets/2447e822-6a88-4886-bef0-71cf84711281" />
<img width="1110" height="446" alt="image" src="https://github.com/user-attachments/assets/a8b7c7ca-867f-485a-953a-90f4a62e08e6" />
<img width="1114" height="549" alt="image" src="https://github.com/user-attachments/assets/39164e9b-0505-41af-aa05-758a42c67690" />
<img width="915" height="549" alt="image" src="https://github.com/user-attachments/assets/beaf68dc-7192-492c-bd5c-cd4bf76de58c" />
<img width="459" height="348" alt="image" src="https://github.com/user-attachments/assets/8922cf3f-bed0-4eda-b240-5bb01cd777ca" />

En total son **13 entidades** organizadas en 5 módulos. Algunos criterios de diseño aplicados:

- `INT` para todos los identificadores y llaves foráneas — más eficiente en índices y joins.
- `DECIMAL` en lugar de `FLOAT` para pesos, costos y cantidades, evitando errores de redondeo.
- `BOOLEAN` para banderas de estado (`activo`, `accesible`, `requiere_refrigeracion`).
- `DATETIME` donde importa la hora exacta (alimentación, eventos médicos) y `DATE` donde solo el día es relevante.
- Las restricciones `NOT NULL` / nullable están definidas por regla de negocio, no por conveniencia.

¿Quieres que genere el DDL completo en SQL (CREATE TABLE con constraints), o te interesa profundizar en alguna entidad específica?}

