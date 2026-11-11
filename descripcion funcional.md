**Contexto**

En el SENA, la Escuela Nacional de Instructores ENI, desea un aplicativo Web donde puedan registrar las convocatorias a capacitaciones que ofrecen a los instructores de la entidad para que estos puedan inscribirse a alguna de ellas.

**Reglas del negocio:**

1.	Todas las capacitaciones deben tener (título, área, descripción, fecha inicio, fecha final, ciudad, cupos totales, cupos asignados, estado)

2.	Cada capacitación puede tener los estados:
  - **Borrador**: cuando se crea.
  - **Publicada**: cuando se hace visible a los instructores para su inscripción.
  - **Cerrada**: cuando ya no recibe mas inscripciones.
  - **Cancelada**: cuando no se va a realizar.
3.	Las capacitaciones deben ser listadas en orden por fecha de inicio. Iniciando por la más próxima a realizarse.
4.	Se debe permitir filtrar el listado de capacitaciones por **área** o **ciudad**.
5.	Se debe permitir hacer búsqueda de capacitaciones por palabras claves.
6.	Los instructores solo pueden inscribirse a capacitaciones en estado **Publicada**.
7.	Un instructor sólo podrá inscribirse a una sola capacitación en el mismo año.
8. Un instructor sólo podrá inscribirse a una capacitación si esta tiene cupo disponible.
9. La inscripción de un instructor requiere su número de identificación, nombres, apellidos, correo electrónico, teléfono, centro de formación y regional a la que pertenece.
10. La  inscripción de un instructor requiere el envío de un archivo pdf con los requisitos exigidos.


**Roles:**

**1.	Administrador**

- Gestiona convocatorias.
- Cambia el estado de las convocatorias.
- Consulta gráficamente las estadísticas de una convocatoria a capacitación (número de inscritos, porcentaje de inscripción).
- Consulta el listado de Instructores inscritos en una determinada capacitación.

**2.	Instructor**

- Consulta el listado de capacitaciones en estado **Publicada**.
- Realiza filtros y búsquedas de capacitaciones por área y ciudad, de acuerdo con Regla de negocio 3 y 4
- Se inscribe a la capacitación que desee conforme con las Reglas de negocio 6, 7, 8, 9 y 10.
