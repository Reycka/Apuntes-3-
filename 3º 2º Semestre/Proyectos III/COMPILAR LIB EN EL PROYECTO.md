CAMBIAR EL RESULTADO DE LA COMPILACIÓN DE .EXE(por defecto) a DLL
- 1º Entras en configuraciones del proyecto
- 2º En la sección de general de la parte de propiedades de configuración buscamos "Tipo de configuración" (El 4º desde arriba)
- 3º En ese apartado seleccionamos lib clickando el desplegable y buscando la opción

**IMPORTANTE ANTES DE COMPILAR:**
- Eliminar el método main ya que las librerías estáticas no tienen de esto y no se podrá ejecutar la compilación

COMPILACIÓN:
- En modo **RELEASE** compilas haciendo click derecho en tu proyecto, compilar
- Para borrar la  el .idb:
	- Estos son archivos de debug (depuracion que usa visual) basicamente permiten depurar la librería desde cualquier módulo que la tenga PARECE CHACHI PERO NOSOTROS QUEREMOS QUE LOS MÓDULOS SEAN CAJAS NEGRAS PARA EL USUARIO ASI QUE HAY QUE QUITARLAS DEL CAMINO
	- Propiedades del proyecto -->C/C++ --> Archivos de salida --> Nombre del archivo de base de datos del programa y escribimos la ruta de la carpeta tmp (algo parecido a esto)

```
$(SolutionDir)tmp\$(ProjectName)$(Configuration)\
```
- VALE: LAS PDB NO SE CAMBIARLAS EN CASO DE NO SER NECESARIAS LAS BORRAMOS A PELO PQ NO HAY MANERA DE QUE SE SEPAREN DEL .LIB

- COMO METER LA LIBRERÍA (LOS PASOS QUE HE REALIZADO EN CORE):
	- En propiedades de configuración --> C/C++ --> General --> Directorios de inclusión adicionales --> Agregamos la ruta donde están los archivos .h
	- En propiedades de configuración --> Vinculador --> General --> Directorios de librerías adicionales --> Agregamos la ruta en donde está el .lib
	- En propiedades de configuración --> Vinculador --> Entrada --> Escribir el nombre de la librería y su extension "miLibreria.lib"