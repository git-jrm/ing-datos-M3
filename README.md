# M3: Obtención y preparación de datos

> `Navegación:` [Módulo 2](https://github.com/git-jrm/ing-datos-M2), [Módulo 3](https://github.com/git-jrm/ing-datos-M3)

Algo interesante de ver son los casos y sobretodo sus soluciones
En este espacio se reunen los ejercicios y `Scripts` desarrollados en clases, los conocimientos y experiencias aprendidas en el transcurso del bootcamp.

También encontrarás por cada ejercicio una explicación detallada, instruccines para ejecutar, comentarios en las instrucciones y evidencia de pruebas.

## Índice:
- [Análisis de caso - La librería numpy](#análisis-de-caso---la-librería-numpy)
- [Análisis de caso - Obtención de datos desde archivos](#análisis-de-caso---obtención-de-datos-desde-archivos)
- [  >  ANEXO 1: Código para generar archivos CSV y Excel](#Anexo-1-c%C3%B3digo-para-generar-archivos-csv-y-excel)
- [  >  ANEXO 2: Fragmento de archivos generados](#anexo-2-fragmento-de-archivos-generados)
- [Análisis de caso - Data wrangling](#análisis-de-caso---data-wrangling)
- [  >  ANEXO 1: Código para generar el CSV](#anexo-1-código-para-generar-el-csv)
- [  >  ANEXO 2: Fragmento del CSV generado](#anexo-2-fragmento-del-csv-generado)
- [Evolución del Aprendizaje](#evoluci%C3%B3n-del-aprendizaje)
- [Conclusiones](#conclusiones)

## Análisis de caso - La librería numpy

El objetivo de esta actividad es realizar una simulación de un escenario real en el que debemos adoptar el rol de analista de datos del equipo de desarrollo, en una empresa de análisis financiero bursátil que tiene problemas en la integración y análisis de la información del mercado bursátil. El objetivo es optimizar y mejorar la eficiencia con NumPy garantizando eficiencia y eficacia.

Como analista de datos en la empresa global Statista se nos asignó proponer una solución a los problemas de formatos y estructuras en la herramienta de Rendimiento de activos. 

A continuación se presenta el código desarrollado para dar solución al análisis de caso propuesto, este codigo cuenta con una explicación detallada a modo de comentarios:

Archivo M3-L1-numpy.py :

```Python
import numpy as np


# 1. Carga
# a. Array NymPy con datos de precios de acciones de diferentes días,
# b. matriz 5 filas: acciones X 5 columnas: días de cotización:
datos_financieros = np.array([[10.10, 10.20, 10.30, 11.90, 12.80],
                             [200, 198, 202, 205, 210],
                             [1.1, 1.5, 1.5, 2.1, 1.6],
                             [300.1011, 295.9088, 310.9080, 315.3030, 390.1099],
                             [400.5050, 299.9090, 291.1010, 355.5050, 620.2020]])
nombres_acciones = ['Acción A', 'Acción B', 'Acción C', 'Acción D', 'Acción E']
nombres_dias = ['Día 1', 'Día 2', 'Día 3', 'Día 4', 'Día 5']


# 2. Análisis
# a. Obtener promedio, maximo, minimo de cada accion: a lo largo del tiempo:
promedios = np.mean(datos_financieros, axis=1)
maximos = np.max(datos_financieros, axis=1)
minimos = np.min(datos_financieros, axis=1)
print("Promedios:", promedios)
print("Máximos:", maximos)
print("Mínimos:", minimos)
# b. Calcular la variacion porcentual diaria de cada acción:
variacion_diaria = np.diff(datos_financieros, axis=1) / datos_financieros[:, :-1] * 100
print("Variación diaria:")
print(variacion_diaria)
# c. Aplica log, exponencial y normalización (4 decimales):
logaritmo = np.log(datos_financieros)
exponencial = np.exp(datos_financieros)
np.set_printoptions(precision=4, floatmode='fixed')
normalizacion = np.round(datos_financieros, 4)
print("Logaritmo:")
print(logaritmo)
print("Exponencial:")
print(exponencial)
print("Normalización:")
print(normalizacion)


# 3. Optimización
# a. utiliza indexacion avanzada para extrarer:
# - Precios de la acción A en el Día 3 y Día 5:
precios_accion_a = datos_financieros[0, [2, 4]]
print("Precios de la acción A en el Día 3 y Día 5:", precios_accion_a)
# - Precios de la acción C en el Día 1 y Día 4:
precios_accion_c = datos_financieros[2, [0, 3]]
print("Precios de la acción C en el Día 1 y Día 4:", precios_accion_c)
# - Precios de la acción D en el Día 2 y Día 3:
precios_accion_d = datos_financieros[3, [1, 2]]
print("Precios de la acción D en el Día 2 y Día 3:", precios_accion_d)
# b. broadcasting para operaciones sin bucle:
# - Suma 1% (comisión variable):
comision = 0.0109
datos_financieros_con_comision = datos_financieros * (1 + comision)
print("Datos financieros con comisión del 1%:")
print(datos_financieros_con_comision)
# - Suma 1% (comisión fija):
datos_financieros_suma = datos_financieros + 10
print("Datos financieros con suma de comisón de 10:")
print(datos_financieros_suma)
# - Duplicar cartera de acciones::
datos_financieros_multiplicacion = datos_financieros * 2
print("Datos financieros con multiplicación por 2:")
print(datos_financieros_multiplicacion)


# 4. Comparación con otros métodos:
# a. For: para realizar la tarea "2.a" con ciclo for y sin usar NumPy:
# escribe el dato "datos_financieros" desde cero sin usar numpy:
datos_financieros_sin_numpy = [
   [10.10, 10.20, 10.30, 11.90, 12.80],
   [200, 198, 202, 205, 210],
   [1500, 1550, 1530, 2180, 1600],
   [300.1011, 295.9088, 310.9080, 315.3030, 390.1099],
   [400.5050, 299.9090, 291.1010, 355.5050, 620.2020]
]
promedios_ciclo = []
maximos_ciclo = []
minimos_ciclo = []
for accion in datos_financieros_sin_numpy:
   promedio = sum(accion) / len(accion)
   maximo = max(accion)
   minimo = min(accion)
   promedios_ciclo.append(promedio)
   maximos_ciclo.append(maximo)
   minimos_ciclo.append(minimo)


# b. Array normal: para realizar la tarea "3.a" sin usar NumPy usando datos_financieros_sin_numpy:
precios_accion_a_ciclo = [datos_financieros_sin_numpy[0][2], datos_financieros_sin_numpy[0][4]]
print("Precios de la acción A en el Día 3 y Día 5 (sin NumPy):", precios_accion_a_ciclo)
precios_accion_c_ciclo = [datos_financieros_sin_numpy[2][0], datos_financieros_sin_numpy[2][3]]
print("Precios de la acción C en el Día 1 y Día 4 (sin NumPy):", precios_accion_c_ciclo)
precios_accion_d_ciclo = [datos_financieros_sin_numpy[3][1], datos_financieros_sin_numpy[3][2]]
print("Precios de la acción D en el Día 2 y Día 3 (sin NumPy):", precios_accion_d_ciclo)
```
`$ python3 M3/M3-L1-numpy.py`
```bash
$ python3 M3/M3-L1-numpy.py
Promedios: [ 11.06    203.        1.56    322.46616 393.4444 ]
Máximos: [ 12.8    210.       2.1    390.1099 620.202 ]
Mínimos: [ 10.1    198.       1.1    295.9088 291.101 ]
Variación diaria:
[[  0.99009901   0.98039216  15.53398058   7.56302521]
 [ -1.           2.02020202   1.48514851   2.43902439]
 [ 36.36363636   0.          40.         -23.80952381]
 [ -1.39696256   5.06885905   1.41360145  23.72540065]
 [-25.11728942  -2.93689086  22.12427989  74.45661805]]
Logaritmo:
[[2.3125 2.3224 2.3321 2.4765 2.5494]
 [5.2983 5.2883 5.3083 5.3230 5.3471]
 [0.0953 0.4055 0.4055 0.7419 0.4700]
 [5.7041 5.6901 5.7395 5.7535 5.9664]
 [5.9927 5.7035 5.6737 5.8735 6.4300]]
Exponencial:
[[2.4343e+004 2.6903e+004 2.9733e+004 1.4727e+005 3.6222e+005]
 [7.2260e+086 9.7793e+085 5.3393e+087 1.0724e+089 1.5916e+091]
 [3.0042e+000 4.4817e+000 4.4817e+000 8.1662e+000 4.9530e+000]
 [2.1491e+130 3.2476e+128 1.0608e+135 8.5971e+136 2.6459e+169]
 [8.6519e+173 1.7735e+130 2.6519e+126 2.4766e+154 2.2403e+269]]
Normalización:
[[ 10.1000  10.2000  10.3000  11.9000  12.8000]
 [200.0000 198.0000 202.0000 205.0000 210.0000]
 [  1.1000   1.5000   1.5000   2.1000   1.6000]
 [300.1011 295.9088 310.9080 315.3030 390.1099]
 [400.5050 299.9090 291.1010 355.5050 620.2020]]
Precios de la acción A en el Día 3 y Día 5: [10.3000 12.8000]
Precios de la acción C en el Día 1 y Día 4: [1.1000 2.1000]
Precios de la acción D en el Día 2 y Día 3: [295.9088 310.9080]
Datos financieros con comisión del 1%:
[[ 10.2101  10.3112  10.4123  12.0297  12.9395]
 [202.1800 200.1582 204.2018 207.2345 212.2890]
 [  1.1120   1.5163   1.5163   2.1229   1.6174]
 [303.3722 299.1342 314.2969 318.7398 394.3621]
 [404.8705 303.1780 294.2740 359.3800 626.9622]]
Datos financieros con suma de comisón de 10:
[[ 20.1000  20.2000  20.3000  21.9000  22.8000]
 [210.0000 208.0000 212.0000 215.0000 220.0000]
 [ 11.1000  11.5000  11.5000  12.1000  11.6000]
 [310.1011 305.9088 320.9080 325.3030 400.1099]
 [410.5050 309.9090 301.1010 365.5050 630.2020]]
Datos financieros con multiplicación por 2:
[[  20.2000   20.4000   20.6000   23.8000   25.6000]
 [ 400.0000  396.0000  404.0000  410.0000  420.0000]
 [   2.2000    3.0000    3.0000    4.2000    3.2000]
 [ 600.2022  591.8176  621.8160  630.6060  780.2198]
 [ 801.0100  599.8180  582.2020  711.0100 1240.4040]]
Precios de la acción A en el Día 3 y Día 5 (sin NumPy): [10.3, 12.8]
Precios de la acción C en el Día 1 y Día 4 (sin NumPy): [1500, 2180]
Precios de la acción D en el Día 2 y Día 3 (sin NumPy): [295.9088, 310.908]
```
Este trabajo nos permitió aplicar el uso de la librería NumPy para resolver un caso realista de análisis financiero de una manera simple, mejorando la eficiencia en operaciones matemáticas y comparando su rendimiento con métodos tradicionales ya que se puede aplicar una operación a toda la matriz de una sola vez sin tener que recorrer un ciclo. 

Se evidenció cómo las librerías adecuadas en Python optimizan tanto el desarrollo como la ejecución e interpretación de los datos. Además el escenario propuesto fue de gran ayuda para comprender situaciones reales del día a día de un analista de datos

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

## Análisis de caso - Obtención de datos desde archivos

El objetivo de esta actividad es realizar una simulación de un escenario real en el que debemos adoptar el rol de analista de datos en una empresa de consultoría que trabaja con grandes volúmenes de datos provenientes de diferentes fuentes. El objetivo específico es integrar datos desde múltiples fuentes para luego analizarlos, garantizando eficiencia y eficacia.

Como analista de datos consultor en McKinsey, nuestro principal cliente deportivo ESPN, nos solicita para su área de marketing analizar los datos de los 3 deportes que cuentan con mayor auspicio para la próxima temporada: tenis, fútbol y básquetbol. 

Se requiere procesar la data de los mejores jugadores profesionales de la actualidad. A continuación el código y explicación detallada:

(Los archivos CSV y Excel se generaron con Python: ver ANEXO 1 y 2)

Archivo M3-L3-etl.py :
```Python
import pandas as pd


print(f"\n 1. Carga de datos desde distintos archivos: ")


# 1.a: Importa un archivo CSV en un DataFrame de Pandas: Top jugadores tenis
df_tenis_csv = pd.read_csv("M3/M3-L3-top_tenis.csv")
print(f"\n • {len(df_tenis_csv)} jugadores de tenis. Columnas disponibles: {list(df_tenis_csv.columns)}")
print(df_tenis_csv.head(2))


# 1.b: Carga un archivo Excel en otro DataFrame: Top jugadores fútbol
df_futbol_excel = pd.read_excel("M3/M3-L3-top_futbol.xlsx")
print(f"\n • {len(df_futbol_excel)} jugadores de fútbol. Columnas disponibles: {list(df_futbol_excel.columns)}")
print(df_futbol_excel.head(2))


# 1.c: Extrae información de una tabla web utilizando read_html: Top jugadores NBA
df_nba_raw = pd.read_html("https://www.basketball-reference.com/leagues/NBA_2025_per_game.html")[0]
df_nba_raw = df_nba_raw[df_nba_raw['Player'] != 'Player'].head(100)  # Quitar headers duplicados
print(f"\n • {len(df_nba_raw)} jugadores de NBA. Columnas disponibles: {list(df_nba_raw.columns)}")
print(df_nba_raw.head(2))


print(f"\n 2. Limpieza y estructuración de datos: ")


# - estructuración NBA
df_nba = pd.DataFrame()
df_nba['Jugador'] = df_nba_raw[['Player']]
df_nba['Edad'] = df_nba_raw[['Age']]
df_nba['Equipo'] = df_nba_raw[['Team']]
df_nba['Deporte'] = 'Básquetbol'


# - unifica DataFrames
df_unificado = pd.concat([df_tenis_csv, df_futbol_excel, df_nba], ignore_index=True)
print("\nDataFrame combinado:")
print(df_unificado)


# - Identifica valores nulos y decide si deben ser imputados
print("\nValores nulos antes:", df_unificado.isnull().sum())
df_unificado['Pais'] = df_unificado['Pais'].fillna('N/A', inplace=False)
df_unificado['Edad'] = df_unificado['Edad'].fillna(df_unificado['Edad'].mean(), inplace=False)
print("\nValores nulos después:", df_unificado.isnull().sum())


# - Elimina filas duplicadas si es necesario
print(f"\n Valores duplicados antes: {df_unificado.duplicated().sum()}")
df_unificado.drop_duplicates(subset=['Jugador', 'Deporte'], inplace=True)
print(f"\n Valores duplicados después: {df_unificado.duplicated().sum()}")


# - Verifica y ajusta los tipos numericos, categóricos o strings
print(f"\n df_unificado.info():")
df_unificado.info()
df_unificado['Edad'] = pd.to_numeric(df_unificado['Edad'], errors='coerce')
df_unificado['Deporte'] = df_unificado['Deporte'].astype('category')
df_unificado['Jugador'] = df_unificado['Jugador'].astype('string')
df_unificado['Pais'] = df_unificado['Pais'].astype('string')
df_unificado['Market Value'] = df_unificado['Market Value'].astype('string')
df_unificado['Equipo'] = df_unificado['Equipo'].astype('string')
df_unificado.info()


print(f"\n 3. Transformación y optimización de datos: ")


# - Selecciona las columnas más relevantes para el análisis
df_unificado = df_unificado[['Jugador', 'Edad', 'Deporte']]


# - Renombra columnas para mejorar la legibilidad
df_limpio = pd.DataFrame()
df_limpio[['Nombre Jugador']] = df_unificado[['Jugador']]
df_limpio[['Edad Jugador']] = df_unificado[['Edad']]
df_limpio[['Nombre Deporte']] = df_unificado[['Deporte']]


# Ordena los datos en función de una columna clave
df_limpio = df_limpio.sort_values(by='Edad Jugador', ascending=True, inplace=False)
print("\nDataFrame limpio:", df_limpio)


print(f"\n 4. Exportación de datos: ")


# Carga (Load) DataFrame limpio a CSV y Excel sin indices:
df_limpio.to_csv("M3/M3-L3-jugadores_limpio.csv", index=False)
df_limpio.to_excel("M3/M3-L3-jugadores_limpio.xlsx", index=False)
print("\n DataFrame limpio exportado a CSV y Excel: OK")
```
`$ python3 M3/M3-L3-etl.py`
```bash
 1. Carga de datos desde distintos archivos: 


 • 21 jugadores de tenis. Columnas disponibles: ['Jugador', 'Pais', 'Edad', 'Deporte']
          Jugador Pais  Edad Deporte
0   Jannik Sinner  ITA    23   Tenis
1  Carlos Alcaraz  ESP    22   Tenis


 • 105 jugadores de fútbol. Columnas disponibles: ['Rank', 'Jugador', 'Edad', 'Market Value', 'Deporte']
   Rank          Jugador  Edad Market Value Deporte
0     1     Lamine Yamal    18     €200.00m  Fútbol
1     2  Jude Bellingham    22     €180.00m  Fútbol


 • 100 jugadores de NBA. Columnas disponibles: ['Rk', 'Player', 'Age', 'Team', 'Pos', 'G', 'GS', 'MP', 'FG', 'FGA', 'FG%', '3P', '3PA', '3P%', '2P', '2PA', '2P%', 'eFG%', 'FT', 'FTA', 'FT%', 'ORB', 'DRB', 'TRB', 'AST', 'STL', 'BLK', 'TOV', 'PF', 'PTS', 'Awards']
    Rk                   Player   Age  ...   PF   PTS                        Awards
0  1.0  Shai Gilgeous-Alexander  26.0  ...  2.2  32.7  MVP-1,DPOY-10,CPOY-8,AS,NBA1
1  2.0    Giannis Antetokounmpo  30.0  ...  2.3  30.4          MVP-3,DPOY-8,AS,NBA1


[2 rows x 31 columns]


 2. Limpieza y estructuración de datos: 


DataFrame combinado:
              Jugador Pais  Edad     Deporte  Rank Market Value Equipo
0       Jannik Sinner  ITA  23.0       Tenis   NaN          NaN    NaN
1      Carlos Alcaraz  ESP  22.0       Tenis   NaN          NaN    NaN
2    Alexander Zverev  GER  28.0       Tenis   NaN          NaN    NaN
3        Taylor Fritz  USA  27.0       Tenis   NaN          NaN    NaN
4         Jack Draper  GBR  23.0       Tenis   NaN          NaN    NaN
..                ...  ...   ...         ...   ...          ...    ...
221     Derrick White  NaN  30.0  Básquetbol   NaN          NaN    BOS
222     Malik Beasley  NaN  28.0  Básquetbol   NaN          NaN    DET
223     Devin Vassell  NaN  24.0  Básquetbol   NaN          NaN    SAS
224   Jordan Clarkson  NaN  32.0  Básquetbol   NaN          NaN    UTA
225       Paul George  NaN  34.0  Básquetbol   NaN          NaN    PHI


[226 rows x 7 columns]


Valores nulos antes: Jugador           0
Pais            208
Edad              0
Deporte           0
Rank            121
Market Value    121
Equipo          126
dtype: int64


Valores nulos después: Jugador           0
Pais              0
Edad              0
Deporte           0
Rank            121
Market Value    121
Equipo          126
dtype: int64


 Valores duplicados antes: 6


 Valores duplicados después: 0


 df_unificado.info():
<class 'pandas.core.frame.DataFrame'>
Index: 206 entries, 0 to 225
Data columns (total 7 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   Jugador       206 non-null    object 
 1   Pais          206 non-null    object 
 2   Edad          206 non-null    float64
 3   Deporte       206 non-null    object 
 4   Rank          100 non-null    float64
 5   Market Value  100 non-null    object 
 6   Equipo        86 non-null     object 
dtypes: float64(2), object(5)
memory usage: 12.9+ KB
<class 'pandas.core.frame.DataFrame'>
Index: 206 entries, 0 to 225
Data columns (total 7 columns):
 #   Column        Non-Null Count  Dtype   
---  ------        --------------  -----   
 0   Jugador       206 non-null    string  
 1   Pais          206 non-null    string  
 2   Edad          206 non-null    float64 
 3   Deporte       206 non-null    category
 4   Rank          100 non-null    float64 
 5   Market Value  100 non-null    string  
 6   Equipo        86 non-null     string  
dtypes: category(1), float64(2), string(4)
memory usage: 11.6 KB


 3. Transformación y optimización de datos: 


DataFrame limpio:          Nombre Jugador  Edad Jugador Nombre Deporte
21         Lamine Yamal          18.0         Fútbol
47          Pau Cubarsí          18.0         Fútbol
81              Estêvão          18.0         Fútbol
96        Ethan Nwaneri          18.0         Fútbol
97   Warren Zaïre-Emery          19.0         Fútbol
..                  ...           ...            ...
166       DeMar DeRozan          35.0     Básquetbol
147       Stephen Curry          36.0     Básquetbol
134        Kevin Durant          36.0     Básquetbol
5        Novak Djokovic          38.0          Tenis
148        LeBron James          40.0     Básquetbol


[206 rows x 3 columns]


 4. Exportación de datos: 


 DataFrame limpio exportado a CSV y Excel: OK
```
En este trabajo aprendimos como mediante técnicas de ETL podemos acceder a datos de diversas fuentes con formatos heterogéneos mediante Python y unificarlos de una manera simple.

Además se demostró cómo el DataFrame de Pandas facilita la manipulación y consolidación de datos dispares en múltiples formatos y estructuración de datos de distintas fuentes como lo son archivos CSV, Excel incluso páginas web.

La actividad facilitó el desarrollo de habilidades clave en la recolección y procesamiento de datos heterogéneos mediante librerías de Python, abordando un caso realista que nos permite anticipar escenarios y desafíos comunes para un analista de datos.

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

### ANEXO 1: Código para generar archivos CSV y Excel

Archivo M3-L3-genera.py :
```Python
import pandas as pd
import requests
from bs4 import BeautifulSoup
import re

# Define User-Agent para simular navegador
headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"}

# ****************  FÚTBOL  ****************
# - Extrae top jugadores fútbol y guarda en Excel
futbol_players = []
for i in range(1, 5):
   url_page = f"https://www.transfermarkt.com/spieler-statistik/wertvollstespieler/marktwertetop/plus/0/galerie/0?page={i}"
   try:
       response_futbol = requests.get(url_page, headers=headers)
       soup = BeautifulSoup(response_futbol.content, 'html.parser')
       table_body = soup.find('div', class_='responsive-table').find('tbody')
       rows = table_body.find_all('tr', class_=['odd', 'even'])
       for row in rows:
           cols = row.find_all('td')
           if len(cols) > 1:
               rank = cols[0].text.strip()
               player_name = cols[1].find('img')['alt'].strip()
               age = cols[5].text.strip()
               market_value_element = cols[-1].find('a')  # Buscar el enlace en la última columna
               if market_value_element:
                   market_value = market_value_element.text.strip()
               else:
                   market_value = cols[-1].text.strip()
               futbol_players.append({
                   'Rank': rank,
                   'Jugador': player_name,
                   'Edad': age,
                   'Market Value': market_value,
                   'Deporte': 'Fútbol'
               })
   except requests.exceptions.RequestException as e:
       print(f"Error en la solicitud para la página {i}: {e}")
       continue
   except Exception as e:
       print(f"Ocurrió un error al procesar la página {i}: {e}")
       continue
if futbol_players:
   df_futbol = pd.DataFrame(futbol_players)
   # PARA PRUEBAS: duplica un 5% de los datos
   df_futbol = pd.concat([df_futbol, df_futbol.sample(frac=0.05, random_state=42)], ignore_index=True)
   # Guarda en Excel
   df_futbol.to_excel("M3/M3-L3-top_futbol.xlsx", index=False)

# ****************  TENIS  ****************

# - funcion obtiene edad jugador (requerimiento)
def extract_age(jugador_soup):
   try:
       infobox = jugador_soup.find('table', class_='infobox')
       if infobox:
           filas = infobox.find_all('tr')
           for fila in filas:
               th = fila.find('th')
               if th and 'born' in th.get_text().lower():
                   td = fila.find('td')
                   if td:
                       texto_born = td.get_text()
                       patron_edad = r'\(age\s+(\d+)\)'
                       match = re.search(patron_edad, texto_born)
                       if match:
                           return match.group(1)
   except:
       pass
   return "N/A"

# - Extrae top jugadores tenis y guarda en CSV
url = "https://en.wikipedia.org/wiki/Current_tennis_rankings"
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.content, 'html.parser')
tennis_players = []
tabla = soup.find('table', class_='wikitable')
if tabla:
   filas = tabla.find_all('tr')
   for fila in filas:
       celdas = fila.find_all('td')
       if len(celdas) >= 3:
           nombre_celda = celdas[1] if len(celdas) > 1 else celdas[0]
           nombre_link = nombre_celda.find('a')
           nombre_country = nombre_celda.find('abbr')
           if nombre_link:
               nombre = nombre_link.text.strip()
               country = nombre_country.text if nombre_country else "N/A"
               edad = "N/A"
               jugador_url = "https://en.wikipedia.org" + nombre_link['href']
               jugador_response = requests.get(jugador_url, headers=headers)
               jugador_soup = BeautifulSoup(jugador_response.content, 'html.parser')
               edad = extract_age(jugador_soup)
               tennis_players.append((nombre, country, edad, 'Tenis'))
if tennis_players:
   df_tenis = pd.DataFrame(tennis_players, columns=['Jugador', 'Pais', 'Edad', 'Deporte'])
   # PARA PRUEBAS: duplica un 5% de los datos
   df_tenis = pd.concat([df_tenis, df_tenis.sample(frac=0.05, random_state=42)], ignore_index=True)
   # Guarda en CSV
   df_tenis.to_csv("M3/M3-L3-top_tenis.csv", index=False)
```

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

### ANEXO 2: Fragmento de archivos generados

Archivo M3-L3-top_tenis.csv :
```bash
Jugador,Pais,Edad,Deporte
Jannik Sinner,ITA,23,Tenis
Carlos Alcaraz,ESP,22,Tenis
Alexander Zverev,GER,28,Tenis
Taylor Fritz,USA,27,Tenis
Jack Draper,GBR,23,Tenis
Novak Djokovic,SRB,38,Tenis
Ben Shelton,USA,22,Tenis
Alex de Minaur,AUS,26,Tenis
Holger Rune,DEN,22,Tenis
Lorenzo Musetti,ITA,23,Tenis
Andrey Rublev,N/A,27,Tenis
Frances Tiafoe,USA,27,Tenis
Casper Ruud,NOR,26,Tenis
Daniil Medvedev,N/A,29,Tenis
Tommy Paul,USA,28,Tenis
Karen Khachanov,N/A,29,Tenis
Flavio Cobolli,ITA,23,Tenis
Jakub Menšík,CZE,19,Tenis
Alejandro Davidovich Fokina,ESP,26,Tenis
Grigor Dimitrov,BUL,34,Tenis
Jannik Sinner,ITA,23,Tenis
```

Archivo M3-L3-top_futbol.xlsx :

```bash
Rank	Jugador	Edad	Market Value	Deporte
1	Lamine Yamal	18	€200.00m	Fútbol
2	Jude Bellingham	22	€180.00m	Fútbol
3	Erling Haaland	25	€180.00m	Fútbol
4	Kylian Mbappé	26	€180.00m	Fútbol
5	Vinicius Junior	25	€170.00m	Fútbol
6	Bukayo Saka	23	€150.00m	Fútbol
7	Pedri	22	€140.00m	Fútbol
8	Florian Wirtz	22	€140.00m	Fútbol
9	Jamal Musiala	22	€140.00m	Fútbol
10	Federico Valverde	27	€130.00m	Fútbol
…
…
96	João Pedro	23	€50.00m	Fútbol
97	Éderson	26	€50.00m	Fútbol
98	Micky van de Ven	24	€50.00m	Fútbol
99	Bremer	28	€50.00m	Fútbol
100	Pedro Neto	25	€50.00m	Fútbol
84	Eberechi Eze	27	€55.00m	Fútbol
54	Victor Osimhen	26	€70.00m	Fútbol
71	Sandro Tonali	25	€60.00m	Fútbol
46	Harry Kane	32	€75.00m	Fútbol
45	Nicolò Barella	28	€75.00m	Fútbol
```

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

## Análisis de caso - Data wrangling

El objetivo de esta actividad es realizar una simulación de un escenario real en el que debemos adoptar el rol de científico de datos encargado de optimizar la manipulación de datos. Con el objetivo de desarrollar una solución usando Pandas, garantizando eficiencia y eficacia.

Como científico de datos en la Fintech chilena Betterplan se nos encargó la tarea de optimizar la manipulación de datos y aplicar técnicas de Data Wrangling. 

Como origen contamos con un CSV* unificado con información de múltiples fuentes, el cual procesaremos con el código explicado a continuación:

(El archivo CSV se generó con Python: ver ANEXO 1 y 2)

Archivo M3-L5-wrangling.py :

```Python
import pandas as pd
import numpy as np

print(f"\n 1. Carga de datos desde distintos archivos: ")

# 1.a: Importa un dataset en formato CSV
df = pd.read_csv("M3/M3-L5-data.csv")

# 1.b: Inspecciona con head(), info() y describe()
print(f"\n head():\n{df.head()}")
print(f"\n df.info():")
df.info()
print(f"\n describe():\n{df.describe()}")

# 1.c: Identifica valores nulos y duplicados.
print(f"\n Valores nulos por columna:\n{df.isnull().sum()}")
print(f"\n Valores duplicados: {df.duplicated().sum()}")

print(f"\n 2. Limpieza y transformación de datos: ")

# 2.a: Imputa valores nulos utilizando estrategias adecuada
df['monto'] = df['monto'].fillna(0)  # imputa 0 para evitar error (auditar valores)
df['fuente_info'] = df['fuente_info'].fillna('N/A')
df['forma_pago'] = df['forma_pago'].fillna('N/A')

# 2.b: Elimina registros duplicados
df.drop_duplicates(inplace=True)

# 2.c: columnas categóricas (optimización columnas object)
df['tipo'] = df['tipo'].astype('category')
df['fuente_info'] = df['fuente_info'].astype('category')
df['forma_pago'] = df['forma_pago'].astype('category')
print(f"\n df.info():")
df.info()

# verificacion (AL FINAL DEL PASO 2):
print(f"\n Valores nulos por columna:\n{df.isnull().sum()}")
print(f"\n Valores duplicados: {df.duplicated().sum()}")

print(f"\n 3. Optimización y estructuración de datos: ")

# 3.a: Aplica funciones de groupby y agregación
# agrupación de usuarios con agregación de ingresos y egresos
resumen = df.groupby(['id_usuario']).agg(
   total_ingresos=('monto', lambda x: x[df['tipo'] == 'ingreso'].sum()),
   total_egresos=('monto', lambda x: x[df['tipo'] == 'egreso'].sum()),
   count=('monto', 'size')
).reset_index()
print(f"\n Resumen de datos:\n{resumen}")

# 3.b: Filtra los datos para obtener subconjuntos de interés.
# agrega columna con saldo
resumen['saldo'] = resumen['total_ingresos'] - resumen['total_egresos']
# agrega columna con % no gastado
resumen['porcentaje_no_gastado'] = (resumen['total_ingresos'] - resumen['total_egresos']) / resumen['total_ingresos'] * 100
# subconjuntos de interés: menor_gasto (porcentual)
top_menor_gasto = 70
# ordena por % no gastado
resumen.sort_values(by='porcentaje_no_gastado', ascending=False, inplace=True)
sub_menor_gasto = resumen[resumen['porcentaje_no_gastado'] > top_menor_gasto].head(10)
print(f"\n • 1° subconjuntos de interés: {len(sub_menor_gasto)} usuarios con +{top_menor_gasto}% no gastado \n{sub_menor_gasto}")

# subconjuntos de interés: mayor ahorro (neto)
top_mayor_saldo = 100000
# ordena por % no gastado
resumen.sort_values(by='saldo', ascending=False, inplace=True)
sub_mayor_saldo = resumen[resumen['saldo'] > top_mayor_saldo].head(10)
print(f"\n • 2° subconjuntos de interés: {len(sub_mayor_saldo)} usuarios con saldo > {top_mayor_saldo} \n{sub_mayor_saldo}")

# 3.c: Renombra y reorganiza columnas para mejorar la interpretación.
resumen.rename(columns={
   'id_usuario': 'ID Usuario',
   'total_ingresos': 'Total Ingresos',
   'total_egresos': 'Total Egresos',
   'count': 'Cantidad de Movimientos',
   'saldo': 'Saldo Neto',
   'porcentaje_no_gastado': '% No Gastado'
}, inplace=True)
#resumen = resumen[['ID Usuario', 'Total Ingresos', 'Total Egresos', 'Cantidad de Movimientos', 'Saldo Neto', '% No Gastado']]
print(f"\n Resumen de datos optimizado:\n{resumen}")

print(f"\n 4. Exportación de datos: ")

# 4. a y b: Exporta DataFrames de interés (menor gasto y mayor saldo)
# sub_menor_gasto
sub_menor_gasto.to_csv('M3/M3-L5-sub_menor_gasto.csv', index=False)
sub_menor_gasto.to_excel('M3/M3-L5-sub_menor_gasto.xlsx', index=False)
# sub_mayor_saldo
sub_mayor_saldo.to_csv('M3/M3-L5-sub_mayor_saldo.csv', index=False)
sub_mayor_saldo.to_excel('M3/M3-L5-sub_mayor_saldo.xlsx', index=False)
# resumen
resumen.to_csv('M3/M3-L5-resumen.csv', index=False)
resumen.to_excel('M3/M3-L5-resumen.xlsx', index=False)

print("DataFrames de interés y completo exportados con éxito.")
```
`$ python3 M3/M3-L5-wrangling.py`
```bash
 1. Carga de datos desde distintos archivos: 


 head():
        timestamp  id_usuario    tipo  monto fuente_info forma_pago
0  20250701000026         496  egreso  977.0       email   efectivo
1  20250701000313         246  egreso  645.0       email   efectivo
2  20250701000325         364  egreso  282.0       email   efectivo
3  20250701000332         511  egreso  602.0       email   efectivo
4  20250701000426          49  egreso  563.0         NaN        NaN


 df.info():
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 105000 entries, 0 to 104999
Data columns (total 6 columns):
 #   Column       Non-Null Count   Dtype  
---  ------       --------------   -----  
 0   timestamp    105000 non-null  int64  
 1   id_usuario   105000 non-null  int64  
 2   tipo         105000 non-null  object 
 3   monto        104895 non-null  float64
 4   fuente_info  94894 non-null   object 
 5   forma_pago   76909 non-null   object 
dtypes: float64(1), int64(2), object(3)
memory usage: 4.8+ MB


 describe():
          timestamp     id_usuario          monto
count  1.050000e+05  105000.000000  104895.000000
mean   2.025072e+13     501.323790    1031.220611
std    8.961673e+06     288.299984    2585.851985
min    2.025070e+13       1.000000      10.000000
25%    2.025071e+13     252.000000     271.000000
50%    2.025072e+13     502.000000     530.000000
75%    2.025072e+13     751.000000     793.000000
max    2.025073e+13    1000.000000   19998.000000


 Valores nulos por columna:
timestamp          0
id_usuario         0
tipo               0
monto            105
fuente_info    10106
forma_pago     28091
dtype: int64


 Valores duplicados: 5000


 2. Limpieza y transformación de datos: 


 df.info():
<class 'pandas.core.frame.DataFrame'>
Index: 100000 entries, 0 to 99999
Data columns (total 6 columns):
 #   Column       Non-Null Count   Dtype   
---  ------       --------------   -----   
 0   timestamp    100000 non-null  int64   
 1   id_usuario   100000 non-null  int64   
 2   tipo         100000 non-null  category
 3   monto        100000 non-null  float64 
 4   fuente_info  100000 non-null  category
 5   forma_pago   100000 non-null  category
dtypes: category(3), float64(1), int64(2)
memory usage: 3.3 MB


 Valores nulos por columna:
timestamp      0
id_usuario     0
tipo           0
monto          0
fuente_info    0
forma_pago     0
dtype: int64


 Valores duplicados: 0


 3. Optimización y estructuración de datos: 


 Resumen de datos:
     id_usuario  total_ingresos  total_egresos  count
0             1         75026.0        44270.0     93
1             2         64775.0        43411.0     96
2             3         63800.0        46416.0    102
3             4         51919.0        39100.0     83
4             5         33828.0        42083.0     98
..          ...             ...            ...    ...
995         996         47760.0        50514.0    103
996         997         36975.0        45862.0     99
997         998         29737.0        47232.0     92
998         999         53273.0        50063.0    112
999        1000         63054.0        43539.0     87


[1000 rows x 4 columns]


 • 1° subconjuntos de interés: 2 usuarios con +70% no gastado 
     id_usuario  total_ingresos  total_egresos  count     saldo  porcentaje_no_gastado
162         163        167536.0        39556.0     93  127980.0              76.389552
966         967        139514.0        39400.0     92  100114.0              71.759107


 • 2° subconjuntos de interés: 3 usuarios con saldo > 100000 
     id_usuario  total_ingresos  total_egresos  count     saldo  porcentaje_no_gastado
162         163        167536.0        39556.0     93  127980.0              76.389552
865         866        158649.0        49771.0    106  108878.0              68.628230
966         967        139514.0        39400.0     92  100114.0              71.759107


 Resumen de datos optimizado:
     ID Usuario  Total Ingresos  Total Egresos  Cantidad de Movimientos  Saldo Neto  % No Gastado
162         163        167536.0        39556.0                       93    127980.0     76.389552
865         866        158649.0        49771.0                      106    108878.0     68.628230
966         967        139514.0        39400.0                       92    100114.0     71.759107
488         489        143237.0        46250.0                      108     96987.0     67.710857
606         607        138484.0        42411.0                       97     96073.0     69.374801
..          ...             ...            ...                      ...         ...           ...
164         165          3698.0        54383.0                      103    -50685.0  -1370.605733
692         693          2374.0        54264.0                      106    -51890.0  -2185.762426
938         939          3770.0        55817.0                      100    -52047.0  -1380.557029
980         981             0.0        53389.0                       98    -53389.0          -inf
633         634          5517.0        59574.0                      115    -54057.0   -979.825992


[1000 rows x 6 columns]


 4. Exportación de datos: 
DataFrames de interés exportados con éxito.
```

Este trabajo nos permitió aprender técnicas y desarrollar habilidades de Data Wrangling utilizando las librerías Pandas y Numpy, para optimizar la obtención, limpieza, transformación y análisis de grandes volúmenes de datos financieros, demostrando la eficacia de estas herramientas en entornos reales.

Además, se evidenció la relevancia del Data Wrangling como proceso clave en la preparación de datos de calidad, el cual debe estar respaldado por un adecuado y diligente Gobierno de Datos, garantizando la integridad, seguridad y trazabilidad de la información para apoyar decisiones confiables y efectivas.

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

### ANEXO 1: Código para generar el CSV

Archivo M3-L5-genera.py :

```Python
import pandas as pd
import numpy as np
from datetime import datetime, timedelta

n_usuarios = 1000
n_filas = 100000
ing_min = 2000
ing_max = 20000
egr_min = 10
egr_max = 1000

ing_prob = 0.05  # probabilidad ingreso
egr_prob = 1 - ing_prob  # probabilidad egreso

np.random.seed(42)
movimientos = {
   'timestamp': [(datetime(2025, 7, 1) + timedelta(days=np.random.randint(0, 31))).strftime('%Y%m%d') + f"{np.random.randint(0, 24):02}{np.random.randint(0, 60):02}{np.random.randint(0, 60):02}" for _ in range(n_filas)],
   'id_usuario': np.random.randint(1, n_usuarios+1, n_filas),
   'tipo': np.random.choice(['ingreso', 'egreso'], n_filas, p=[ing_prob, egr_prob])
}
df = pd.DataFrame(movimientos)

# ordenar por 'timestamp'
df.sort_values(by='timestamp', inplace=True)

# monto: OK
df.loc[df['tipo'] == 'ingreso', 'monto'] = np.random.randint(ing_min, ing_max, (df['tipo'] == 'ingreso').sum())
df.loc[df['tipo'] == 'egreso', 'monto'] = np.random.randint(egr_min, egr_max, (df['tipo'] == 'egreso').sum())
# 0.1% de los datos de 'monto' debe ser NaN
df.loc[df.sample(frac=0.001).index, 'monto'] = np.nan

# fuente_info: OK
fuente_info_choices = ['email', 'manual', '']
df.loc[df['tipo'] == 'ingreso', 'fuente_info'] = 'email'
df.loc[df['tipo'] == 'egreso', 'fuente_info'] = np.random.choice(fuente_info_choices, (df['tipo'] == 'egreso').sum(), p=[0.7, 0.2, 0.1])

# forma_pago:
forma_pago_choices = ['efectivo', 'tarjeta', '']
df.loc[(df['fuente_info'] == 'email') & (df['tipo'] == 'ingreso'), 'forma_pago'] = 'transferencia'
df.loc[(df['fuente_info'] == 'email') & (df['tipo'] == 'egreso'), 'forma_pago'] = np.random.choice(forma_pago_choices, ((df['fuente_info'] == 'email') & (df['tipo'] == 'egreso')).sum(), p=[0.8, 0.0, 0.2])
df.loc[(df['fuente_info'] == 'manual'), 'forma_pago'] = np.random.choice(forma_pago_choices, (df['fuente_info'] == 'manual').sum(), p=[0.5, 0.3, 0.2])

# duplicar 5% de los datos
df_duplicados = df.sample(frac=0.05, random_state=42)
df = pd.concat([df, df_duplicados], ignore_index=True)

# Genera el CSV
df.to_csv('M3/M3-L5-data.csv', index=False)
print("CSV 'M3/M3-L5-data.csv' generado con éxito.")
```

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

### ANEXO 2: Fragmento del CSV generado

Archivo M3-L5-data.csv :

```bash
timestamp,id_usuario,tipo,monto,fuente_info,forma_pago
20250701000026,496,egreso,977.0,email,efectivo
20250701000313,246,egreso,645.0,email,efectivo
20250701000325,364,egreso,282.0,email,efectivo
20250701000332,511,egreso,602.0,email,efectivo
20250701000426,49,egreso,563.0,,
20250701000431,472,egreso,566.0,email,
20250701000432,514,egreso,620.0,email,efectivo
20250701000449,37,ingreso,3609.0,email,transferencia
20250701000512,97,egreso,641.0,manual,efectivo
20250701000514,242,egreso,223.0,,
20250701000550,867,egreso,283.0,email,efectivo
20250701000621,516,egreso,628.0,email,efectivo
20250701000628,491,egreso,505.0,manual,efectivo
20250701000629,57,egreso,86.0,email,efectivo
20250701000642,672,egreso,383.0,manual,tarjeta
20250701000740,243,egreso,185.0,email,
20250701000744,673,egreso,834.0,email,efectivo
20250701000748,963,egreso,502.0,email,
20250701000758,344,egreso,508.0,email,efectivo
20250701000814,752,egreso,728.0,,
20250701000843,127,egreso,814.0,,
20250701000854,148,egreso,735.0,,
20250701000905,579,egreso,944.0,email,efectivo
20250701000949,667,egreso,603.0,email,
…
20250712055559,165,egreso,780.0,email,
20250702005156,593,egreso,816.0,email,efectivo
20250707134024,758,egreso,111.0,manual,
20250728005415,899,egreso,261.0,email,efectivo
20250725131955,320,egreso,244.0,email,efectivo
20250724234755,853,egreso,892.0,manual,efectivo
20250710205001,375,egreso,913.0,email,efectivo
20250727090138,543,egreso,654.0,email,efectivo
20250729162555,812,egreso,590.0,email,efectivo
20250702210145,49,egreso,195.0,email,efectivo
20250722031513,731,egreso,138.0,email,efectivo
20250707024750,925,egreso,624.0,,
20250714172013,963,egreso,336.0,email,efectivo
20250721081210,668,egreso,504.0,email,efectivo
20250711190004,708,ingreso,19959.0,email,transferencia
20250713095401,347,egreso,436.0,email,
20250718203928,7,egreso,216.0,email,efectivo
20250715123716,307,ingreso,19088.0,email,transferencia
20250703153517,255,egreso,579.0,email,efectivo
20250711212252,350,egreso,751.0,email,efectivo
20250702080547,571,egreso,774.0,email,efectivo
20250714060451,592,egreso,930.0,,
20250713184549,911,egreso,938.0,manual,efectivo
20250703032617,979,egreso,221.0,email,
20250709103236,978,egreso,966.0,email,efectivo
20250704153223,496,egreso,87.0,manual,efectivo
20250714205346,398,egreso,55.0,manual,efectivo
20250707104019,936,egreso,459.0,email,efectivo
20250718174555,176,egreso,963.0,email,efectivo
20250708083858,376,egreso,794.0,email,efectivo
20250713214053,262,egreso,801.0,email,efectivo
```

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

## Evolución del Aprendizaje

Este módulo nos llevó desde una visión inicial del ciclo de vida de los datos hasta la aplicación concreta de técnicas de Data Wrangling con Pandas y NumPy. El recorrido fue:

- **Recolección**: Obtención de datos desde múltiples fuentes (CSV, Excel, Web)
- **Limpieza**: Identificación y tratamiento de valores nulos, duplicados e inconsistencias
- **Transformación**: Normalización, reordenamiento, cambio de estructuras y tipos
- **Análisis inicial**: Generación de estadísticas, agrupaciones y visualizaciones básicas

A lo largo del módulo, adquirimos un enfoque más técnico y riguroso sobre la importancia de preparar datos de calidad para análisis efectivos. Cada trabajo fue una oportunidad de aplicar estos conceptos con datasets reales y con sentido práctico.

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)

## Conclusiones

El **Módulo 3** nos permitió profundizar el ecosistema de Python para la manipulación de grandes volúmenes de datos mediante la aplicación de técnicas y herramientas poderosas que nos facilitan la labor. También gracias a las actividades prácticas aprendimos a usar librerías clave como NumPy, Pandas y BeautifulSoup para la extracción, limpieza y transformación de datos. La práctica de técnicas ETL y Data Wrangling en escenarios realistas nos brindó una comprensión profunda de cómo abordar los desafíos cotidianos en la manipulación de datos.

Además pudimos constrastar los roles de Analista de datos y Cientifico de datos, sumados al rol de Ingeniero de datos nos da los 3 principales roles para implementar la estrategia de datos de una organización, impulsada por una adecuada Gobernanza de Datos.

[Volver](#m3-obtenci%C3%B3n-y-preparaci%C3%B3n-de-datos)
