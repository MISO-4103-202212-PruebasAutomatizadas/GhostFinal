# MISO - Pruebas automatizadas

**Entrega final**

## Integrantes

- Ronald Lugo <r.lugoq@uniandes.edu.co>
- Juan Sebastian Ballesteros <j.ballesterosm@uniandes.edu.co>
- Rafael Brache <r.brache@uniandes.edu.co>
- Edinson Morales <e.moralesm2@uniandes.edu.co>

## Links
- [Informe de la estrategia:](https://uniandes-my.sharepoint.com/:w:/g/personal/r_lugoq_uniandes_edu_co/EZiJeKyCT-dAhdCjxl7435kBgaRVbya9YeLZaBM7DEpbpQ?e=SBaSdU)
  - Estrategia
  - Links
  - Pros y contra de herramientas
- [Inventario de pruebas exploratorias:](https://uniandes-my.sharepoint.com/:x:/g/personal/r_lugoq_uniandes_edu_co/ERcV_aRmEQVHnL8zSLFe1H4BpT2uUE-xgY0Y97Mn7zJgTA?e=zLedDO)
- [Registro de incidencias:](https://github.com/MISO-4103-202212-PruebasAutomatizadas/Ghost/issues)
- [Video:](https://uniandes-my.sharepoint.com/:f:/g/personal/r_lugoq_uniandes_edu_co/EpczswqO9WhJpb5l22L-hzABlKqu-02uoTHoO19r0bjt9w)

### Escenarios
| Funcionalidad | Escenario                                            |
|---------------|------------------------------------------------------| 
| Post          | Creación y publicación inmediata de Post exitosa  |
| Post          | Creación y publicación programada de Post exitosa | 
| Post          | Despublicar un post de manera exitosa                |
| Post          | Asignar tag a Post y publicar actualización          |
| Post          | Eliminar Post satisfactoriamente                     |
| Tag           | Creación de un tag exitoso                           |
| Tag           | Encontrar de un tag creado                           |
| Tag           | Actualizacion de un tag exitosa                      |
| Tag           | Eliminacion de un tag exitoso                        |
| Page          | Creación y publicación inmediata de Page exitosa     |
| Page          | Creación y publicación programada de Page exitosa    |
| Page          | Despublicar un page de manera exitosa                |
| Page          | Asignar tag a Page y publicar actualización          |
| Page          | Eliminar Page satisfactoriamente                     |
| Member        | Creación de un miembro exitoso                       |
| Member        | Encontrar el miembro creado                          |
| Member        | Eliminacion de un member exitoso                     |
| Member        | Buscar un miembro creado                             |

### Herramientas
- `node: v16.15.0`
- `npm: 8.5.5` 
- `playwright: 1.22.2`
- `resemblejs: 4.1.0`
- `http-server: 14.1.0`
- `kraken-node: 1.0.24`

## TNT - Sistema / Caja negra / Automatizada / Regresión visual 
*En la primera semana se genera las imágenes de referencia para comparar en las siguientes iteraciones*

### Configuraciones
1. configurar en archivo properties.json con datos de pruebas:
		- url: url de ghost
    - urlAdmin: url de ghost admin
    - pathReports: "./reports/tests/" -> path de exportación de screenshots en cada prueba
    - userAdmin: user admin en ghost
    - adminPass: password admin en ghost

2. .\resemblejs\config.json
	- referencePath: ../report/reference/  -> *path imágenes Ghost de referencia*
  - testPath: ../report/tests/  -> *path imágenes Ghost de prueba*
  - resultsPath: ../report/results/  -> *path resultados de resemblejs*
  - reportJsonName: results.json  -> *nombre del archivo json generado por resemblejs*
  - optionsCompare:  -> *opciones de configuración de la comparación*
    - output: 
      - errorColor: 
        - red: 255
        - green: 0
        - blue: 255
      - errorType: movement
      - largeImageThreshold: 1200
      - useCrossOrigin: false
      - outputDiff: true
  - scaleToSameSize: true  -> *comparación de imágenes en la misma escala*
  - ignore: "antialiasing  


### Ejecución de pruebas de regresión visual

1. abrir terminal bash
  - En visual studio code / menú superior / Terminal / New terminal / 
  - En ventana de terminal / menú superior derecho / flecha abajo / Git Bash
2. ubicarse en directorio de trabajo
  - `cd pruebas-de-regresion`
3. instalar dependencias
  - `npm install`
4. ejecutar pruebas
  - `node index.js && node index_tags.js && node index_page.js && node index_members.js`
5. aprobar imágenes como referencia (se recomienda ejecutar la primera vez que se ejecute el test, y cada vez que se desee generar imágenes de referencia a partir del último test ejecutado)
  - `npm run approve`
6. ejecutar pruebas de regresión con resemblejs
	- `cd .\resemblejs\`
	- `node .\index.js`
7. verificar generación de resultados
	- `path: ..\reports\results\`  -> *verificar creación de imágenes y results.json*
8. iniciar servidor web local para consultar reporte
	- `cd pruebasDeRegresion\`
	-	`node .\node_modules\http-server\bin\http-server`
	- `ir a http://127.0.0.1:8080/reports/`  -> *confirmar que el puerto que inició el servidor sea el 8080*

## TNT - Aceptación / Funcionales / Automatizada / E2E
### Configuraciones
- `cd .\pruebas-e2e`
- `npm install`

1. properties.json: es necesario actualizar ADMIN1 y PASSWORD1
	- ADMIN1: usuario de ghost local 
	- PASSWORD1: password de ghost local 
	- POSTTITLE: titulo post de prueba 
	- POSTDESC: descripción de post de prueba 
	- MINUTESADDPUBLISHPOST: minutos a futuro para programar la publicación de un post 
	- TAGTEST1: tag de prueba 
	- <PAGETITLE> : titulo page de prueba
	- <PAGEDESC> : Conetido de page de prueba
2. page_objects: en caso que ghost local tenga una url diferente a `http://localhost:2368`, se debe actualizar en los siguientes page_objects
	- dashboard.page.js
	- login.page.js
	- page.js
	- post_edit.page.js
	- post.page.js
	- tag_edit.page.js
	- tags.page.js
	- page.page.js
	- page_edit.page.js

### Ejecución de pruebas E2E
1. abrir terminal bash
  - En visual studio code / menú superior / Terminal / New terminal / 
  - En ventana de terminal / menú superior derecho / flecha abajo / Git Bash
2. ubicarse en directorio de trabajo
  - `cd pruebas-e2e`
3. instalar dependencias
  - `npm install`
4. ejecutar pruebas
  - `node ./node_modules/kraken-node/bin/kraken-node run`
5. verificar generación de resultados
	- `path: ..\reports\screenshots\`  -> *verificar creación de imágenes*
