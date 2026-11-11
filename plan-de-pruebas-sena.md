# Plan de Pruebas de Software — Sistema de Gestión de Capacitaciones SENA

**Documento elaborado bajo el estándar ISO/IEC/IEEE 29119-3:2013 (Software Testing — Part 3: Test Documentation)**

---

## 1. Información del Documento y Control de Cambios

El presente documento constituye el Plan de Pruebas Oficial para el proyecto del **Sistema de Gestión de Capacitaciones de la Escuela Nacional de Instructores (ENI) del SENA**. Este documento ha sido diseñado como una guía operativa y ejecutable para el equipo de Aseguramiento de Calidad (QA), desarrolladores y partes interesadas de la entidad.

### 1.1 Ficha Técnica del Documento

El control administrativo del documento especifica los atributos normativos y los responsables de su vigencia dentro del marco institucional.

| Atributo | Detalle Normativo / Operativo |
| :--- | :--- |
| **Identificador Único del Documento** | `SENA-ENI-TP-2026-V1.0` |
| **Título del Proyecto** | Sistema de Gestión de Capacitaciones SENA |
| **Organización Emisora** | Equipo de Ingeniería de Software y Aseguramiento de Calidad — SENA / ENI |
| **Autoridad de Aprobación** | Líder de QA, Arquitecto de Software y Director del Proyecto ENI |
| **Estado del Documento** | Versión Final para Ejecución |
| **Fecha de Emisión** | 9 de Noviembre de 2026 |

### 1.2 Historial de Modificaciones

El historial de revisiones garantiza la trazabilidad formal de las modificaciones aplicadas a la estrategia de pruebas durante el ciclo de vida del software.

| Versión | Fecha | Autor / Rol | Descripción del Cambio | Razón del Cambio |
| :--- | :--- | :--- | :--- | :--- |
| **0.1** | 01/11/2026 | Equipo de QA | Borrador inicial de estrategia de pruebas | Alineación con especificaciones funcionales |
| **0.5** | 05/11/2026 | Ingeniero Senior de Testing | Integración de estructura ISO/IEC/IEEE 29119-3 | Ajuste a estándares de documentación internacional |
| **1.0** | 09/11/2026 | Líder de Aseguramiento de Calidad | Versión aprobada para ejecución formal | Validación de alcance y criterios de éxito con ENI |

---

## 2. Introducción, Contexto del Negocio y Alcance

### 2.1 Contexto Institucional del Negocio

La Escuela Nacional de Instructores (ENI) del SENA requiere un aplicativo web centralizado que permita publicar, gestionar e inscribir capacitaciones dirigidas a los instructores de la entidad a nivel nacional. La solución busca optimizar la divulgación de convocatorias, automatizar la recepción de documentos de requisitos y controlar de forma estricta el cumplimiento de los cupos y límites de inscripción por instructor.

El testing de este aplicativo es crítico para evitar inconsistencias operativas como sobrecupos en talleres, inscripciones duplicadas en un mismo año lectivo o accesos no autorizados a la modificación de convocatorias.

### 2.2 Alcance del Plan de Pruebas

El alcance define con precisión los límites operativos del proceso de pruebas para garantizar el uso eficiente de los recursos asignados.

#### Funcionalidades Incluidas en el Alcance (In-Scope)

El equipo de pruebas validará de forma exhaustiva las siguientes funcionalidades descritas en las especificaciones funcionales del proyecto:

