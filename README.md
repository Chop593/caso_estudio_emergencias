# 🏥 Emergency Dashboard — Clínica San José
> **Caso de Estudio:** Rediseño de Salidas Efectivas para la Sala de Emergencias  
> **Sistema Operativo Destino:** Panel de Control en Tiempo Real para la Dirección Médica

**Nombres de los Integrantes:** Alexander Cepeda

---

## 📖 Contexto Histórico y Situación Actual: El Caso de la Clínica San José

La **Clínica San José** ha experimentado un incremento del 40% en su flujo de pacientes de urgencias debido a su ubicación estratégica y al aumento de incidentes de alta complejidad en la zona periurbana. A pesar de contar con un cuerpo médico altamente capacitado y equipamiento de vanguardia para la Unidad de Cuidados Intensivos (UCI), la gestión operativa interna se encuentra al borde del colapso debido a un cuello de botella tecnológico.

### El Problema de Raíz: El Sistema Heredado (*Legacy*)
Actualmente, la coordinación de la sala de emergencias depende de un software de facturación y registro clínico diseñado a finales de los años 90. Este sistema antiguo genera un **reporte automático en texto plano** que se imprime o se muestra en un monitor monocromo en la oficina de la dirección médica. 

Este reporte presenta los siguientes inconvenientes en su flujo de información:
*   Muestra a los pacientes en una lista estrictamente cronológica (por hora de llegada), ignorando por completo la gravedad de sus síntomas.
*   Mezcla números de pólizas de seguro, códigos de barras de facturación e IDs internos en las mismas líneas donde se describen paros cardiorrespiratorios o politraumatismos.
*   No se comunica con el sistema de inventario de camas de la clínica ni con el marcador de asistencia de los médicos de guardia.

### La Crisis del Director Médico
A las 21:00 de un viernes (hora pico de ingresos), el Director Médico de la Clínica San José se encuentra ante una encrucijada crítica:
1.  **Falta de Visibilidad:** Tiene 3 pacientes con sospecha de infarto agudo de miocardio esperando en la sala general, pero su reporte actual no los resalta. Están "escondidos" entre pacientes con cuadros gripales leves.
2.  **Ceguera de Recursos:** No sabe con certeza cuántas de las 25 camas de emergencias están desocupadas o en proceso de desinfección, lo que retrasa los traslados urgentes.
3.  **Falta de Coordinación de Personal:** El sistema no le indica qué especialista está libre o atrapado en un procedimiento largo (como una cirugía de trauma), impidiendo la delegación eficiente de pacientes críticos.

### La Misión del Rediseño
Este Dashboard interactivo moderno **no es un simple cambio cosmético**. Es una intervención de ingeniería de interfaces diseñada para salvar vidas. Al transformar el flujo de texto plano en una matriz de datos semaforizada (🟢/🟡/🔴) y modular, el Director Médico pasa de descifrar un reporte confuso a **gestionar recursos en tiempo real**, reduciendo el tiempo de asignación de camas de 25 minutos a menos de 3 segundos.

### Paso 1: Análisis de Deficiencias
*Basándose en la teoría de diseño de salidas, identifiquen y expliquen **3 deficiencias críticas** del reporte antiguo:*

1. **Deficiencia 1:** **Sobrecarga cognitiva e ineficiencia en el patrón de lectura (Formato lineal plano).**
   * *Descripción y Justificación:* El sistema heredado genera un bloque homogéneo de texto plano separado por tuberías (`|`), obligando al Dr. Silva a realizar una lectura secuencial completa de izquierda a derecha de los 12 registros para extraer variables críticas. En medicina de urgencias, esto aumenta peligrosamente el tiempo de respuesta ante cuadros de riesgo inminente como el del paciente `PAC001` (Posible IAM) o `PAC003` (Trauma Craneoencefálico).

2. **Deficiencia 2:** **Ausencia de codificación visual y semaforización cromática para el Triage.**
   * *Descripción y Justificación:* La interfaz viola los principios elementales de ergonomía y diseño visual al etiquetar estados críticos (`CRITICO`, `GRAVE`, `MODERADO`, `LEVE`) utilizando exactamente el mismo color, peso y tamaño de fuente que los datos administrativos. Al carecer de alertas visuales basadas en colores normados (🟢/🟡/🔴), no es posible identificar de forma inmediata que pacientes como `PAC003`, `PAC007` (Shock Séptico) y `PAC012` (Intoxicación) requieren priorización absoluta sobre las consultas crónicas ambulantes (`PAC010`).

