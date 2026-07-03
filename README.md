# Analítica de Producto y Optimización de Negocio en RappiPlus

## 📋 Descripción del Proyecto
Este proyecto despliega una solución integral de analítica de datos para la plataforma RappiPlus. El objetivo principal fue diagnosticar la salud comercial, financiera y operativa del negocio mediante tres enfoques analíticos: ingeniería y visualización de datos comerciales, un análisis profundo de retención por cohortes, y la evaluación estadística de experimentos A/B en la interfaz de usuario.

---

## 🛠️ Tecnologías y Herramientas Utilizadas
* **Base de Datos:** PostgreSQL (Extracción, limpieza, agregaciones complejas y uniones de datos).
* **Análisis de Datos & Estadística:** Python (Pandas, NumPy, Statsmodels para pruebas A/B).
* **Business Intelligence:** Power BI & DAX (Modelado de datos en estrella, diseño de páneles ejecutivos y análisis YTD).
* **Documentación:** Jupyter Notebooks & Markdown.

---

## 📈 Estructura y Módulos del Proyecto

### 1. Business Intelligence: Dashboard de Ventas y Margen Operativo (Power BI)
Se estructuró un modelo de datos robusto con una tabla de hechos conectada a dimensiones (incluyendo una tabla de fechas `Dim_Fecha` independiente) para habilitar cálculos de tiempo precisos mediante DAX. El reporte se compone de dos pantallas interconectadas mediante *Drill-through*:

* **Overview Ejecutivo:** Monitorea métricas clave de salud financiera ($51.95M de Revenue Total, $5.96M de Profit Total, Gasto en Marketing y Ticket Promedio). Incluye una curva acumulativa de ingresos (**Revenue YTD**) para medir la aceleración comercial.
* **Detalle de Producto (Auditoría Táctica):** Permite profundizar a nivel de SKU para identificar el origen exacto de las pérdidas del negocio.

#### 💡 Insights de Negocio Clave:
* **Subsidio de Categorías:** La categoría de *Electrónica* es el pilar del negocio generando **+$2.06M** en ganancias reales, mientras que *Hogar* (-$0.85M) y *Moda* (-$0.99M) operan actualmente con pérdidas críticas.
* **Anomalía de Marketing:** Al auditar los datos, se descubrió que el producto **Phone-Pro-128GB** tiene un margen destructivo (-$1.85M) debido a una sobreasignación masiva de presupuesto de marketing (cerca de $2.8M), lo que opacó por completo su facturación. Por otro lado, productos como **Blender-XL-Red** y **Jacket-Winter-M** presentan un problema de costos de producto inflados frente a su precio de venta actual.

---

### 2. Análisis de Retención por Cohortes (SQL & Python)
Se implementó un análisis de cohortes de comportamiento basado en el mes de registro de los usuarios, evaluando de manera estricta su actividad recurrente en las semanas 1, 2 y 3. 

Para garantizar la precisión de las métricas de negocio y evitar sesgos analíticos (como registrar un 100% de retención artificial), el conteo se realizó **filtrando exclusivamente los registros de interacción real del usuario (`activo = 1`)**, aislando el ruido transaccional.

#### 📊 Resultados de la Matriz de Retención:
| Cohorte | Clientes Iniciales | Retención W1 (%) | Retención W2 (%) | Retención W3 (%) |
| :---: | :---: | :---: | :---: | :---: |
| **2025-01** | 1,627 | 42.84% | 41.06% | 40.32% |
| **2025-02** | 1,444 | 42.31% | 42.17% | 43.98% |
| **2025-03** | 1,636 | 41.38% | 43.09% | 42.18% |
| **2025-04** | 1,606 | 42.34% | 43.40% | 41.28% |
| **2025-05** | 1,687 | 41.20% | 40.07% | 41.85% |

* **Conclusión:** El ecosistema de la plataforma demuestra una retención sumamente lineal y madura, estabilizándose de forma saludable en torno al **~42%** de lealtad durante las primeras tres semanas críticas. No existe una curva de decaimiento acelerado, lo que valida la fuerza de la propuesta de valor en el onboarding.

---

### 3. Validación de Impacto mediante Experimentación (Test A/B)
Se evaluó el impacto de un rediseño de la interfaz de usuario (UI) en el flujo de Checkout para medir si la modificación afectaba significativamente la tasa de conversión de compra.

* **Hipótesis Nula ($H_0$):** La nueva UI del checkout no tiene un impacto significativo en la tasa de conversión.
* **Hipótesis Alternativa ($H_1$):** La nueva UI del checkout genera una diferencia estadísticamente significativa en la tasa de conversión.
* **Prueba Aplicada:** Z-test para dos proporciones independientes ($\alpha = 0.05$).

#### 📊 Resultados Estadísticos:
* **Conversión Control:** 15.69%  
* **Conversión Tratamiento:** 16.29%  
* **Diferencia Absoluta:** +0.60%  
* **P-Value:** 0.416059

#### 🚀 Recomendación de Negocio:
**No se rechaza la Hipótesis Nula ($H_0$)**. Dado que el p-value ($0.416$) es sustancialmente mayor que el nivel de significancia del 5%, la diferencia observada del +0.60% se atribuye completamente al azar o al ruido muestral. **La recomendación estratégica es mantener la versión Control**, evitando gastar recursos técnicos y de infraestructura en desplegar un cambio de UI que no genera un retorno de inversión comprobable.