1. **Gestión de Convocatorias a Capacitaciones (Rol Administrador)**: Creación, edición, eliminación lógica y actualización del ciclo de vida de los estados de capacitación (**Borrador**, **Publicada**, **Cerrada**, **Cancelada**).
2. **Visualización y Consulta de Estadísticas (Rol Administrador)**: Generación gráfica del porcentaje de inscripción y conteo en tiempo real de instructores inscritos por capacitación.
3. **Consulta de Listados de Inscritos (Rol Administrador)**: Reportes detallados de instructores registrados en cada convocatoria.
4. **Catálogo y Búsqueda de Capacitaciones (Rol Instructor)**: Listado ordenado cronológicamente por fecha de inicio (de la más próxima a la más lejana), ordenamiento dinámico, filtros combinados por **Área** y **Ciudad**, y búsqueda por palabras clave.
5. **Proceso de Inscripción de Instructores (Rol Instructor)**: Validación de reglas de negocio para la inscripción, recolección de datos personales y demográficos completos, y carga/validación de archivos adjuntos en formato PDF.
6. **Validación Estricta de Reglas de Negocio (RN-1 a RN-10)**:
   - Registro de atributos obligatorios completos (Título, Área, Descripción, Fecha Inicio, Fecha Final, Ciudad, Cupos Totales, Cupos Asignados, Estado).
   - Transiciones de estado permitidas y restricciones asociadas.
   - Restricción de inscripción exclusiva a capacitaciones en estado **Publicada**.
   - Restricción de un máximo de 1 inscripción por instructor en el mismo año lectivo.
   - Control de disponibilidad de cupos en tiempo real (Cupos Asignados < Cupos Totales).
   - Validación de la obligatoriedad y formato del documento PDF adjunto.

#### Componentes Excluidos del Alcance (Out-of-Scope)

Los siguientes elementos quedan explícitamente excluidos del presente ciclo de pruebas dinámicas:

1. **Pruebas de la Infraestructura de Servidores y Red**: La configuración física del centro de datos y hardware de red del SENA es gestionada por el área de infraestructura tecnológica bajo sus propios protocolos.
2. **Integración con Sistemas Externos de Nómina o Recursos Humanos**: La verificación de la veracidad laboral del instructor se asume como válida mediante el registro de datos provisto en el aplicativo.
3. **Pruebas de Migración de Datos Históricos**: El proyecto contempla un lanzamiento desde cero, sin migración de datos legacy de convocatorias anteriores.

### 2.3 Referencias Normativas e Internas

El diseño y ejecución de este plan se fundamentan en las siguientes normas e insumos del proyecto:

* **ISO/IEC/IEEE 29119-3:2013**: *Software and systems engineering — Software testing — Part 3: Test documentation*.
* **ISO/IEC/IEEE 29119-2:2013**: *Software and systems engineering — Software testing — Part 2: Test processes*.
* **Descripción Funcional del Software**: Especificación funcional de requisitos y reglas de negocio del Sistema de Gestión de Capacitaciones SENA.

### 2.4 Glosario Técnico

* **ENI**: Escuela Nacional de Instructores del SENA.
* **TDR**: *Test Data Requirements* (Requerimientos de Datos de Prueba).
* **UAT**: *User Acceptance Testing* (Pruebas de Aceptación del Usuario).
* **RN**: Regla de Negocio especificada en la descripción funcional.

---

## 3. Objetivos de Prueba, Métricas y Criterios de Éxito

### 3.1 Objetivos Generales y Específicos

El objetivo principal es verificar que el Sistema de Gestión de Capacitaciones SENA cumpla rigurosamente con todas las especificaciones funcionales y reglas de negocio establecidas, garantizando una experiencia de usuario fluida, segura y libre de defectos críticos antes de su despliegue en producción.

#### Objetivos Específicos
* Validar el 100% de los requerimientos funcionales correspondientes a los roles de Administrador e Instructor.
* Garantizar la integridad de los datos durante la inscripción de instructores y la carga de archivos PDF.
* Verificar la correcta aplicación de las restricciones del negocio, especialmente la disponibilidad de cupos y el límite de una inscripción anual por instructor.

### 3.2 Criterios de Éxito del Proceso de Pruebas

Para declarar el proceso de testing como exitoso y autorizar el paso a producción, el sistema debe cumplir con los siguientes umbrales medibles:

* **Cobertura de Requisitos Funcionales**: 100% de las reglas de negocio (RN-1 a RN-10) y casos de uso de roles ejecutados y verificados.
* **Cierre de Defectos Críticos**: 0 defectos abiertos de Severidad 1 (Bloqueante / Crítico) y Severidad 2 (Alta).
* **Defectos Menores Aceptables**: Máximo 3 defectos abiertos de Severidad 3 (Media/Baja), con plan de mitigación aprobado para la siguiente iteración.
* **Tasa de Éxito de Ejecución**: Mínimo 95% de los casos de prueba ejecutados con resultado "Exitoso" (Pass).

