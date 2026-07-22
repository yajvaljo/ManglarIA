# Repositorio para proyecto manglar IA
## Tema línea de costa y variables climáticas

### Objetivo:
Generar datos para caracterizar la dinámica de la línea de costa y variables climáticas (temperatura de la superficie del océano, dirección del viento, altura de olas, índice multivariado ENSO-MEI.v2 de la NOAA, entre otras) en las áreas de interés mediante el uso de datos satelitales Landsat. (Reserva de la Biosfera Marismas Nacionales, Nayarit -RBMNN- y Reserva de la Biosfera Ría Lagartos -RBRL-)

### Métodos:

![Diagrama Modelado](DiagramaLineaCosta_MDC.svg)

+ Se generaron series de tiempo sobre transectos equidistantes en su origen cada 100 m, a partir de datos de las colecciones Landsat 5, 7, 8 y 9, de las variaciones en la posición de la línea de costa entre el 01/01/1995 y el 16/05/2026 utilizando las herramientas desarrolladas por Vos, et al 2019 (https://github.com/kvos/CoastSat.git). Para cubrir la línea de costa de los sitios de estudio, el análisis se llevó a cabo sobre secciones de menos de 100 km<sup>2</sup>, seis para la RBMNN y ocho para la RBRL.
+ Las series de tiempo se guardaron como archivos csv en cada folder correspondiente a cada sección (https://drive.google.com/open?id=19Q-8HNnPpkFknKTVcnUGPsBpboWE8rSU&usp=drive_fs). Estos archivos cuyas hileras son fechas y cuyas columnas representan cada transecto, es utilizado en el script llamado [extract_era5_data](extract_era5_data.ipynb) junto con un archivo geojson que define el área de la sección, para extraer los promedios trimestrales de variables ambientales y climáticas de la colección ERA5 en Google Earth Engine ("ECMWF/ERA5/HOURLY") y estimaciones de la anomalía en el nivel medio del mar reportado por Copernicus Marine Service (https://data.marine.copernicus.eu/product/SEALEVEL_GLO_PHY_L4_MY_008_047/services) en su producto: "cmems_obs-sl_glo_phy-ssh_my_allsat-l4-duacs-0.125deg_P1D" para añadirlas a cada hilera de fecha en el archivo csv.
+ Para establecer la influencia de las variables ambientales en la dinámica mostrada por la línea de costa, el archivo con los datos de series de tiempo y datos ambientales y climáticos integrados se emplea en un tercer script llamado [coastal_dynamic_modeling](coastal_dynamic_modeling.ipynb), donde haciendo uso de un modelo autorregresivo de retardo distribuido, se explora su influencia en la dinámica de la linea de costa representada con funciones empíricas ortogonales.

