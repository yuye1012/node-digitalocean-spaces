# Compilación de los proyectos

(Nota: En la carpeta 'target' de cada proyecto ya está compilado el fichero '.jar' para cada ejercicio, se puede recompilarlos)

- Cada proyecto puede ser recompilado tanto por el comando 'mvn package' en el directorio raíz del proyecto correspondiente, como a través del entorno Eclipse.

- Una vez compilado el proyecto correctamente, se generará un fichero '.jar' en la carpeta 'target' que podrá ser ejecutado posteriormente.





# Ejercicio 1

- Para poder ejecutar el ejercicio 1 hay que tener el fichero 'cite75_99.txt' disponible en el sistema de fichero HDFS (Hadoop), por lo tanto, subimos este fichero desde el local al directorio '/user/hdadmin' dentro del sistema de fichero HDFS con el siguiente comando:
```
$ hdfs dfs -copyFromLocal patentes-mini/cite75_99.txt /user/hdadmin
```
- Una vez teniendo el fichero disponible, se ejecutaría el programa (fichero .jar) en el Hadoop con el siguiente comando:
```
$ yarn jar citingpatents-0.0.1-SNAPSHOT.jar /user/hdadmin/cite75_99.txt ejercicio1
```
- Cuando se termina la ejecución, se puede ver el resultado (que son varios ficheros repartidos dentro del directorio 'ejercicio1' indicado en el comando de la ejecución) a través del comando:
```
$ hdfs dfs -text /user/hdadmin/ejercicio1/*
```




# Ejercicio 2

- Como el ejercicio 2 se va a utilizar la salida del ejercicio 1, dejamos el fichero 'citingpatents-0.0.1-SNAPSHOT.jar' generado en el ejercicio 1 al directorio 'src/resources' de este ejercicio, y realizamos el mismo proceso explicado en la compilación de los proyectos para generar el fichero '.jar' del ejercicio2.

- Ejecutamos los siguientes comandos para configurar la variable del entorno (para usar el 'jar' del ejercicio 1) y ejecutar el programa indicando el directorio de salida como 'ejercicio2':
```
$ export HADOOP_CLASSPATH="./citingpatents-0.0.1-SNAPSHOT.jar"
$ yarn jar citationnumberbypatent_chained-0.0.1-SNAPSHOT.jar -libjars $HADOOP_CLASSPATH /user/hdadmin/cite75_99.txt ejercicio2
```
- Al igual que antes, para ver el resultado de la ejecución utilizamos el siguiente comando:
```
$ hdfs dfs -text /user/hdadmin/ejercicio2/*
```




# Ejercicio 3

- Para el reemplazo del código de cada país por el nombre correspondiente, el programa utilizará el fichero 'country_codes.txt', el cual debe estar disponible en el disco local (no en el HDFS).

- Para ejecutar el programa, usamos el comando similar al anterior, indicando también los ficheros txt que van a ser usado con la opción '-files' (country_codes.txt en local y apat63_99.txt en HDFS), cuya salida sería el directorio ejercicio 3:
```
$ yarn jar creasequencefile-0.0.1-SNAPSHOT.jar -files patentes-mini/country_codes.txt /user/hdadmin/apat63_99.txt ejercicio3
```
- Para ver los resultados:
```
$ hdfs dfs -text /user/hdadmin/ejercicio3/*
```




# Ejercicio 4

- En el ejercicio 4 se va a utilizar la salida del ejercicio 3, por lo tanto, indicamos tanto la ruta del dicho fichero en el HDFS, como la salida, ejecutando el comando:
```
$ yarn jar sortsecundario-0.0.1-SNAPSHOT.jar /user/hdadmin/ejercicio3/part-m-00000 ejercicio4
```
- Y al igual que antes, para ver el resultado:
```
$ hdfs dfs -text /user/hdadmin/ejercicio4/*
```