### 3.3 Criterios de Entrada, Salida, Suspensión y Reanudación

La gestión del proceso de testing según ISO/IEC/IEEE 29119-3 exige la definición clara de condiciones operativas para iniciar, pausar y finalizar las actividades.

```
+-----------------------------------------------------------------------+
|                         CRITERIOS DE ENTRADA                          |
|  - Código desplegado en Ambiente de QA con Build estable              |
|  - Especificaciones funcionales aprobadas                             |
|  - Casos de prueba diseñados y revisados                              |
|  - Datos de prueba y archivos PDF de muestra preparados               |
+-----------------------------------------------------------------------+
                                   |
                                   v
+-----------------------------------------------------------------------+
|                       EJECUCIÓN DE PRUEBAS                            |
+-----------------------------------------------------------------------+
        |                                                 ^
        | (Ocurrencia de bloqueo crítico)                 | (Resolución de defecto)
        v                                                 |
+----------------------------------+            +-----------------------+
|      CRITERIOS DE SUSPENSIÓN     | ---------> | CRITERIOS REANUDACIÓN |
| - Defecto Severidad 1 en flujo   |            | - Despliegue de Hotfix|
|   principal de inscripción       |            | - Corrección confirmada|
| - Inestabilidad del Ambiente QA  |            |   en ambiente de QA   |
+----------------------------------+            +-----------------------+
        |
        v (Completitud sin bloqueos)
+-----------------------------------------------------------------------+
|                         CRITERIOS DE SALIDA                           |
|  - 100% de casos de prueba planificados ejecutados                    |
|  - 0 defectos Severidad 1 y 2 pendientes                              |
|  - Informe de Cierre de Pruebas aprobado por QA Lead y ENI            |
+-----------------------------------------------------------------------+
```

#### Criterios de Entrada (Entry Criteria)
* Disponibilidad del entorno de QA totalmente configurado con la versión candidata desplegada.
* Casos de prueba aprobados y cargados en la herramienta de gestión de pruebas.
* Set de datos de prueba preconfigurados (instructores ficticios, centros de formación, regionales y archivos PDF de prueba).

#### Criterios de Suspensión (Suspension Criteria)
* Presencia de un defecto de Severidad 1 que bloquee el flujo principal de inscripción o gestión de convocatorias sin workaround disponible.
* Inestabilidad del entorno de QA que provoque caídas del sistema o indisponibilidad por más de 4 horas consecutivas.
* Modificaciones de requisitos no planificadas que afecten a más del 20% de los casos de prueba durante la ejecución.

#### Criterios de Reanudación (Resumption Criteria)
* Despliegue de una nueva compilación (build) con la corrección verificada del defecto bloqueante.
* Restablecimiento y confirmación de estabilidad del entorno de pruebas por parte del equipo de infraestructura/desarrollo.

#### Criterios de Salida (Exit Criteria)
* Ejecución del 100% de la suite de pruebas planificada.
* Cumplimiento estricto de los umbrales de cierre de defectos (0 bloqueantes/altos).
* Entrega y firma del Reporte de Cierre de Pruebas (Test Completion Report) bajo ISO/IEC/IEEE 29119-3.

### 3.4 Métricas a Recolectar durante la Ejecución

Las métricas cuantitativas permitirán monitorear el avance y evaluar la calidad del software en tiempo real.

| Métrica | Fórmula / Método de Cálculo | Objetivo / Meta |
| :--- | :--- | :--- |
| **Cobertura de Requisitos** | (Requisitos Probados / Total Requisitos) * 100 | 100% |
| **Porcentaje de Ejecución** | (Casos Ejecutados / Total Casos Planificados) * 100 | 100% |
| **Porcentaje de Pasos Exitosos** | (Casos Exitosos / Total Casos Ejecutados) * 100 | >= 95% |
| **Densidad de Defectos** | Total Defectos Encontrados / Requisitos Funcionales | Monitoreo de calidad relativa |
| **Tasa de Re-apertura** | (Defectos Reabiertos / Total Defectos Corregidos) * 100 | < 5% |

---

## 4. Tipos de Pruebas y Secuencia de Ejecución

Para optimizar la detección temprana de fallos y garantizar una validación progresiva de la arquitectura del software, las pruebas se estructuran en fases secuenciales obligatorias.

```
[Fase 1: Unitarias] ---> [Fase 2: Integración] ---> [Fase 3: Sistema] ---> [Fase 4: UAT]
    (Desarrollo)              (APIs & BD)             (End-to-End)         (Usuarios ENI)
                                                           |
                                                           v
                                                [Pruebas Especializadas]
                                                (Seguridad & Rendimiento)
```

### 4.1 Secuencia Justificada de Niveles de Prueba

La secuencia elegida responde al principio de pruebas tempranas, garantizando que los componentes de menor nivel sean estables antes de combinarlos e interactuar con la interfaz gráfica de usuario.

#### Fase 1: Pruebas Unitarias (Unit Testing)
* **Objetivo**: Validar el correcto funcionamiento de métodos, funciones y componentes aislados de código (ej. algoritmo de ordenamiento de fechas, validadores de formato de correo o teléfono).
* **Justificación**: Permite detectar errores de lógica interna a bajo costo antes de ensamblar los módulos. Se ejecuta en el entorno de desarrollo por el equipo de desarrollo.

#### Fase 2: Pruebas de Integración (Integration Testing)
* **Objetivo**: Verificar la comunicación entre módulos internos (ej. servicio de carga de PDF con la base de datos, servicio de cálculo de cupos con el módulo de inscripciones) y servicios web.
* **Justificación**: Asegura que las interfaces entre componentes procesen y transmitan los datos correctamente antes de ejecutar pruebas de cara al usuario.

#### Fase 3: Pruebas de Sistema (System Testing - End to End)
* **Objetivo**: Validar el comportamiento completo e integrado del sistema frente a las especificaciones funcionales y reglas de negocio (RN-1 a RN-10) a través de la interfaz web.
* **Justificación**: Es la fase central donde el equipo independiente de QA simula las operaciones reales de Administradores e Instructores para garantizar que la solución satisfaga las necesidades operativas.

#### Fase 4: Pruebas de Aceptación del Usuario (UAT - User Acceptance Testing)
* **Objetivo**: Validar la usabilidad y la adecuación al proceso de negocio SENA por parte de instructores reales y funcionarios de la ENI.
* **Justificación**: Constituye la validación final previa al paso a producción, asegurando que los flujos operacionales sean intuitivos y respondan a la dinámica institucional.

#### Pruebas Complementarias Especializadas (Seguridad y Rendimiento)
* **Seguridad**: Validación de controles de acceso por rol, subida segura de archivos PDF (prevención de malware o scripts maliciosos) y protección contra inyecciones SQL o XSS.
* **Rendimiento / Carga**: Simulación de accesos concurrentes de instructores durante el lanzamiento de convocatorias de alta demanda.

---

## 5. Estrategia de Pruebas y Técnicas de Diseño

### 5.1 Enfoque General y Aplicación de Técnicas de Diseño (ISO/IEC/IEEE 29119-4)

El diseño de los casos de prueba combinará técnicas de caja negra (Black-Box Testing) estructuradas para garantizar una cobertura exhaustiva de las reglas de negocio descritas en la especificación funcional.

#### 1. Partición de Equivalencia y Análisis de Valores Límite (BVA)
Se aplicará a la validación de cupos (RN-8) y a los atributos numéricos de la convocatoria (RN-1):
* **Cupos Asignados**:
  * Clases Válidas: `0 <= Cupos Asignados < Cupos Totales` (Permite inscripción).
  * Valores Límite: `Cupos Asignados = Cupos Totales - 1` (Último cupo disponible), `Cupos Asignados = Cupos Totales` (Capacitación llena, rechaza inscripción).
  * Clases Inválidas: `Cupos Asignados > Cupos Totales` (Estado inconsistente de sistema).

#### 2. Tablas de Decisión (Decision Table Testing)
Se utilizarán para la regla de inscripción de instructores (RN-6, RN-7, RN-8, RN-10):
* **Condiciones**:
  1. ¿Estado de Capacitación == "Publicada"?
  2. ¿Instructor ya inscrito en el año lectivo actual == Falso?
  3. ¿Cupos Disponibles > 0?
  4. ¿Archivo PDF adjunto válido cargado?
