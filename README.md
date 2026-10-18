# 📊 Modelamiento Estadístico de Precipitaciones en Ibagué

![R](https://img.shields.io/badge/Language-R-blue.svg)
![Environment](https://img.shields.io/badge/Environment-Google%20Colab-orange.svg)
![Platform](https://img.shields.io/badge/Platform-GitHub-black.svg)

En este proyecto se busca hacer un análisis exploratorio y modelamiento de series de tiempo de los datos de precipitación histórica registrados en la estación meteorológica del Aeropuerto Perales (Ibagué, Tolima) desde 2000 - 2026. El proyecto busca identificar patrones estacionales, tendencias climáticas y comportamientos anómalos en las lluvias de la región utilizando R y herramientas estadísticas, con el fin de demostrar algunos fenomenos climaticas(sequias) en análisis de datos geoespaciales y meteorológicos para aplicaciones reales.

---

## 📋 Tabla de Contenidos
- Descripción del Proyecto
- Objetivos del Análisis
- Fases Del proyecto
- Tecnologías y Librerías
- Cómo Ejecutar el Notebook
- Resultados y Tablas Generadas
- Conclusiones
- Contacto

---

## 🌌 Descripción del Proyecto


Este proyecto hace un analisis estadistico estructurado sobre pruebas analiticas y observaciones en graficos utilizando el lenguaje **R** dentro del entorno de **Google Colab**. El flujo de trabajo está diseñado de manera secuencial para procesar los datos de entrada, aplicar transformaciones y modelos sobre los datos usando ARIMA despues estructurar los resultados finales en tablas consolidadas que facilitan la interpretación de la información.

---

## 🎯 Objetivos del Análisis

* **Limpieza y Estructuración:** Se busca hacer un extraccion de datos en la tabla para poder trabajabar sobre los datos historicos. 

* **Análisis Exploratorio:** En este momento el proyecto busca observar graficos y aplicar pruebas de hipotesis para dar conclusiones acertadas sobre las propiedades de los datos 

* **Construcción de Tablas Resumen:** al final se busca entregar dos tablas una con la prediccion del aa;o actual en este caso el 2026 y otra tabla del 2027 con los datos mes a mes de la precipitacion

---

## 🌑 Fases del proyecto

* 1.**En la primera** fase de los datos lo que hacemos es observar si tienen alguna tendencia de normalidad o estacionalidad ademas de calcular su media y sd.

con esto ya hecho buscamos transformar primero con la funcion ts() y ya luego usando la transformacion de box-cox, teniendo en cuenta que no no garantiza normalidad la transformacion pero nos ayuda a regularisar una media y sd mas manejable ademas de ayudarnos a trabajar con unos datos mas estructurados, realizamos algunas pruebas muy importantes sobre estos datos como graficos, qqnorm,acf,pacf de lo que concluimos que la transformacion de los datos no nos da una normalidad pero si una mejora en la media y sd aparte en sus graficos de correlacion se observa una estacionalidad mas marcada por lo que aplicamos una prueba de hipotesis ADF(),KPSS()

* **Prueba ADF:** La hipótesis nula ($H_0$) es que la serie **no es estacionaria** (tiene una raíz unitaria). Si el **p-valor < 0.05**, rechazamos $H_0$ y concluimos que **sí es estacionaria**.

* **Prueba KPSS:** La hipótesis nula ($H_0$) es que la serie **es estacionaria**. Si el **p-valor < 0.05**, rechazamos $H_0$ y concluimos que **no es estacionaria**.

De esta prueba tenemos un p-value = 0.01 para ambos casos por lo que concluimos que los datos tienen estacionalidad

* 2. **En la segunda** fase con la estacionalidad de nuestros datos analizamos una serie de modelos ARMA(p,q) , ARIMA(p,d,q) , SARIMA(p,0,q).

De estos modelos y usando la estacionalidad concluimos que manejamos 0 grados de diferencias por lo que descartamos usar un arima con un d > 0. usando la libreria de forecast y Arima generamos 16 modelos que hacen prediccion sobre diferentes condiciones como 
* $p$ (Autorregresivo - AR): Cuántos retardos (lags) pasados de la propia serie se usan para predecir el valor actual.

* $q$ (Medias Móviles - MA): Cuántos errores pasados (shocks aleatorios) se usan en el modelo.

Ademas de probar diferentes condiciones en su estacionalidad aun que siempre gana una estacionalidad c(0,0,0) 

Despues de este calculo de modelos vamos a evaluar cual es el que mejor resultados da esto lo hacemos en una tabla de AIC,BIC donde el MODELO GANADOR ES **ARIMA13(2,0,2)**, seleccionamos este modelo ya que con la funcion del forecast() nos dice que el mejor modelo es arima11 pero solo esta evaluando alrededor de 11 modelos mientras que nosotros estamos evaluando 16 modelos donde conseguimos uno mejor que el estimado por auto.arima()


* 3.**En la tercera** Fase se estudia el ruido donde lo mas importante es la prueba de shapiro-willks la cual arroja un p-value < 0.05 por esto no quiere decir que los residuos sean no normales lo que sucede es que por el tama;o de la muestra tan grande se calcula mal la estimacion del p-value aun que con el teorema del limite central podemos ajustar esto y conseguir la normalidad por otra parte cuando analizamos el hist,acf,qqnorm conseguimos que si es normal

* 4.**En la cuarta** Fase ya con el modelo arima13 elegido y analizado procedemos aplicar una transformacion inversa de box-cox para dar resultados estos analisis de estos resultados los damos al final del archivo en las conclusiones luego de esto generamos dos tablas 2026,2027 las cuales contienen las predicciones de los dos siguentes a;os mes a mes podemos estimar dos a;os gracias a la naturaleza con la que fue seleccionado el modelo arima13 a su p = 2 y q = 2 tienen buenos registrados pasados para estimar una peque;a distancia en el futuro.

* Con todo lo anterior podemos decir que el proyecto fue un exito ademas de poder modelas bastante bien la precipitacion en ibague podemos sacar algunas conclusiones sobre fenomenos climatologicos aparte se buscara automatizar para que lo apliques a una base de datos con los datos de tu region. muchas gracias si leiste todo <3

---

## 🛠️ Tecnologías y Librerías

* **Lenguaje:** R
* **Entorno:** Google Colab (Kernel de R)
* **Control de Versiones:** Git & GitHub
* **Librerías Principales de R:**
  * `dplyr` ` (Manipulación y transformación de datos)
  * `ggplot2` (Visualización gráfica y exploración de datos)
  * `forecast` (Modelamiento de series de tiempo y pronósticos)
  * `readxl` (Lectura e importación de archivos de Excel)
  * `tseries` (Pruebas de estacionariedad y análisis estadístico de series de tiempo)

---


## 🌆 Como Ejecutar el Notebook

Solamente clona el repositorio y abrelo desde google-colab en el ambiente cambia tipo de entorno y pones R luego instalas todas las librerias y en la carpeta de la izquierda subes tu excel con los datos y le das al 
CTRL + F9 y se ejecutara todo el cuaderno estara en proceso el hecho de que te genere un archivo ya con todos los graficos y no lo tengas que ir a leer.

---

## 🧾Resultados y Tablas generadas

---

## 💧Conclusiones y Observaciones en el clima

* **Estacional en ibague**: Las pruebas de hipótesis (ADF y KPSS) y las funciones de autocorrelación confirmaron una componente estacional anual (período de 12 meses) donde en la primera parte de los 12 meses se ve un pico de menos lluvias y un aumento de lluvias al pasar la primera parte del año aun que nose marca esa estacionalidad estricta ya que puede variar segundo los datos historicos a un poco mas de medio año y menos lluvias .

* **Modelo Óptimo**: (ARIMA(2,0,2)): Tras evaluar 16 combinaciones alternativas superando las limitaciones de un análisis automatizado convencional, el modelo seleccionado demostró el mejor balance en métricas de error y criterios de información (AIC/BIC) para capturar la persistencia de las precipitaciones.

* **Validación de Residuos**: Aunque la prueba de Shapiro-Wilk mostró sensibilidad ante el gran tamaño muestral, el análisis gráfico conjunto (histograma, Q-Q plot y ACF de los residuos) respaldó la hipótesis de normalidad complementada por el Teorema del Límite Central.

* **Fenomenos en el modelo**: Al comparar las proyecciones del 2026 con los datos reales, notamos una desviación importante en los últimos meses. Esto tiene una explicación clara: la intensa sequía y los incendios que afectaron al Tolima recientemente. Como nuestro modelo se alimenta de datos históricos (2000–2026), una anomalía de esta magnitud no tenía precedentes en la serie. Lejos de ser un error del modelo, esto demuestra lo atípico del fenómeno. Con este aprendizaje, el análisis nos deja bases muy valiosas para entender el comportamiento climático y prepararnos mejor ante futuros eventos extremos de cara al 2027

---

## 📞Contacto 

### Nicolas Bernal

### Matematico Con Enfasis En Estadistica 

i'm learning english for comunicate more, i understand a bit, sorry

[![Email](https://img.shields.io/badge/Email-nicolasbernalhrr%40gmail.com-red?style=flat&logo=gmail)](mailto:nicolasbernalhrr@gmail.com)


[![GitHub](https://img.shields.io/badge/GitHub-TuUsuario-black?style=flat&logo=github)](https://github.com/Nicolas-Bernal)
