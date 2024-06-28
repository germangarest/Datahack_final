# Datahack_final
1. Descripción del problema
DH Marketing Consultants te ha contratado en calidad de analista de datos para investigar y analizar un conjunto de datos del departamento de marketing. El director de marketing requiere generar valor a partir de estos datos y te solicita realizar un análisis. Dicho análisis debe basarse en los diversos factores que podemos medir en el conjunto de datos. Se espera llevar a cabo, como mínimo, las siguientes tareas:

Limpieza de Datos
Transformación de Datos
Visualización
2. Dataset
Los datos suministrados provienen de una fuente de datos de acceso público que contiene información relacionada con cinco campañas de marketing llevadas a cabo por una empresa. Estos datos incluyen detalles sobre las plataformas utilizadas y el número de ventas generadas a través de estas plataformas, junto con otros datos de gran relevancia que ofrecen un potencial significativo para extraer una gran cantidad de información valiosa.

2.1 Obtención de los datos
Los datos han sido obtenidos de manera pública y gratuita a través del siguiente enlace. El contexto se basa en la necesidad de crear un modelo de respuesta que potencie de manera significativa la eficiencia de una campaña de marketing al aumentar las respuestas o reducir los gastos. El objetivo radica en prever quiénes responderán a una oferta de producto o servicio, lo cual puede optimizar la estrategia de marketing y maximizar los recursos invertidos en la campaña.

2.2. Campos y registros
Los campos que conforman el dataset podrían ser clasificados en 4 grupos principales, siendo 29 en total:

Datos Demográficos y Personales:

ID: Identificación única del cliente. (Tipo de dato: Entero)

Year_Birth: Año de nacimiento del cliente. (Tipo de dato: Entero)

Education: Nivel educativo del cliente. (Tipo de dato: Cadena de texto)

Marital_Status: Estado civil del cliente. (Tipo de dato: Cadena de texto)

Income: Ingresos anuales del hogar del cliente. (Tipo de dato: Numérico - decimal)

Kidhome: Número de niños pequeños en el hogar del cliente. (Tipo de dato: Entero)

Teenhome: Número de adolescentes en el hogar del cliente. (Tipo de dato: Entero)

Dt_Customer: Fecha de inscripción del cliente con la empresa. (Tipo de dato: Fecha)


Comportamiento de Compra:

Recency: Número de días desde la última compra del cliente. (Tipo de dato: Entero)

NumDealsPurchases: Número de compras realizadas con descuento. (Tipo de dato: Entero)

NumWebPurchases: Número de compras realizadas a través del sitio web de la empresa. (Tipo de dato: Entero)

NumCatalogPurchases: Número de compras realizadas usando catálogo. (Tipo de dato: Entero)

NumStorePurchases: Número de compras realizadas directamente en tiendas. (Tipo de dato: Entero)

NumWebVisitsMonth: Número de visitas al sitio web de la empresa en el último mes. (Tipo de dato: Entero)


Gastos en Productos:

MntWines: Monto gastado en productos de vino en los últimos 2 años. (Tipo de dato: Numérico - decimal)

MntFruits: Monto gastado en productos de frutas en los últimos 2 años. (Tipo de dato: Numérico - decimal)

MntMeatProducts: Monto gastado en productos de carne en los últimos 2 años. (Tipo de dato: Numérico - decimal)

MntFishProducts: Monto gastado en productos de pescado en los últimos 2 años. (Tipo de dato: Numérico - decimal)

MntSweetProducts: Monto gastado en productos dulces en los últimos 2 años. (Tipo de dato: Numérico - decimal)

MntGoldProds: Monto gastado en productos de oro en los últimos 2 años. (Tipo de dato: Numérico - decimal)


Respuestas a Campañas de Marketing:

AcceptedCmp3: 1 si el cliente aceptó la oferta en la tercera campaña, 0 en caso contrario. (Tipo de dato: Entero - binario)

AcceptedCmp4: 1 si el cliente aceptó la oferta en la cuarta campaña, 0 en caso contrario. (Tipo de dato: Entero - binario)

AcceptedCmp5: 1 si el cliente aceptó la oferta en la quinta campaña, 0 en caso contrario. (Tipo de dato: Entero - binario)

AcceptedCmp1: 1 si el cliente aceptó la oferta en la primera campaña, 0 en caso contrario. (Tipo de dato: Entero - binario)

AcceptedCmp2: 1 si el cliente aceptó la oferta en la segunda campaña, 0 en caso contrario. (Tipo de dato: Entero - binario)

Complain: 1 si el cliente presentó una queja en los últimos 2 años. (Tipo de dato: Entero - binario)

Z_CostContact: Costo fijo asociado al contacto con el cliente. (Tipo de dato: Entero)

Z_Revenue: Ingresos generados por el contacto con el cliente. (Tipo de dato: Entero)

Response: 1 si el cliente aceptó la oferta en la última campaña, 0 en caso contrario. (Tipo de dato: Entero - binario)

3. ETL
3.1 Extracción (conexión de orígen)
Para la extracción de datos se ha hecho una conexión de orígen de datos desde PowerBI hasta el archivo llamado marketing_campaign.xlsx desde Menú Datos > Libro de Excel obteniendose la siguiente visualización:

3.2 Transformación (PowerQuery)
3.3 Carga (PowerBI)
4. Modelo de Datos (Esquema en Estrella)

