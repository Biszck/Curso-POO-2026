Clase 18 - 20 de mayo de 2026
=============================



Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Sobrecarga de operadores, singleton y AdminDBMedicamentos - 2025 <https://youtu.be/8l5L7JraHXU>`_

`Sobrecarga de operadores 2021 <https://youtu.be/QGTNAjeRdNg>`_

`Singleton 2021 <https://youtu.be/RNAZ0pu-Ybc>`_

`const 2025 <https://youtu.be/-z9BhQSPHJg>`_ 

`const 2021 <https://youtu.be/UqXE4GeFd_s>`_ 


Sobrecarga de operadores 
========================

- Supongamos los siguientes objetos de la clase Poste:

.. code-block:: c

	Poste p1;  // Su único miembro dato es un float para la altura del Poste
	Poste p2;

- Necesitamos unir estos Postes para obtener un único Poste con sus alturas sumadas.
- ¿Podemos hacer lo siguiente?

.. code-block:: c

	Poste unidos = p1 + p2;

**Otro ejemplo**

.. code-block:: c

	class Cliente  {
	private:
	    int saldo;

	public:
	    Cliente() : saldo( 0 )  {
	    }

	    void operator+( int sumando )  {
	        this->saldo += sumando;
	    }

	    void operator-( int sustraendo )  {
	        this->saldo -= sustraendo;
	    }

	    bool operator<( Cliente otroCliente )  {
	        if ( this->saldo < otroCliente.saldo )
	            return true;
	        return false;
	    }
	};

	int main( int argc, char ** argv )  {
	    Cliente juan;

	    Cliente carlos;

	    juan + 50;  // Suma 50 a su cuenta

	    carlos + 100;  // Quita 100 a carlos

	    if ( juan < carlos )  {
	        qDebug() << "juan tiene menos";
	    }

	    return 0;
	}




Singleton
=========

- Un singleton es un patrón de diseño que restringe la creación de instancias de una clase a una única instancia.


Ejemplo de AdminDB como singleton
=================================

.. code-block:: c

	#ifndef ADMINDB_H
	#define ADMINDB_H

	class AdminDB  {

	private:
	    static AdminDB * instancia;
	    AdminDB();

	public:
	    static AdminDB * getInstancia();

	    void conectar();
	};

	#endif // ADMINDB_H


.. code-block:: c

	#include "admindb.h"
	#include <QDebug>

	AdminDB * AdminDB::instancia = nullptr;

	AdminDB::AdminDB()  {
	}

	AdminDB * AdminDB::getInstancia()  {
	    if( instancia == nullptr )  {
	        instancia = new AdminDB;
	    }
	    return instancia;
	}

	void AdminDB::conectar()  {
	    qDebug() << "La base se encuentra conectada...";
	}


.. code-block:: c

	#include "admindb.h"

	int main( int, char ** )  {

	    AdminDB::getInstancia()->conectar();

	    return 0;
	}




const
=====

- Una variable definida como const no podrá ser modificada a lo largo del programa (se crea como sólo lectura)
- Se puede aplicar a cualquier tipo:

.. code-block:: c	

	const float pi = 3.14;
	const peso = 67;  // Si no se indica el tipo entonces es int
	                  // Aunque sólo en compiladores viejos



const con punteros
^^^^^^^^^^^^^^^^^^

.. code-block:: c	

	int x = 10;
	int * px = &x;  // normal

	const int y = 10;
	int * py = &y;  // El compilador dirá: "invalid conversion from const int*
	               // to int*". La inversa sí se permite

	int y = 10;
	const int * py = &y;  // permitido (pero el contenido es de sólo lectura)

	*py = 6;  // No permitido. El contenido apuntado es de sólo lectura

	int z = 10;
    const int * const pz = &z;  // Analizar


const en parámetros de funciones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Cuando los parámetros son punteros, decimos que no podrá modificar los objetos referenciados

.. code-block:: c	

	int funcion( const char * ch )


- Lo mismo sucede con referencias

.. code-block:: c	

	int funcion( const char& ch )


const en clases
^^^^^^^^^^^^^^^

.. code-block:: c	

	class ClaseA  {
	    const int i;
	    int x;

	public:
	    int funcion( ClaseA cA, const ClaseA &c )  {
	        cA.x = 1;
	        cA.i = 2;  // No compila. i es de sólo lectura.
	        c.x = 3;   // No compila. El objeto c es de sólo lectura.

	        return cA.x;
	    }
	}; 


.. code-block:: c	

	// A la variable i sólo la puede inicializar el constructor y sólo con la forma:
	ClaseA() : i( 8 )  {  }   

	// Si en el cuerpo del constructor se hace:
	ClaseA()  { 
	    i = 8;  // Compila? i es de solo lectura o no
	}   


- Aplicado a métodos de una clase no permite modificar ninguna propiedad de la clase

.. code-block:: c	

	class ClaseB  {
	    int x;

	    void funcion( int i ) const  {
	        x = x + i;  // Compila?
	    }
	};




Próximos pasos para cerrar la asignatura
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Miércoles 27 de mayo finalizamos con los temas de la asignatura y hacemos simulacro del primer parcial.
- Lunes 1 de junio es el primer parcial.
- Miércoles 3 de junio es el oral del primer parcial, la programación en vivo del Login y presentación de GitHub individual.
- El desarrollo del primer parcial se entrega en el sistema de autocorrección y otorga una nota del 0 al 8.
- En el oral se tratarán los temas que figuran en `Temas para examen <https://github.com/cosimani/Curso-POO-2026/blob/main/ExamenFinal.rst>`_
- La programación en vivo es el desarrollo del Login con o sin QtDesigner. El docente elige cuál de las dos.
- Para la presentación de GitHub individual se pedirá que se clone y se haga push desde consola.
- Lunes 8 de junio se presentan todos los proyectos.
- El proyecto se evaluará con esta `Rúbrica para Trabajo Integrador <https://docs.google.com/spreadsheets/d/1hIZHseh0gT1SujRvPCBrctL8YzdA9tgLtqfP3rcKYeo/edit?usp=drive_link>`_ 
- Preparar una presentación de 10 minutos para la exposición del proyecto.
- Usen los recursos que quieran para la presentación (diapositivas, videos, demostración en vivo, código, etc).