* **Acciones**:
  * Si todas las condiciones son Verdaderas -> Inscripción Exitosa (Cupos Asignados incrementa en 1).
  * Si alguna condición es Falsa -> Rechazo de inscripción con mensaje de error específico.

#### 3. Pruebas de Transición de Estados (State Transition Testing)
Se aplicará al ciclo de vida de las convocatorias (RN-2):

```
+------------+   Publicar    +-----------+    Límite Cupos / Fecha   +-----------+
|  Borrador  | ------------> | Publicada | ------------------------> |  Cerrada  |
+------------+               +-----------+                           +-----------+
      |                            |
      | Cancelar                   | Cancelar
      v                            v
+--------------------------------------------------------------------------------+
|                                   Cancelada                                    |
+--------------------------------------------------------------------------------+
```

* **Transiciones Válidas**:
  * `Borrador -> Publicada` (Habilita inscripciones).
  * `Publicada -> Cerrada` (Deshabilita inscripciones).
  * `Borrador -> Cancelada` / `Publicada -> Cancelada` (Deshabilita inscripciones).
* **Transiciones Inválidas (Pruebas Negativas)**:
  * `Cerrada -> Borrador` / `Cancelada -> Publicada` (Transiciones no contempladas).

### 5.2 Estrategia de Re-prueba y Pruebas de Regresión

* **Re-prueba (Confirmation Testing)**: Cada defecto corregido por desarrollo será re-probado de forma inmediata ejecutando el caso de prueba fallido original.
* **Pruebas de Regresión (Regression Testing)**: Tras la integración de correcciones o nuevos builds, se ejecutará una suite automatizada de regresión compuesta por los flujos críticos de negocio (creación de convocatoria, ordenamiento por fecha, filtrado y flujo exitoso de inscripción) para asegurar que los cambios no introduzcan impactos no deseados en funcionalidades existentes.

### 5.3 Entorno de Pruebas (Test Environment Requirements)

De acuerdo con la norma ISO/IEC/IEEE 29119-3 (Clause 7.6), se especifican las características del entorno de QA:

* **Servidor de Aplicación**: Instancia idéntica en arquitectura a producción (Node.js/Java/Python según stack del SENA) aislada en la red de pruebas.
* **Base de Datos de QA**: Motor relacional (PostgreSQL / MySQL) poblado con datos sintéticos y anonimizados de centros de formación, regionales e instructores ficticios.
* **Navegadores Soportados**: Google Chrome (últimas 2 versiones), Mozilla Firefox, Microsoft Edge y Chrome Mobile para pruebas de diseño responsivo.
* **Herramientas de Software y Automatización**:
  * **Gestión de Pruebas y Defectos**: Jira / TestRail.
  * **Automatización Web**: Selenium WebDriver / Playwright / Cypress.
  * **Pruebas de API / Servicios**: Postman / Bruno.
  * **Pruebas de Carga**: JMeter.

---

## 6. Matriz de Cobertura y Casos de Prueba Típicos

Para asegurar que el plan sea inmediatamente usable por un tester, se presenta el mapeo de los requerimientos a condiciones de prueba y casos de prueba ejecutables.

### 6.1 Matriz de Trazabilidad: Requisitos vs. Condiciones de Prueba

La trazabilidad bidireccional garantiza que no existan reglas de negocio sin validar ni casos de prueba huérfanos.

| Requisito / Regla | Descripción de la Regla de Negocio | Rol Asociado | Condición de Prueba Principal |
| :--- | :--- | :--- | :--- |
| **RN-1** | Atributos obligatorios en la convocatoria | Administrador | Validar la creación completa con 9 atributos requeridos. |
| **RN-2** | Transición de estados de convocatoria | Administrador | Verificar comportamiento en Borrador, Publicada, Cerrada y Cancelada. |
| **RN-3** | Listado ordenado por Fecha de Inicio | Instructor / Admin | Confirmar orden ascendente por fecha de inicio más próxima. |
| **RN-4** | Filtro del listado por Área y Ciudad | Instructor / Admin | Probar filtrado individual y combinado por área y ciudad. |
| **RN-5** | Búsqueda por palabras clave | Instructor / Admin | Validar búsqueda exacta y parcial en título y descripción. |
| **RN-6** | Inscripción restringida a estado Publicada | Instructor | Intentar inscripción en capacitaciones en Borrador, Cerrada o Cancelada. |
| **RN-7** | Límite de 1 sola inscripción anual | Instructor | Intentar segunda inscripción de un mismo instructor en el mismo año. |
| **RN-8** | Control de cupos disponibles | Instructor | Intentar inscripción en convocatoria con Cupos Asignados == Cupos Totales. |
| **RN-9** | Formulario con 7 datos obligatorios | Instructor | Validar la obligatoriedad de ID, nombres, apellidos, correo, tel, centro, regional. |
| **RN-10** | Requisito adjunto en archivo PDF | Instructor | Probar carga de PDF válido, archivo no PDF (txt, docx) y omisión de archivo. |