3. **Deficiencia 3:** **Desconexión física y falta de jerarquía de los recursos clínicos de infraestructura.**
   * *Descripción y Justificación:* Los datos sobre la disponibilidad de camas en Observación (0/10), Críticos (0/3), UCI General (1/8) y el estado de los Médicos de Guardia se encuentran relegados al final del documento de texto plano. Esta disposición ignora el orden lógico de toma de decisiones del Director Médico; para gestionar el traslado a UCI de `PAC003` o `PAC007`, el doctor primero debe leer todo el reporte antes de enterarse de que solo queda una cama UCI libre en todo el hospital.

---

### Paso 2: Criterios de Selección Tecnológica
*Respondan a las 4 preguntas que justifican el canal de salida seleccionado para el Dr. Alejandro Silva:*

1. **¿Quién recibirá la información?**
   * *Respuesta:* El receptor principal es el **Dr. Alejandro Silva**, Director Médico de la Clínica San José. Requiere un nivel de detalle macro sobre el estado total de la sala (KPIs de camas y personal) combinado con un nivel micro operativo (alertas específicas de signos vitales fuera de rango y estados de Triage) para orquestar recursos de alta jerarquía.

2. **¿Cómo accederá a ella?**
   * *Respuesta:* Accederá a través de una aplicación web responsiva compatible con pantallas fijas de escritorio (monitores principales en la central de emergencias u oficina de dirección) y dispositivos móviles/tablets con conectividad Wi-Fi interna, garantizando movilidad absoluta mientras realiza rondas clínicas en el área de Choque o UCI.

3. **¿Con qué rapidez se requiere?**
   * *Respuesta:* Se requiere en **tiempo real estricto**, con una frecuencia de actualización automatizada mediante *polling* o *websockets* de pocos segundos. Un desfase o retraso en la sincronización diferida de datos podría costar la vida de pacientes graves que esperan la liberación de una cama de observación o traslado inmediato.

4. **¿Qué nivel de interacción requiere?**
   * *Respuesta:* Requiere un nivel de interacción alto y ágil. El Dr. Silva debe ser capaz de filtrar la cola de pacientes según su gravedad (ej. ver solo Triage Crítico/Rojo), ordenar las filas por tiempo de espera acumulado para evitar cuellos de botella y presionar botones de acción rápida directa (ej. "Dar de Alta" a `PAC002` o `PAC008` para liberar las camas saturadas, o "Derivar a UCI" para reubicar a `PAC003`).

---

### Paso 3: Justificación Teórica y Diseño Conceptual
*Expliquen las decisiones de diseño a partir del modelo conceptual y los principios teóricos:*

1. **Modelo Conceptual Aplicado (Información - Presentación - Contexto):**
   * **Información (Qué mostrar):** Decidimos resumir los datos crudos en variables numéricas clave de alto nivel (KPIs globales): Camas Disponibles, Cupos UCI, Total de Críticos y Médicos Disponibles (aislando al Dr. Macías que está libre). Agrupamos y estructuramos las descripciones clínicas de los comentarios en estados de acción explícitos, eliminando el ruido del ID del operador de turno.
   * **Presentación (Cómo mostrar):** Implementamos el diseño *Bento Box* mediante tarjetas visuales bien delimitadas con fuentes tipográficas de gran grosor (`font-extrabold`). Los pacientes se muestran en una tabla dinámica ordenada de forma descendente por nivel de Triage (Críticos arriba, Leves abajo) utilizando píldoras cromáticas semaforizadas: Rojo (`🔴 #EF4444`) para Crítico/Grave, Amarillo (`🟡 #F59E0B`) para Moderado y Verde (`🟢 #10B981`) para Leves listos para alta médica.
   * **Contexto (A quién y cuándo):** La propuesta responde al entorno hostil y de alta interrupción de una sala de emergencias. Al utilizar un esquema de modo oscuro de alto contraste, se optimiza el escaneo de la interfaz en ambientes de estrés visual, permitiendo que el Dr. Silva tome una decisión médica precisa en un rango inferior a **3 segundos** tras levantar la vista hacia la pantalla.

2. **Principios de Diseño de Interfaces y Pantallas Modernas:**
   * **Principio 1: Jerarquía Visual y Patrón de Lectura (F/Z):** Aplicamos este principio ubicando los elementos de control y métricas de infraestructura crítica en la zona superior izquierda (donde el ojo occidental procesa primero el estado del sistema), descendiendo hacia el desglose de pacientes en el cuerpo central y las acciones operativas a la derecha.
   * **Principio 2: Simplicidad Operativa (Menos es Más):** Se eliminó la visualización de datos de relleno administrativo en la interfaz principal. Los comentarios extensos de texto del reporte antiguo fueron sintetizados mediante burbujas informativas (*tooltips*) o truncados con elipsis, manteniendo la pantalla limpia de texto innecesario y previniendo errores de lectura por fatiga visual.

---

