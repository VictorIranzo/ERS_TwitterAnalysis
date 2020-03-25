1. Utilizando el script 'twitterstream_edm_v3.py' se han obtenido los datos que luego se volcaban en un fichero. Por el uso de la versión de Python 3, de la lectura se obtenía un JSON en parte difícil de parsear (puede verlo en los ficheros 'inp.txt' y 'inpSpain.txt', donde se añade el carácter b' al principio de cada línea). Esto hace que se haya tenido que incluir código como el siguiente para leer correctamente el fichero:
	line = line.strip("'<>() ").replace('\'', '\"')
	line = line.replace("b\"{", "{")
	line = line.replace("}\"", "}")
	line = line.replace("\\\\", "\\")

2. Una vez volcada la salida del script a un fichero, se eliminaban los tweets que no interesaban para el análisis (por no contener la información que buscaba) y el resultado de la limpieza se ha ido añadiendo a los fichero 'inp.txt' y 'inpSpain.txt'. Esto ha permitido incrementar de manera iterativa el contenido útil repitiendo el paso 1. El código para la limpieza es similar al del análisis. Los métodos usados son: cleanNotUsefulTweets() y cleanNotUsefulTweetsSpain().

3. Se invoca al análisis, representado por las funciones analyzeUsa() y analyzeSpain(). Como resultado, al terminar se imprimen 2 diccionarios que se emplean para almacenar la información de interés. En el primero, la clave es el código del estado y como valor tiene una colección con el análisis de sentimientos de cada tweet en ese estado. En el segundo caso, la clave pertenece a un idioma y el valor es una colección con las coordenadas de cada tweet en ese idioma. Además, se generan dos ficheros CSV que se adjuntan: 'out.csv' y 'outSpain.csv'.

4. Los ficheros CSV tienen los elementos necesarios para la generación de sendos mapas. Ambos se han generado empleando el editor online de Vega Lite. Están basados en los siguientes ejemplos:
- https://vega.github.io/vega-lite/examples/geo_repeat.html (Se elimina la sección de repeat. Se han tenido que emplear unos identificadores que están almacenados en la variable states_codes)
- https://vega.github.io/vega-lite/examples/geo_layer.html (Se cambia el mapa de EEUU por el del mundo y se hace una proyección para mostrar España)

5. El editor online se encuentra disponible en https://vega.github.io/editor/#/custom/vega-lite. Lo único que hay que proporcionarle son los ficheros 'vegaEEUU.json' y 'vegaSpain.json'. Se ha intentado almacenar el HTML pero al recargar la página no iba correctamente. Estos JSON apuntan a los CSV localizados en el repositorio de GitHub. En su lugar, el resultado de los mapas generado se puede consultar también en los ficheros 'mapaEEUU.png' y 'mapaSpain.png'.