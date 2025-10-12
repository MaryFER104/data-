🎬 Movie Dataset Analysis
Análisis exploratorio de datos sobre películas (2000–2022) — enfoque en presupuesto, ingresos y calificaciones IMDB.

📊 Dataset
22 películas | 6 variables
Periodo: 2000–2022
Variables: Title, Genre, Year, Budget, Revenue, IMDB_Rating

🧹 Limpieza de datos
Durante el preprocesamiento se realizaron correcciones de formato y tratamiento de valores faltantes

🧮 **Imputaciones (valores faltantes)**  

Todas las imputaciones se realizan por asignación explícita (no `inplace` sobre una columna).

```python
# IMDB_Rating (18.18% faltante): imputación por media
rating_mean = df['IMDB_Rating'].mean()
df['IMDB_Rating'] = df['IMDB_Rating'].fillna(rating_mean)

# Revenue (13.64% faltante): imputación por media
revenue_mean = df['Revenue'].mean()
df['Revenue'] = df['Revenue'].fillna(revenue_mean)

# Genre (18.18% faltante): imputación por moda (valor más frecuente)
genre_mode = df['Genre'].mode()[0]
df['Genre'] = df['Genre'].fillna(genre_mode)

#Year
Algunos registros estaban escritos con texto (“Two Thousand”) en lugar de valores numéricos.
Todos los años se estandarizaron como enteros (int), permitiendo análisis temporales.
df['Year'] = df['Year'].str.replace('Two Thousand', '2000', regex=True)
df['Year'] = df['Year'].astype(int)

#Budget
Algunos valores estaban expresados con sufijos (“80M”).
Se convirtieron a formato numérico en dólares.
df['Budget'] = df['Budget'].str.replace(r'(\d+)M', lambda m: str(int(m.group(1))*1_000_000), regex=True)
df['Budget'] = df['Budget'].astype(float)

```


**Insights**
1. Géneros Más Rentables
Top 3:

🏆 Thriller - $224.9M promedio
🥈 Comedy - $211.5M promedio
🥉 Action - $177.0M promedio

Conclusión: Thriller y Comedy ofrecen mejor ROI.
<img width="979" height="534" alt="Captura de Pantalla 2025-10-12 a la(s) 1 07 20" src="https://github.com/user-attachments/assets/e462f813-bf6c-438c-809c-2c23ac74f99a" />

2. Evolución Calificaciones IMDB

Mejor año: 2003 (8.2)
Peor año: 2019 (3.9)
Media: 5.88
Tendencia: Ligera disminución
<img width="951" height="536" alt="Captura de Pantalla 2025-10-12 a la(s) 1 17 50" src="https://github.com/user-attachments/assets/fd3936b6-71a5-42a3-97c6-034fd2fb54a4" />

3. Correlación Budget-Revenue
r = + (correlación positiva)

Mayor presupuesto → Mayores ingresos (tendencia)
<img width="621" height="435" alt="Captura de Pantalla 2025-10-12 a la(s) 1 19 23" src="https://github.com/user-attachments/assets/638aa8ac-67eb-47db-82ea-5bdc4b454e95" />

Conclusión general
La base se encuentra limpia y lista para modelado o análisis predictivo.

Autor: María Fernanda Pérez | Fecha: Octubre 2025