### 6.2 Especificación de Casos de Prueba Representativos (Guía Operativa)

#### Caso de Prueba CP-01: Verificación de Límite de Inscripción Anual por Instructor (RN-7)

* **ID Caso de Prueba**: `CP-FUNC-001`
* **Módulo / Funcionalidad**: Inscripciones / Restricciones de Negocio
* **Objetivo**: Verificar que el sistema impida la inscripción de un instructor si este ya se encuentra inscrito en otra capacitación en el mismo año lectivo.
* **Precondiciones**:
  1. Existe un instructor con número de identificación `1015432109` registrado previamente en la capacitación "Pedagogía Humana 2026" (Estado: Publicada).
  2. Existe una segunda capacitación "Evaluación por Competencias 2026" en estado **Publicada** y con cupos disponibles.
* **Pasos de Ejecución**:
  1. Ingresar al aplicativo como Instructor.
  2. Buscar la capacitación "Evaluación por Competencias 2026".
  3. Hacer clic en el botón **Inscribirse**.
  4. Inserte los datos del formulario incluyendo la identificación `1015432109`.
  5. Adjuntar un archivo PDF válido con los requisitos.
  6. Hacer clic en **Confirmar Inscripción**.
* **Resultado Esperado**: El sistema bloquea el registro, muestra un mensaje de advertencia claro al usuario: *"El instructor ya cuenta con una inscripción registrada para el presente año lectivo"* y no incrementa los cupos asignados.

#### Caso de Prueba CP-02: Control de Disponibilidad de Cupos y Cambio de Estado (RN-8 y RN-2)

* **ID Caso de Prueba**: `CP-FUNC-002`
* **Módulo / Funcionalidad**: Inscripciones / Control de Cupos
* **Objetivo**: Verificar que el sistema no permita inscripciones cuando los cupos asignados alcancen el límite de cupos totales.
* **Precondiciones**:
  1. Capacitación "Seguridad Digital SENA" en estado **Publicada** con `Cupos Totales = 10` y `Cupos Asignados = 9`.
* **Pasos de Ejecución**:
  1. Realizar la inscripción exitosa del instructor A.
  2. Verificar que `Cupos Asignados` cambie automáticamente a `10`.
  3. Intentar realizar la inscripción del instructor B utilizando datos válidos y archivo PDF.
* **Resultado Esperado**: En la paso 1, la inscripción se procesa con éxito. En la paso 3, el sistema rechaza la solicitud mostrando el mensaje: *"La capacitación seleccionada ha completado el total de cupos disponibles"*. El botón de inscripción se deshabilita y el estado de la capacitación cambia automáticamente a **Cerrada**.

#### Caso de Prueba CP-03: Validación de Carga de Archivo Adjunto en Formato PDF (RN-10)

* **ID Caso de Prueba**: `CP-FUNC-003`
* **Módulo / Funcionalidad**: Inscripciones / Adjuntos
* **Objetivo**: Validar que el sistema acepte únicamente archivos en formato PDF y rechace otros formatos no autorizados.
* **Precondiciones**: Capacitación en estado **Publicada** con cupos disponibles.
* **Pasos de Ejecución**:
  1. Iniciar el formulario de inscripción con datos de un instructor válido.
  2. Adjuntar un archivo con formato `.docx` o `.jpg` en el campo de requisitos.
  3. Hacer clic en **Confirmar Inscripción**.
  4. Reemplazar el archivo adjunto por un archivo en formato `.pdf`.
  5. Hacer clic en **Confirmar Inscripción**.
