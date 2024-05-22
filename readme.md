# Menú para la consola en C++ 🖥

## ℹ Instalación y Uso 
 1. Descarga el archivo `Menu.h`
 2. Inclúyalo en tu carpeta de trabajo
 3. Importa el archivo de encabezado en donde desee usarlo
 
 ~~~C++
 // archivo .cpp u otro .h 

   #include "Menu.h" 
 ~~~

## 📎 Descripción del programa

 El programa permite mostrar un menú de opciones amigable para el usuario, este se maneja a través de las teclas direccionales. Además, puedes modificar los colores con la librería [Colors](github.com/r0ggdev/Colores) o con sus valores numéricos, se le puede asignar diferentes caracteres ASCII al final o inicio de cada opcion, modificar la posición y la cantidad de elementos a mostrar, soporta hasta 25 opciones. 

 Con esta librería podrás crear dos tipos de menú diferentes.
 ### Menú Horizontal   

 Dentro de este apartado tenemos dos opciones
 
 1. El menú que **muestra todas las opciones** y puedes desplazarte con las teclas direccionales [➡] **Izquierda** y [⬅] **Derecha**.
    ~~~C++
    // los parámetros obligatorios son _x, _y, _num_options
    Menu::RightLeft::AllOptions menu1( _x,  _y, _num_options, _symbol_left,  _symbol_right, _txt_color, _bg_color);
    ~~~
    ![alt text](Sources/MenuAllRgithLeft.gif)

 2. El menú que solo **muestra una opción a la vez**, de igual forma te puedes desplazar con las teclas direccionales [➡] **Izquierda** y [⬅] **Derecha**.
    ~~~C++
    // los parámetros obligatorios son _x, _y, _num_options
    Menu::RightLeft::SingleOption menu1( _x,  _y, _num_options, _symbol_left,  _symbol_right, _txt_color, _bg_color);
    ~~~
  
    ![alt text](Sources/MenuSingleUpDown.gif)
 
 ### Menú Vertical 
 Dentro de este apartado tenemos dos opciones
 
 1. El menú que muestra **todas las opciones** y puedes desplazarte con las teclas direccionales [⬆] **arriba** y [⬇] **arriba**.
    ~~~C++
    // los parámetros obligatorios son _x, _y, _num_options
    Menu::UpDown::SingleOption menu1( _x,  _y, _num_options, _symbol_left,  _symbol_right, _txt_color, _bg_color);
    ~~~
    ![alt text](Sources/MenuAllUpDown.gif)
 
 2. El menú que solo **muestra una opción a la vez**, de igual forma te puedes desplazar con las teclas direccionales [⬆] **arriba** y [⬇] **arriba**.
      ~~~C++
    // los parámetros obligatorios son _x, _y, _num_options
    Menu::UpDown::SingleOption menu1( _x,  _y, _num_options, _symbol_left,  _symbol_right, _txt_color, _bg_color);
    ~~~
    ![alt text](Sources/MenuSingleUpDown.gif)
 

## ⚠ Uso
Para hacer el uso de esta libreria tenemos que elegir el tipo de menu que queremos usar, luego, tenemos que definir las opciones dentro de un arreglo de tipo `const char*`, luego las pasamos con la función `addOptions(_options,...)`. 

Luego debemos pasarle las funciones que se ejecutaran al momento de seleccionar alguna opcion `addOptions(_options,_functions)`.

~~~C++
    // se incluye la libreria 
    #include "Menu.h" 

    // los parámetros obligatorios son _x, _y, _num_options
    Menu::RightLeft::AllOptions menu1( _x,  _y, _num_options, _symbol_left,  _symbol_right, _txt_color, _bg_color);

    // si existen parametros los declarmos en el main
    int param1 = 10;
	int param2 = 20;
	char param3 = 'A';
	char param4 = 'J';

	// se crea un vector con las funciones que se ejcutaran en el menu, se hace usos de lambda
	vector<function<void()>> functions = { 
		[param1, param2]() { exampleFunction1(param1, param2); },
		[param3, param4]() { exampleFunction2(param3, param4); },
		[]() { std::cout << "Option 3 selected!\n"; },
		[]() { std::cout << "Option 4 selected!\n"; }

        // las funciones "exampleFunction1", "exampleFunction2" son funciones voids que se declaran fuera del main con normalidad.
	};

    // declaramos las opciones
    const char* options[] = { "Opcion 1","Opcion 2", "Opcion 3","Opcion 4" };
    
    // agregamos las opciones
    menu1.addOptions(options, functions);

	// se crea un bucle para el menu
	while (true) {
		menu1.showMenu();
	}
~~~