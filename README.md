# sigua-modal
Utilidades y ejemplos para visualizar cartografía de Sigua en una ventana modal de Bootstrap 3

Esta utilidad permite utilizar en Internet la cartografía de SIGUA (http://www.sigua.ua.es) utilizando el framework Bootstrap de Twitter. Está diseñado para la versión 3 de Bootstrap

Su funcionamiento es muy sencillo y permite navegar por el mapa de forma continua, pudiendo además obtener información puntual sobre las estancias, con estos datos:
> - Actividad
> - Departamento
> - Denominación
> - Superficie
> - Ocupantes
> - Enlaces a redes sociales (Twitter, Facebook, G+)
> - Enlaces a visores cartográficos web (OpenStreetMap y GMaps)

Para navegar entre las diferentes plantas se utiliza un **control de plantas** que permite cambiar de una planta a otra

----------


Información
-------------

La cartografía se visualiza en una ventana modal cuyo tamaño es persolizable mediante CSS 
```
#map { min-height: 350px;}
```
Este  visor utiliza tres  librerías Javascript que pueden referirse de forma local (directorio **assets**) o remota:
> - **LeafletJS**: Pequeña pero potente utilidad para visualizar cartografía en la web
> - **Jquery**: Framework de sobra conocido para facilitar el uso de Javascript
> **Bootstrap:**Framework creado por Twitter para crear interfaces web con CSS. La versión utilizada es la 3.X

Aparte de dichas librerías, encontramos dos ficheros javascript que contienen la funcionalidad de Sigua (también en **assets/js**:
> - **sigua_capas.js**: Contiene la articulación de las capas cartográficas utilizadas.
> - **sigua_main_basico[1/2/3].js**: Contiene la funcionalidad de información, cambio de capas y demás funciones. Hay 3, uno para cada ejemplo.
Opcionalmente se utiliza **Font Awesome** para dibujar iconos

La información de carácter puntual es obtenida utilizando el API RestFul de Sigua: http://web.ua.es/es/sigua/api-rest.html

Para crear un modal de Sigua utiliza esta plantilla
```
<div class="modal" id="miMapaModal" tabindex="-1" role="dialog" aria-labelledby="miMapaModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-hidden="true">×</button> 
                <h4 class="modal-title">Título</h4>
            </div>
            <div class="modal-body" id="map"></div>
            <div class="modal-footer">
            	<div class="btn-group hide" data-toggle="buttons" id="plantas">
						<span class="badge">Plantas</span>
							<label class="btn btn-default btn-xs active"> <input type="radio" name="planta" id="PB" value="PB" checked="true"> PB  </label>
							<label class="btn btn-default btn-xs"> <input type="radio" name="planta" id="P1" value="P1"> P1  </label>
							<label class="btn btn-default btn-xs"> <input type="radio" name="planta" id="P2" value="P2"> P2  </label>
							<label class="btn btn-default btn-xs"> <input type="radio" name="planta" id="P3" value="P3"> P3  </label>
							<label class="btn btn-default btn-xs"> <input type="radio" name="planta" id="P4" value="P4"> P4  </label>
							<label class="btn btn-default btn-xs"> <input type="radio" name="planta" id="PS" value="PS"> PS  </label>
					</div>	              
        </div>            
      </div>
    </div>
 </div>
```

Zooms predefinidos
-------------
Con el objeto de facilitar al desarrollador el acceso rápido a un espacio concreto hemos definido una propiedad en el botón de inicio, llamada **data-value**, que permite indicar la vista inicial que se mostrará en el mapa. Permite 4 opciones de zoom.

> - **Zoom a una estancia**: El valor de data-value debe de ser el código completo de una estancia, con sus 9 caracteres. Ej: (data-value="0037P1013")
> - **Zoom a un edificio y una planta determinada**:  El valor de data-value debe de ser los 6 primeros caracteres de una estancias. Ej: (data-value="0007P2")
> - **Zoom a un edificio**:  El valor de data-value debe de ser los 4 primeros caracteres de una estancias. Ej: (data-value="0007")
> - **Vista general de la UA**:  El valor de data-value debe de estar vacio (data-value="")

Ejemplo de zoom a una estancia
```
<a href="#miMapaModal" id="elCodigo" data-value="0037PB016" role="button" class="btn btn-primary" data-toggle="modal">Abrir Mapa en 0037PB016</a>
```

Personalización
-------------
Sí quieres extender la funcionalidad cuando se selecciona una estancia en el popup (info), aparece información de la estancias y un botón, ** Seleccionar estancia**, que llama a una función llamada **showCodigo** que recibe como variable el código de estancia. Puedes utilizarlo para incorporarlo a  tu website. E
```
function showCodigo( codigo ) {
	alert("Hola, has seleccionado la estancia con codigo " + codigo );
} 
```


Ejemplos
-------------
Hemos realizado cuatro ejemplos con diferentes funcionalidades:


> - **index_basico1.html**: Es el modal más básico, con el mapa de la UA y la posibilidad de cambiar de planta. También puede obtener información de las estancias
> - **index_basico2.html**: Las mismas prestaciones que el anterior,  pero se dispone de un control de formulario tipo SELECT para obtener el listado de edificios. Cuando se selecciona uno se hace un zoom a su totalidad
> - **index_basico3.html:**: Al igual que el anterior, pero en este caso los edificios aparecen en un sidebar lateral
> - **index_codigo.html:**: Al igual que el primero, pero en este caso la vista se centra en una estancia que se pasa como parámetro en el botton

