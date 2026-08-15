# NovaMarket-analysis
NovaMarket: Explorando Métodos de Correlación en Python
🎯 Objetivo del proyecto

Este notebook es una práctica guiada sobre análisis de correlación aplicada al comportamiento de clientes de NovaMarket. El objetivo no es solo calcular coeficientes, sino aprender a elegir el método correcto según el tipo de variable, visualizar las relaciones antes de confiar en un número, y detectar correlaciones engañosas (colinealidad, paradoja de Simpson) antes de sacar conclusiones de negocio.

El notebook recorre, de forma progresiva, cada técnica de correlación disponible y cierra con un bloque de ética y buenas prácticas para evitar interpretaciones causales incorrectas o decisiones discriminatorias basadas en datos.

📂 Dataset utilizado
nova_market_activity.csv → Datos de comportamiento y consumo de clientes de NovaMarket, con columnas como:
visitas_ultimos_30d, compras, gasto_publicitario_dirigido, puntuacion_satisfaccion, edad_cliente, ingresos_mensuales — variables numéricas.
estado_suscripcion — variable binaria (Yes/No, codificada a 1/0).
region, tipo_dispositivo — variables categóricas.
🔄 Etapas del análisis realizadas
Scatterplot inicial: primer acercamiento visual entre visitas_ultimos_30d y gasto_publicitario_dirigido, segmentado por tipo_dispositivo, para reconocer visualmente una relación positiva antes de calcular cualquier coeficiente.
Heatmap y Pairplot: matriz de correlación general (df.corr() + sns.heatmap()) para tener una vista global de todas las variables numéricas, complementada con un pairplot segmentado por tipo de dispositivo.
Correlación de Pearson y Spearman: cálculo y comparación de ambos coeficientes sobre las variables numéricas clave, identificando un caso de colinealidad fuerte (compras vs ingresos_mensuales, ≈0.96) y una relación moderada (visitas_ultimos_30d vs gasto_publicitario_dirigido, ≈0.57-0.59), con validación visual mediante scatterplots.
Correlación punto-biserial: análisis de la relación entre la variable binaria estado_suscripcion y las variables numéricas del dataset, para entender si los clientes suscritos se comportan de forma distinta a los no suscritos.
V de Cramér: medición de la asociación entre las variables categóricas region y tipo_dispositivo, mediante tabla de contingencia y prueba de chi-cuadrado.
Detección de correlaciones engañosas: comparación de la correlación global entre gasto_publicitario_dirigido y compras frente a la misma correlación calculada por región, revelando que el efecto de la publicidad varía según el segmento geográfico — un ejemplo práctico de por qué segmentar antes de concluir.
Automatización con funciones reutilizables: construcción de funciones propias (corr_numerica, corr_point_biserial, cramer_v) para aplicar cada método de correlación de forma sistemática sobre listas de columnas, sin repetir código.
Ética y buenas prácticas: cierre del notebook con seis principios aplicados directamente sobre los datos —correlación no es causalidad, riesgo de reforzar sesgos, la paradoja de Simpson, transparencia en métodos y supuestos, la importancia del contexto (variables categóricas), y por qué la correlación nunca justifica decisiones discriminatorias.
🔍 Principales hallazgos
compras e ingresos_mensuales presentan colinealidad fuerte (Pearson y Spearman ≈ 0.96), es decir, aportan información muy similar y deben tratarse con cuidado si se usan juntas en un modelo.
visitas_ultimos_30d y gasto_publicitario_dirigido muestran una relación moderada y consistente entre Pearson y Spearman (≈0.57-0.59), confirmada visualmente con scatterplot.
La relación entre gasto_publicitario_dirigido y compras cambia según la región: la correlación global (≈0.20) es débil, pero al segmentar por región se observa que la publicidad es más efectiva en el sur que en otras zonas — evidencia de que los promedios globales pueden ocultar patrones relevantes.
La asociación entre region y tipo_dispositivo es prácticamente nula (V de Cramér ≈ 0.053), es decir, el dispositivo que usa un cliente no depende de su región.
Los clientes suscritos muestran diferencias sutiles en variables como visitas_ultimos_30d frente a los no suscritos (punto-biserial ≈ 0.168), un efecto real pero de magnitud pequeña.
▶️ Cómo ejecutar el notebook

Puedes abrir y correr este análisis directamente en Google Colab, sin instalar nada en tu computador:

Entra a Google Colab.
Ve a Archivo > Abrir notebook > GitHub.
Pega la URL de este repositorio.
Selecciona el archivo NovaMarket_analysis_Google_Colab.ipynb de la lista que aparece.
El notebook se abrirá listo para ejecutar.

💡 Alternativa rápida: si el repositorio es público, puedes pegar directamente esta estructura de URL en tu navegador: https://colab.research.google.com/github/<usuario>/<repositorio>/blob/main/NovaMarket_analysis_Google_Colab.ipynb

🔁 Guía de reproducción
Ejecuta todas las celdas en orden, usando Entorno de ejecución > Reiniciar y ejecutar todo. El notebook está organizado como una progresión de técnicas: visualización inicial → heatmap/pairplot → Pearson/Spearman → punto-biserial → V de Cramér → correlaciones engañosas → automatización con funciones → ética.
La carga del dataset se repite en varias celdas (/content/nova_market_activity.csv), ya que cada sección del notebook fue pensada para poder ejecutarse de forma semi-independiente durante el aprendizaje — no es necesario cargar el archivo manualmente antes de cada sección, ya está incluido en el código.
Si subes el dataset a un entorno distinto a Colab (por ejemplo, Jupyter local), ajusta la ruta /content/nova_market_activity.csv según dónde hayas guardado el archivo.
Las funciones definidas en la sección de automatización (corr_numerica, corr_point_biserial, cramer_v) deben ejecutarse antes de las celdas que las invocan, ya que Python necesita que la función exista en memoria antes de poder llamarla.

⚠️ Si al ejecutar alguna celda aparece un error de tipo KeyError o NameError, generalmente significa que se corrió una celda fuera de orden o que el entorno se reinició a mitad de camino. La solución es reiniciar el entorno y ejecutar todas las celdas nuevamente desde el inicio.

🔗 Repositorio

Link al repositorio público del proyecto:
