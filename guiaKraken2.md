# Construccion de base de datos para Kraken2 (Tesis)

## Overview

En esta guia nos basaremos en el trabajo de Ottoni et al. (2021) y Fellows et al. (2021) para conocer los pasos a realizar para construir una base de datos personalizada en el programa Kraken2.


## Pasos a seguir

1. Primero hay que descargar los metadatos de interés, en este caso utilizaremos genomas completos de bacterias, arqueas, plantas, animales, hongos, cloroplastos, y virus. Usaremos la base de datos de genomas RefSeq que se actualizó el 13 de septiembre de 2021.

        DBNAME=customkraken2_Sep2021
        DBSIZE=<tamaño de base de datos en bytes>
        THREADS=<número de hilos de procesamientos que se requieren>
        kraken2-build --download-taxonomy --threads $THREADS        --db $DBNAME
        kraken2-build --download-library bacteria --threads         $THREADS --db $DBNAME
        kraken2-build --download-library viral --threads        $THREADS --db $DBNAME
        kraken2-build --download-library archaea --threads        $THREADS --db $DBNAME
        kraken2-build --download-library fungi --threads        $THREADS --db $DBNAME
        kraken2-build --download-library animals --threads        $THREADS --db $DBNAME
        kraken2-build --download-library plants --threads       $THREADS --db $DBNAME 
        kraken2-build --build --threads $THREADS --db $DBNAME       --max-db-size $DBSIZE 
### Clasificación taxonómica de las lecturas con la base de datos personalizada en Kraken2

2. La base de datos personalizada se utilizará para realizar la clasificación taxonómica de las lecturas previamente procesadas

        kraken2 --db $DBNAME --threads $THREADS filename.collapsed.gz --output filename.krk --gzip-compressed --report filename.krk.report



