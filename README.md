
---

## 👥 Equipo de Desarrollo e Ingeniería
*   **Alexander Cepeda** — 
---

## 🔍 1. Auditoría de Usabilidad e Identificación de Fallas (Sistema Legacy)

El reporte en texto plano del sistema antiguo representaba un riesgo latente para la gestión clínica debido a tres debilidades arquitectónicas en su interfaz:

| Dimensión de la Falla | Manifestación en el Sistema Antiguo | Impacto Clínico / Operativo |
| :--- | :--- | :--- |
| **Sobrecarga Cognitiva** | Ausencia de agrupación semántica. Los datos clínicos críticos se mezclaban secuencialmente con metadatos administrativos. | **Aumento en el TTI (Time-to-Interactive):** El Director Médico se veía forzado a leer de forma lineal en situaciones de alto estrés. |
| **Ceguera de Contraste** | Formato plano homogéneo sin jerarquía tipográfica, variaciones de peso (`font-weight`) ni variaciones de color. | **Invisibilidad de Urgencias:** Las prioridades de vida (Triage) no capturaban la atención del ojo de manera inmediata. |
| **Desconexión de Recursos** | Dispersión de los indicadores de capacidad hospitalaria (camas ocupadas, disponibilidad en UCI, médicos de turno). | **Bloqueo en la Toma de Decisiones:** Incapacidad para coordinar derivaciones rápidas o gestionar altas eficientemente. |

---

## ⚙️ 2. Justificación de la Arquitectura Tecnológica Seleccionada

Para mitigar los problemas del sistema anterior, se descartó el prototipado estático en favor de un **Dashboard Web Interactivo** construido con **HTML5 Pro, Tailwind CSS y JavaScript Vanilla**.

### Criterios de Selección:
1.  **Cero Latencia de Renderizado:** Al no depender de pesados frameworks de JavaScript o librerías externas de gráficos de terceros, el *Time to First Byte* (TTFB) es casi nulo. El dashboard es instantáneo, crucial para terminales médicas de recursos limitados.
2.  **Ergonomía Lumínica Hospitalaria:** Se implementó un esquema de diseño de modo oscuro profundo (`bg-slate-950`). En salas de monitoreo continuo con luz artificial constante, reduce drásticamente el síndrome de fatiga visual (*Digital Eye Strain*) del personal tras jornadas extendidas de 12 a 24 horas.
3.  **Flexibilidad de Consulta:** Gracias al sistema de cuadrícula responsiva (*Grid Fluid Layout*) de Tailwind, la interfaz escala perfectamente desde la pantalla principal de monitoreo en la sala de emergencias hasta dispositivos móviles si el director se encuentra supervisando otra área clínica.

---

## 🧠 3. Fundamentación Teórica del Rediseño (Modelo Conceptual)

El núcleo de la solución se estructuró dividiendo el problema de diseño en las tres dimensiones normativas de la teoría de salidas efectivas:

### 📊 A. Dimensión de Información (¿Qué datos viajan?)
El dashboard fue diseñado bajo el principio de **relevancia estricta**. Filtramos el ruido administrativo del sistema antiguo para aislar únicamente tres tipos de indicadores clave de rendimiento (KPIs) con impacto de decisión inmediato:
*   **Indicadores de Demanda Crítica:** Conteo en tiempo real de pacientes en estado de Triage I (Resucitación / Rojo) en espera de asignación.
*   **Indicadores de Capacidad Operativa:** Ratio exacto de camas libres en sala y cupos disponibles en la Unidad de Cuidados Intensivos (UCI).
*   **Indicadores de Eficiencia Temporal:** Tiempo de retraso promedio en Triage II para evitar el colapso de la sala de espera.

### 🎨 B. Dimensión de Presentación (¿Cómo se codifican?)
*   **Ley de Región Común (Gestalt):** Agrupación en módulos aislados de estilo *Bento Box* para que el usuario asocie la información de un solo vistazo.
*   **Patrón de Lectura en "Z":** Los datos críticos se ubican en la esquina superior izquierda (donde se inicia el escaneo visual occidental) y las acciones de contingencia operativa se desplazan a la esquina inferior derecha.
*   **Semaforización Cromática Internacional:**
    *   `🔴 #EF4444` -> **Triage I (Crítico / Emergencia Severa):** Dispara un estado de alerta visual pulsante y de alta prioridad.
    *   `🟡 #F59E0B` -> **Triage II (Urgencia / Moderado):** Requiere intervención prioritaria en tiempos controlados.
    *   `🟢 #10B981` -> **Triage III (Estable / Leve):** Casos estándar sin compromiso de funciones vitales.

### 🏥 C. Dimensión de Contexto (El entorno del usuario)
El entorno del Director Médico está definido por la **alta tasa de interrupción**, niveles extremos de estrés auditivo/visual y la necesidad de tomar decisiones bajo presión. El dashboard no está diseñado para ser "estudiado", sino para ser **escaneado**. Su interfaz permite realizar una evaluación situacional exacta de la sala en un intervalo inferior a **3 segundos**.

---