* **Resultado Esperado**: En la paso 3, el sistema muestra un error de validación en línea: *"Formato de archivo no válido. Se requiere un archivo en formato PDF"*. En el paso 5, el sistema procesa la inscripción correctamente.

---

## 7. Registro de Riesgos de Testing y Plan de Mitigación

De acuerdo con la estructura exigida por la norma ISO/IEC/IEEE 29119-3 (Clause 6.2.6), los riesgos se clasifican en Riesgos del Producto (calidad técnica/funcional del software) y Riesgos del Proyecto (gestión, recursos y tiempos).

### 7.1 Riesgos del Producto (Product Risks)

Los riesgos del producto evalúan las posibles fallas funcionales y técnicas del sistema y su impacto directo en la operación de la ENI.

| ID | Descripción del Riesgo | Impacto | Probabilidad | Nivel de Exposición | Plan de Mitigación / Tratos de Riesgo |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RP-01** | Fallo en la validación del límite anual de inscripción (RN-7) permitiendo inscripciones múltiples bajo variaciones en el documento de identidad. | Alto (5) | Media (3) | **Alto (15)** | Diseñar pruebas de integración orientadas a sanear espacios, guiones y tipos de documento. Automatizar pruebas con escenarios borde en la BD. |
| **RP-02** | Condición de carrera (Race Condition) en inscripciones concurrentes sobre el último cupo disponible (RN-8). | Alto (5) | Media (3) | **Alto (15)** | Ejecutar pruebas de carga y concurrencia simulando múltiples solicitudes simultáneas sobre el cupo `N-1`. |
| **RP-03** | Subida de archivos PDF maliciosos o ejecutables renombrados a `.pdf` afectando la seguridad del servidor (RN-10). | Crítico (6)| Baja (2) | **Medio (12)** | Incorporar pruebas de seguridad (PenTesting) en la carga de archivos: validación de cabeceras MIME y antivirus en servidor. |
| **RP-04** | Error en el algoritmo de ordenamiento por fecha de inicio (RN-3) mostrando convocatorias vencidas en primer lugar. | Medio (3)| Baja (2) | **Bajo (6)** | Diseñar casos de prueba con conjuntos de datos cronológicos variados (fechas pasadas, presentes, futuras). |

### 7.2 Riesgos del Proyecto (Project Risks)

Los riesgos del proyecto contemplan los imprevistos organizacionales, de agenda y recursos que podrían interferir con la ejecución oportuna de las pruebas.

| ID | Descripción del Riesgo | Impacto | Probabilidad | Nivel de Exposición | Plan de Mitigación / Tratos de Riesgo |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RJ-01** | Retrasos en la entrega del entorno de pruebas (QA) por parte del equipo de desarrollo/infraestructura. | Alto (5) | Media (3) | **Alto (15)** | Definir un ambiente local alternativo con contenedores Docker para iniciar pruebas unitarias e integración de API tempranamente. |
| **RJ-02** | Indisponibilidad de instructores clave del SENA para la fase de Pruebas de Aceptación de Usuario (UAT). | Medio (4)| Media (3) | **Medio (12)** | Coordinar con la ENI la reserva de agenda de los instructores con 2 semanas de anticipación y elaborar guías de UAT paso a paso. |
| **RJ-03** | Cambios de último momento en las Reglas de Negocio durante la fase de ejecución de pruebas. | Alto (5) | Baja (2) | **Medio (10)** | Establecer un protocolo formal de Control de Cambios. Todo cambio exigirá re-estimación de tiempos y actualización del plan. |

---

## 8. Cronograma Indicativo, Fases e Hitos

El cronograma proyectado abarca un ciclo de testing de **4 semanas**, estructurado conforme a las fases del proceso dinámico de pruebas.

```
Semana 1: Planificación, Análisis y Diseño de Pruebas
Semana 2: Configuración de Entorno & Ejecución Ciclo 1 (Funcional)
Semana 3: Re-pruebas, Regresión Automatizada & Pruebas No Funcionales
Semana 4: Pruebas de Aceptación UAT & Informe de Cierre
```

### 8.1 Plan de Trabajo por Fases

