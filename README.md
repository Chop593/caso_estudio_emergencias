# 🏥 Rediseño Estructural: Dashboard de Emergencias Médicas

Este repositorio contiene la entrega de la Actividad Práctica sobre el diseño de pantallas efectivas enfocado en la optimización del flujo clínico de la **Clínica San José**.

---


---

## 🔍 1. Diagnóstico del Reporte Heredado (Legacy)

El antiguo sistema de texto plano violaba las leyes fundamentales de la usabilidad e interfaz de usuario, provocando cuellos de botella en la gestión médica:

1.  **Carga Cognitiva Saturada:** Forzaba al Director Médico a realizar lecturas secuenciales e interpretar datos crudos sin un orden de criticidad.
2.  **Ceguera de Contraste:** Al usar un formato monótono de caracteres planos, los datos críticos (como pacientes en Triage I) se camuflaban con metadatos de control administrativo.
3.  **Inversión de Flujo:** No permitía identificar la correlación de recursos disponibles (Camas/UCI) en tiempo real para agilizar las altas y derivaciones.

---

## ⚙️ 2. Fundamentación Tecnológica y de Diseño

### Criterios de Selección:
* **Ecosistema:** HTML5 nativo y Tailwind CSS por su óptimo rendimiento de renderizado en terminales físicas de bajo consumo dentro del hospital.
* **Ergonomía:** Se aplicó una interfaz con esquema oscuro (*Slate-950*) que disminuye significativamente la fatiga ocular del personal durante guardias nocturnas prolongadas.

### Aplicación del Modelo Conceptual:
* **Información:** Eliminamos el ruido visual secundario. La pantalla solo despliega los indicadores clave (KPIs) con impacto inmediato en la toma de decisiones críticas (Camas, UCI, Triage).
* **Presentación:** Estructura basada en la *Ley de la Región Común* (tarjetas limpias y aisladas). Se implementó semaforización cromática normada de acuerdo a protocolos internacionales de urgencia (🟢/🟡/🔴).
* **Contexto:** Interfaz optimizada para escenarios hospitalarios de alta interrupción, permitiendo un escaneo y comprensión situacional total en un lapso inferior a 3 segundos.

---

### Interfaz del Dashboard Implementado:
![Vista del Dashboard](mockup.png)

---
*Entrega desarrollada bajo los lineamientos de la rúbrica de Diseño de Salidas Efectivas.*
