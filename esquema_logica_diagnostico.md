# Esquema Lógico del Diagnóstico de Madurez

Este documento detalla la arquitectura lógica implementada en el diagnóstico (`diagnostico.html`). A diferencia de un árbol de decisiones complejo con múltiples ramas muertas, este sistema utiliza un **Modelo de Puntuación de Madurez** (Maturity Scoring Model) que es más robusto y preciso para consultoría.

## 1. Estructura General

El flujo se compone de **5 Pasos Secuenciales**:
*   **Paso 1 (Contexto):** Filtra por industria (no afecta el puntaje, pero personaliza el feedback).
*   **Pasos 2-5 (Evaluación):** Preguntas estratégicas donde cada opción tiene un valor de peso (1 a 4).
*   **Cálculo Final:** Promedio matemático de las respuestas.
*   **Resultado:** Asignación a una de las 4 Etapas de Madurez.

---

## 2. Detalle de los Pasos

### Paso 1: El Filtro de Industria (Contexto)
*   **Objetivo:** Hacer sentir al usuario comprendido.
*   **Opciones:** Servicios, E-commerce, Inversiones, Tradicional.
*   **Lógica:** No suma puntos. Sirve para validar la intención del usuario ("Analizaremos tu caso bajo la óptica de este sector").

### Pasos 2 a 5: El Motor de Puntuación
Cada pregunta tiene 4 opciones, diseñadas para corresponder a un nivel de madurez específico.

| Valor (Points) | Significado del Nivel | Perfil del Usuario |
| :--- | :--- | :--- |
| **1** | **Inicial / Idea** | Apenas validando, sin ventas, miedo a fallar. |
| **2** | **Tracción / Riesgo Personal** | Ya vende, pero opera como persona natural (desordenado). |
| **3** | **Consolidación / Riesgo Operativo** | Opera formalmente, necesita protección y blindaje. |
| **4** | **Expansión / Optimización** | Alto volumen, busca eficiencia fiscal y diversificación. |

**Las Preguntas:**
*   **Q2 (Etapa Actual):** ¿Idea vs. Operando vs. Expandiendo?
*   **Q3 (Bloqueo):** ¿Miedo vs. Problemas de Cobro vs. Tiempo?
*   **Q4 (Volumen):** `<10k` vs. `10k-50k` vs. `50k+`.
*   **Q5 (Visión):** Side hustle vs. Vivir de ello vs. Vender la empresa.

---

## 3. Lógica de Cálculo (El Algoritmo)

El sistema captura los valores de las respuestas Q2, Q3, Q4 y Q5.

```javascript
/* Algoritmo Simplificado */
Promedio = (ValQ2 + ValQ3 + ValQ4 + ValQ5) / 4
Resultado Final = Redondear(Promedio)
```

**Ejemplo de Ejecución:**
*   Usuario responde: Q2(2), Q3(1), Q4(2), Q5(2)
*   Suma: 7
*   Promedio: 1.75
*   Redondeo: 2
*   **Resultado:** Etapa 2 (Estructuración)

---

## 4. Los 4 Resultados Posibles (Enfoque: LLC como Solución)

El objetivo es posicionar la **Incorporación de LLC** como la herramienta clave, pero con un ángulo diferente según la madurez.

### 🟢 Etapa 1: Exploración (Score ~1) -> "LLC Prematura"
*   **Diagnóstico:** "Tu foco debe ser validar, no burocratizar."
*   **Veredicto LLC:** **No la necesitas todavía.** Abrirla ahora sería un gasto innecesario de mantenimiento ($300-$800/año + reportes).
*   **Call to Action (CTA):** "Guía de Validación Pre-LLC" (Lead Magnet).
*   **Objetivo:** Ahorrarle dinero al cliente y ganar confianza por honestidad.

### 🟡 Etapa 2: Estructuración (Score ~2) -> "LLC Vital para Protegerte"
*   **Diagnóstico:** "Tienes ventas pero estás desnudo legalmente."
*   **Veredicto LLC:** **Indispensable.** Necesitas una LLC para separar tu patrimonio personal de tu negocio comercial. Si te demandan hoy, van contra tus ahorros personales.
*   **Solución:** Paquete de Incorporación LLC Estándar.
*   **Call to Action (CTA):** "Agenda para Constituir tu LLC".

### 🟠 Etapa 3: Corrección (Score ~3) -> "LLC para Bancarizar y Ordenar"
*   **Diagnóstico:** "Operas informalmente y pierdes oportunidades bancarias."
*   **Veredicto LLC:** **Urgente.** Necesitas la LLC principalmente para acceder a **Banca Business** (Mercury/Relay) y pasarelas de pago (Stripe) sin bloqueos.
*   **Solución:** Paquete de Incorporación + Banking Setup.
*   **Call to Action (CTA):** "Agenda para Formalizar tu Estructura".

### 🔵 Etapa 4: Expansión (Score ~4) -> "LLC para Optimización Fiscal"
*   **Diagnóstico:** "Tu volumen exige eficiencia, no solo operación."
*   **Veredicto LLC:** **Estratégica.** Una LLC simple puede no ser suficiente; podrías necesitar una LLC anónima, una estructura Holding o elección de tributación como C-Corp.
*   **Solución:** Consultoría de Estructuración Avanzada.
*   **Call to Action (CTA):** "Sesión de Estrategia Fiscal Corporativa".

---

## 5. Resumen del Flujo UX

1.  **Inicio:** "Descubre si una LLC es rentable para ti hoy".
2.  **Preguntas:** Enfocadas en *riesgo* y *fricción operativa*.
3.  **Resultado:**
    *   Si es Etapa 2, 3 o 4 -> **El producto es la LLC**, pero el "Job to be done" cambia (Protección / Bancarización / Impuestos).
    *   Si es Etapa 1 -> Descalificado positivamente (educación).
