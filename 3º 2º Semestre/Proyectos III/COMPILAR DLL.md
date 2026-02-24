CAMBIAR EL RESULTADO DE LA COMPILACIÓN DE .EXE(por defecto) a DLL
- 1º Entras en configuraciones del proyecto
- 2º En la sección de general de la parte de propiedades de configuración buscamos "Tipo de configuración" (El 4º desde arriba)
- 3º En ese apartado seleccionamos dll clickando el desplegable y buscando la opción

**IMPORTANTE ANTES DE COMPILAR:**
- En cada método que querrais que se vea en otro proyecto (PARA QUE CORE PUEDA LLAMARLO Y HACER COSAS CON ÉL), teneis que utilizar esta linea delante de los métodos en el .h **__declspec(dllexport)**, SI LO QUE QUEREIS ES QUE SE EXPORTE LA CLASE ENTERA SE HACE LO MISMO PERO DELANTE DEL NOMBRE DE LA CLASE
	- EJEMPLO
		- Solo quiero que se acceda a un método de la clase: (Estoy en el .h)
			- Mi_Clase
				- private:
					- int a 
					- int b
					- void estoNoquieroQueSeVea()
				- public:
					- **__declspec(dllexport)** void estoQuieroQueSeVea()
		- Exporto la clase entera: (Estoy en el .h)
			- **__declspec(dllexport)** Mi_Clase
				- private:
					- int a 
					- int b
					- void estoNoquieroQueSeVea()
				- public:
					-  void estoQuieroQueSeVea()


COMPILACIÓN:
- En modo **RELEASE** compilas haciendo click derecho en tu proyecto, compilar
- Para borrar la pdb:
	- Propiedades del proyecto --> Vinculador --> Depuración --> 2ª opcion "Genera archivos de base de datos del programa" --> Escribes la ruta de tmp