La distribución de actividades por fases delimita las tareas diarias del equipo de calidad.

| Fase de Testing | Duración Estimada | Actividades Principales | Entregables Clave |
| :--- | :--- | :--- | :--- |
| **Fase 1: Planificación y Diseño** | 5 días hábiles | Elaboración del Plan de Pruebas, diseño de Casos de Prueba en Jira/TestRail, matriz de trazabilidad. | Plan de Pruebas Aprobado, Suite de Casos de Prueba. |
| **Fase 2: Preparación del Entorno** | 2 días hábiles | Configuración de BD QA, generación de datos de prueba y carga de archivos PDF de muestra. | Entorno QA Listo, *Test Data Readiness Report*. |
| **Fase 3: Ejecución Ciclo 1** | 5 días hábiles | Ejecución de casos de prueba de Sistema (RN-1 a RN-10), reporte de incidentes en Jira. | Registro de Ejecución, Reporte Diario de Defectos. |
| **Fase 4: Re-pruebas y Regresión** | 4 días hábiles | Validación de Hotfixes, ejecución de suite de regresión y pruebas de rendimiento/seguridad. | *Test Status Report*, Suite de Regresión Aprobada. |
| **Fase 5: Pruebas UAT y Cierre** | 4 días hábiles | Acompañamiento a instructores en UAT, consolidación de métricas finales y firma de aceptación. | *Test Completion Report* (Informe de Cierre). |

### 8.2 Hitos Principales del Proyecto (Milestones)

* **Hito 1 (Día 5)**: Aprobar los Casos de Prueba y la Matriz de Trazabilidad.
* **Hito 2 (Día 7)**: Certificar la preparación del Entorno de QA (*Test Environment Readiness*).
* **Hito 3 (Día 17)**: Lograr la resolución y verificación del 100% de los defectos Severidad 1 y 2.
* **Hito 4 (Día 20)**: Obtener la Firma de Aprobación del Informe de Cierre de Pruebas por la ENI.

---

## 9. Roles, Responsabilidades y Gobierno de Comunicaciones

### 9.1 Matriz de Asignación de Responsabilidades (RACI)

La matriz RACI especifica el nivel de participación de cada rol durante las etapas clave de testing:
* **R (Responsible)**: Quien realiza la actividad.
* **A (Accountable)**: Quien aprueba y responde por el resultado final.
* **C (Consulted)**: Quien aporta información clave para la actividad.
* **I (Informed)**: Quien recibe información sobre el avance.

| Actividad / Proceso de Testing | QA Lead | Tester / QA Engineer | Dev Lead | Director ENI / Product Owner |
| :--- | :---: | :---: | :---: | :---: |
| Elaboración del Plan de Pruebas | **A / R** | C | C | I |
| Diseño de Casos de Prueba | A | **R** | C | I |
| Preparación de Datos de Prueba | A | **R** | C | I |
| Despliegue del Build en QA | I | I | **A / R** | I |
| Ejecución de Pruebas de Sistema | A | **R** | I | I |
| Reporte y Gestión de Incidentes | A | **R** | C | I |
| Corrección de Defectos | I | I | **A / R** | I |
| Ejecución de Pruebas UAT | C | C | I | **A / R** |
| Aprobación del Informe de Cierre | **A** | I | I | **A** |

### 9.2 Protocolo de Comunicaciones y Reportes

De acuerdo con los estándares ISO/IEC/IEEE 29119-3, se establecen los siguientes canales y reportes de seguimiento:

1. **Reporte Diario de Estado (Daily Standup / Bug Tracking)**: Breve actualización sobre casos ejecutados, bloqueos e incidentes reportados en la jornada.
2. **Reporte Semanal de Estado de Pruebas (*Test Status Report*)**: Documento formal emitido cada viernes detallando el avance frente al cronograma, gráfico de burndown de defectos y resumen de riesgos activos.
3. **Informe de Cierre de Pruebas (*Test Completion Report*)**: Documento emitido al finalizar el ciclo de testing que resume las métricas logradas, lista de entregables y la recomendación técnica para el despliegue en producción.

---

**Plan de Pruebas elaborado y digitalizado para el Sistema de Gestión de Capacitaciones SENA.**