Tabla de Hechos:
La tabla de hechos contiene las métricas cuantitativas que vamos analizar. En este caso, las métricas más relevantes para el conjunto de datos de la campaña de marketing son:


CustomerID: clave foránea vinculada a la dimensión Cliente
CampaignI: clave foránea vinculada a la dimensión Campaña
AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5, Response: 1 para aceptado, 0 para no aceptado
Complain: 1 para queja, 0 para no queja
NumDealsPurchases, NumWebPurchases, NumCatalogPurchases, NumStorePurchases, NumWebVisitsMonth: métricas cuantitativas.

Dimensión Cliente:

CustomerID: clave primaria

Year_Birth, Education, Marital_Status, Income, Kidhome, Teenhome: atributos descriptivos

Dimensión Campaña:

CampaignID: clave primaria
CampaignName: "Campaña 1", "Campaña 2", etc
PlatformUsed: Atributos descriptivos sobre la campaña
5. Ratios y métricas de interés
Existen varias métricas clave que podríamos extraer de ese Dataset.

Tasa de Conversión por Cada Campaña:

Métrica: Calcula la tasa de conversión para cada campaña (AcceptedCmp1 hasta AcceptedCmp5) dividiendo el número de clientes que aceptaron la oferta en una campaña entre el total de clientes en esa campaña. Con esto se evalua la efectividad de cada campaña. Una tasa de conversión muy alta indicará una campaña más exitosa.

2.Tasa de Respuesta Global:


Métrica: Calcula la tasa de respuesta global dividiendo el número total de clientes que respondieron positivamente en la última campaña (Response=1) entre el total de clientes. Esta métrica proporciona una visión general de la efectividad global de la campaña y la participación del cliente.


Tasa de Quejas de Clientes:

Métrica: Calcula el porcentaje de clientes que presentaron quejas (Complain=1) en los últimos 2 años. Se indica con esto el grado de insatisfacción del cliente, lo que podría afectar las futuras estrategias de marketing y los esfuerzos de retención del cliente.


Análisis Demográfico de Clientes:

Métricas: Explora la distribución de clientes basada en Educación, Estado Civil e Ingresos. Su busca con ello comprender el perfil demográfico de los clientes puede ayudar a adaptar las campañas de marketing a segmentos de clientes específicos.


Patrones de Compra:

Métricas: Analiza la cantidad promedio invertida en diferentes categorías de productos (MntWines, MntFruits, MntMeatProducts, etc.). Calculamos los ratios de gasto en diferentes categorías de productos para entender las preferencias del cliente. De esta forma identificaremos las categorías de productos populares y preferencias del cliente, facilitando esfuerzos de marketing dirigidos.


Composición del Hogar del Cliente:

Métricas: Explora el número promedio de niños (Kidhome) y adolescentes (Teenhome) en los hogares de los clientes. Calculamos los ratios de niños y adolescentes respecto a adultos en los hogares. Se busca proporcionar un insight sobre la estructura familiar de los clientes, lo que puede influir en las estrategias de marketing, especialmente para productos orientados a la familia.


Canales de Compra de Clientes:

Métricas: Analiza el número de compras realizadas a través de diferentes canales (NumWebPurchases, NumCatalogPurchases, NumStorePurchases, etc.). Calculamos la proporción de compras en línea respecto al total de compras, compras por catálogo respecto al total de compras, etc. Identificaremos así los canales de compra más populares, guiando los esfuerzos de marketing y la asignación de recursos.


Frecuencia de Compras:

Métrica: Analiza el número promedio de días desde la última compra (Recency). Indicamos así la participación y lealtad del cliente. Un valor de recencia más bajo sugiere una participación activa del cliente.


Análisis de Respuestas de Clientes Basado en la Frecuencia de Compras:

Métrica: Calcula las tasas de respuesta basadas en diferentes periodos de recencia (por ejemplo, tasas de respuesta para clientes que realizaron una compra en los últimos 30 días, 60 días, etc.). Identificamos si la actividad reciente del cliente se correlaciona con las respuestas a las campañas, permitiendo campañas dirigidas hacia clientes activos.


Métricas de Lealtad del Cliente:

Métricas: Explora el número de ofertas y descuentos que los clientes han utilizado (NumDealsPurchases) y analizar las tasas de respuesta para estos clientes. Identificamos el impacto de los programas de lealtad y descuentos en las respuestas de los clientes, ayudando a optimizar las futuras campañas.


Participación de los Clientes en el Sitio Web de la Empresa:

Métrica: Analiza el número promedio de visitas al sitio web por mes (NumWebVisitsMonth) y las tasas de respuesta para los clientes basadas en su participación en el sitio web. Nos Ayuda a entender la correlación entre la participación en línea y las respuestas a las campañas, guiando las estrategias de marketing digital.


Análisis de Cohortes:

Métrica: Agrupa a los clientes según su fecha de inscripción (DtCustomer) y analizar sus respuestas a lo largo del tiempo. Proporcionamos insights sobre la evolución del comportamiento del cliente, ayudando a comprender las tendencias de participación a largo plazo.


Análisis de Ingresos y Costos:

Métricas: Calcula los ingresos generados por cliente (Income) y analizar los costos de marketing para cada campaña. Calculareos el ROI (Return on Investment) para cada campaña comparando los ingresos generados con los costos de marketing. Ayuda a evaluar la rentabilidad de las campañas de marketing y a optimizar la asignación presupuestaria.

