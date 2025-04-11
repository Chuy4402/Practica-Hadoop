# Practica-Hadoop
Ejemplos Hadoop
PRE REQUISITOS
Tener instalado docker Desktop

Levantar contenedor
ejecutar lo siguiente [docker-compuse up -d] verificamos si se están los contenedores ejecutándose [Docker PS] Para entrar en nuestro contedor usamos [docker exec -it namenode bash]

Estructura para carpetas de archivos de entrada
Entramos al nodo maestro [docker exec -it namenode bash] luego ejecutamos [hdfs dfs -1s /] Creamos la carpeta con [hdfs dfs -mkdir -p /user/root/] verificamos [hdfs dfs -1s /usuario/]

EJEMPLOS
CRÉDITOS https://gist.github.com/jsdario/6d6c69398cb0c73111e49f1218960f79#file-el_quijote-txt
Descargar un script de ejemplo MapReduce
https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-mapreduce-examples/2.7.1/ descargar [hadoop-mapreduce-examples-2.7.1-sources.jar ] Mover archivo [hadoop-mapreduce-examples-2.7.1-sources.jar] a la misma carpeta Docker-Hadoop. descargar y descomprimir [el_quijote.txt] a la misma carpeta Docker-Hadoop.

Copiar los archivos .jar y .txt al contenedor
usar estos comandos para los archvios [docker cp hadoop-mapreduce-examples-2.7.1-sources.jar namenode:/tmp] [docker cp el_quijote.txt namenode:/tmp ]

Crear carpeta de entrada a contenedor
[docker exec -it namenode bash] luego [ hdfs dfs -mkdir /usuario/raíz/input_contador]

copiar archivo txt
[CD /tmp] luego [hdfs dfs -put el_quijote.txt /user/root/input_contador] por último usar este comando [ hadoop jar hadoop-mapreduce-examples-2.7.1-sources.jar org.apache.hadoop.examples.WordCount input_contador output_contador] ver resuñtado [hdfs dfs -cat /usuario/raíz/output_contador/*] Comprovar [hdfs dfs -ls /usuario/raíz/output_contador]

guardar el contador
[ hdfs dfs -cat /user/root/output_contador/part-r-00000 > /tmp/quijote_wc.txt] luego [ Salir] y luego [docker cp namenode:/tmp/quijote_wc.txt .]

Resultado
El archivo quijote_wc.txt que se encuentra en la carpeta Docker-Hadoop.

Ejemplo de temperaturas
Descargar archivo y descomprima https://github.com/Rkrahul04/Maximum_Temp_Calculation_mapreduce/blob/master/Dataset%20-%20Calculate%20Maximum%20Temperature/Temperature mover el archivo [Temperature.txt] a la misma carpeta Docker-Hadoop.

Copiar los archivos .jar y .txt al contenedor
si ya tienes [hadoop-mapreduce-examples-2.7.1-sources.jar] salta ese paso el archivo [Temperature.txt] usar [docker cp Temperature.txt namenode:/tmp]

crea la carpeta de entrada dentro del contenedor
[docker exec -it namenode bash] [hdfs dfs -mkdir /usuario/raíz/input_temperaturas]

Ejecutar MapReduce
[ hadoop jar hadoop-mapreduce-examples-2.7.1-sources.jar org.apache.hadoop.examples.SecondarySort input_temperaturas output_temperaturas] Resultado [hdfs dfs -cat /usuario/raíz/output_temperaturas/*] comprobar [hdfs dfs -ls /usuario/raíz/output_temperaturas] Ejecutar [ hdfs dfs -cat /user/root/output_temperaturas/part-r-00000 > /tmp/temperaturas_ordenadas.txt] luego [exit] y luego [docker cp namenode:/tmp/temperaturas_ordenadas.txt .]

Ejemplo de Sudoku
Descargar un script de ejemplo MapReduce y el Archivo txt
[hadoop-examples-0.20.205.0.jar] y [puzzle1.dta]

Copiar los archivos .jar y .txt al contenedor
[docker cp hadoop-examples-0.20.205.0.jar namenode:/tmp ] y [docker cp puzzle1.dta namenode:/tmp ]

#Haga lo mismo para el archivo puzzle1.dta

docker cp puzzle1.dta namenode:/tmp 
#ngrese al contenedor namenode ejecutando 

docker exec -it namenode bash

Primero ejecute: 

cd /tmp 

Ejecutar

hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta

Lo anterior es una sola una línea de comando
El resultado es una entrada grande, pero si has realizado correctamente los pasos anteriores, todo debería estar bien.

#Ver los resultados
Ejecutar: 

hadoop jar hadoop-examples-0.20.205.0.jar sudoku puzzle1.dta > solucion_puzzle1.txt 

Después ejecutamos:

 exit

Por último: 

docker cp namenode:/tmp/solucion_puzzle1.txt .

Ahora el archivo de texto esta en la carpeta del  repositorio docker-hadoop.

Recuerde que el comando anterior lleva un punto al final

Ver los resultados
Abrir el archivo solucion_puzzle1.txt que se encuentra en la carpeta del  repositorio docker-hadoop.

Referencia
https://hadoop.apache.org/docs/stable/api/org/apache/hadoop/examples/dancing/package-summary.html


