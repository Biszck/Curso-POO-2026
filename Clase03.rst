Clase 03 - 16 de marzo de 2026
=============================


Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`vector 2021 <https://www.youtube.com/watch?v=mUWIo9uKW5c>`_ 

`Clases 2021 <https://www.youtube.com/watch?v=dH0WqMW3-_w>`_ 




Problema para las próximas semanas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:Una empresa que se dedica al desarrollo de software ofrece soluciones y utiliza las siguientes tecnologías y herramientas:
		- QtCreator como IDE
		- Biblioteca Qt con C++ para aplicaciones Desktop
		- MySQL para base de datos y phpmyadmin para su gestión
		- FastAPI en Python para la API
		- Implementar en contenedores Mysql y FastAPI en un servidor Linux

Necesidad 
^^^^^^^^^

- Se desea una aplicación desktop en Qt que tenga un login de usuarios 
- Cuando un usuario en la aplicación desktop ingrese un usuario válido obtendrá un access token desde la API desarrollada con FastAPI
- Cuando se obtiene el access token, el usuario ya estará logueado, y podrá utilizar este token para próximas consultas a la API
- Los usuarios se almacenarán en una tabla usuarios en MySQL
- Se quiere montar FastAPI y MySQL en contenedores en la nube y que la aplicación desktop pueda loguearse contra FastAPI



Utilidades de la biblioteca estándar de C++
===========================================

vector
^^^^^^

- Mantiene sus elementos en un área contigua de memoria.
- El acceso aleatorio es eficiente.
- La inserción en cualquier posición distinta a la última es ineficiente.
- Se encuentra en #include <vector> en el namespace std

.. code-block:: cpp

	vector< int > v1;                     // vector vacío
	vector< int > v2( 15 );               // vector de 15 elementos
	vector< string > v3( 18, "cadena" );  // 18 elementos con valor inicial
	vector< string > v4( v3 );            // v4 es una copia v3

**Algunas operaciones**

.. code-block:: cpp

	size()          // Tamaño
	bool empty()    // Está vacío?
	void clear()    // Limpia el vector
	front()         // Acceso al primero
	back()          // Al último
	push_back( x )  // Inserción al último
	pop_back()      // Elimina
	w = v           // Asignación
	v == w   v < w  // Comparaciones
	v.at( i )       // Acceso con verificación de rango (lanza out_of_range)
	v[ i ]          // Acceso sin verificación de rango




Clases
======

.. code-block:: cpp

	class Poste  {
	    // Lista de miembros (generalmente funciones y datos)
	    // Los datos no pueden ser inicializados fuera del constructor 
	    // Si las funciones se definen fuera, se usa el operador :: 
	    // :: es el operador de acceso a ámbito
	};


.. code-block::

	class Poste;  // Esto es la declaración de una clase.

.. code-block:: cpp

	class Poste  {  // Esto es la declaración y definición de una clase.
	     
	};




**Ejemplo: Clase Poste**

.. code-block:: cpp

	#include <iostream>
	
	class Poste  {
	private:
	    int altura;
		
	public:
	    Poste() : altura( 0 )  {  }
	    int getAltura();
	};

	int Poste::getAltura()  {
	    return altura;
	}

	int main()  {
	    Poste poste;

	    std::cout << "Altura: " << poste.getAltura() << std::endl;
	    
	    return 0;
	}
	


**Cuestiones sobre declaraciones**

.. code-block:: cpp

	Poste poste;  // Llama al constructor sin parámetros. En esta última versión 
	              // de Poste, esto no serviría, ya que no hay constructor sin parámetros. 
	              // Si no se especifica un constructor, el compilador crea uno. 
	              // Por lo tanto, esta declaración sirve para una clase Poste 
	              // donde el programador no escriba constructor, o escriba uno sin recibir parámetros.

	Poste poste();  // Se entiende como el prototipo de una función sin parámetros que 
	                // devuelve un objeto Poste. Es decir, no sirve para instanciar un 
					// objeto con el constructor sin parámetros de Poste.

	Poste poste1( 12 );  // Válido


**Inicialización de objetos**

.. code-block:: cpp

	// Lo siguiente se permite y funciona casi siempre, (salvo cuando usemos const, que
	// veremos más adelante). Hay que tener presente que aquí, primero se reserva lugar 
	// en memoria para altura conteniendo basura y luego se le asignan los 
	// valores que vienen en los parámetros del constructor.
	Poste( int a )  {
	    altura = a;
	}

	// La siguiente sería la manera más correcta de inicializar los atributos de un 
	// objeto. En este caso, altura nunca contiene basura, sino que 
	// directamente se crean en memoria con el valor que viene en el parámetro del constructor.
	Poste::Poste( int a ) : altura( a )  {  }

	Poste::Poste() : altura( 0 )  {  }


**El puntero this**

- Es un puntero que ya se existe dentro del ámbito de una clase y apunta al propio objeto instanciado.
- Se utiliza para acceder a los atributos y métodos.

.. code-block:: cpp

	#include <iostream>
	
	class Poste  {
	private:
	    int altura;
		
	public:
	    Poste( int altura ) : altura( altura )  {  }
	    
	    int getAltura()  {
	        return this->altura;
	    }

	    void setAltura( int altura )  {
	        this->altura = altura;
	    }

	};


	int main()  {
	    Poste poste;

	    std::cout << "Altura: " << poste.getAltura() << std::endl;
	    
	    return 0;
	}
	

**Destructor**

.. code-block::

	Poste::~Poste()  {
	    this->altura = 0;
	}
	
	
