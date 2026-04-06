Clase 07 - 1 de abril de 2026
=============================



Registro en video de algunos temas de la clase de hoy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`Fución genérica - signals y slots - empty project 2025 <https://youtu.be/wnkHlGuUZZQ>`_ 

`Dibujar a mano - QByteArray - Preprocesador 2021 <https://www.youtube.com/watch?v=8Gu5_ejipus>`_



Macro Q_OBJECT
^^^^^^^^^^^^^^

- Convierte a una clase cualquiera en una clase Qt.
- Una clase Qt permitirá trabajar con signals y slots.
- Incluir la macro Q_OBJECT en la primer línea de la definición de la clase.


QGridLayout
^^^^^^^^^^^

- Ubica los widgets en una grilla
- Con setColumnMinimumWidth() podemos setear el ancho mínimo de columna
- Separación entre widget con setVerticalSpacing( int )
- void addWidget( QWidget * widget, int fila, int columna, int spanFila, int spanCol )



QLineEdit
^^^^^^^^^

.. code-block:: cpp

	QLineEdit * le = new QLineEdit;
	le->setEchoMode( QLineEdit::Password );
	le->setEnabled( false );

	// QLineEdit::Normal  // Se visualizan al escribir
	// QLineEdit::NoEcho  // No se visualiza nada
	// QLineEdit::Password  // Se escribe como asteriscos
	// QLineEdit::PasswordEchoOnEdit  // Se escribe normal y al dejar de editar se convierten en asteriscos

**Señales**

.. code-block:: cpp

	void returnPressed();  // Detecta cuando el usuario presiona Enter.

	void editingFinished();  // Cuando pierde foco.

	void textChanged( const QString & text );  // Texto modificado por código o por usuario desde la gui.

	void textEdited( const QString & text );  // Sólo por el usuario.



Dibujar a mano sobre un QWidget
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: cpp

	// mapa.h
	#include <QWidget>

	class Mapa : public QWidget  {
	    Q_OBJECT

	public:
	    Mapa()  {  }

	protected:
	    void paintEvent( QPaintEvent * );

	};

	// mapa.cpp
	#include "mapa.h"
	#include <QPainter>

	void Mapa::paintEvent( QPaintEvent * )  {
	    QPainter painter( this );
	    painter.drawLine( 0, 0, this->width(), this->height() );
	}


**Clase QPainter**

- Pinta a bajo nivel sobre widgets.
- Debe ser utilizado dentro del método ``paintEvent( QPaintEvent * )``.

.. code-block:: cpp

	void drawEllipse( int x, int y, int ancho, int alto );
	void drawImage( int x, int y, QImage & image );
	void drawLine( int x1, int y1, int x2, int y2 );
	void drawText( int x, int y, QString & text );
	void fillRect( int x, int y, int ancho, int alto );




Ejercicio 03 - Lienzo colaborativo en tiempo real
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Desarrollar una aplicación de escritorio en Qt que permita dibujar a mano alzada sobre un lienzo, con comportamiento suave y continuo, incorporando sincronización colaborativa mediante el servidor VPS del equipo. La aplicación debe cumplir con los siguientes requisitos:

Requisitos generales
--------------------

- La aplicación debe implementar un lienzo de dibujo utilizando paintEvent.
- El sistema debe permitir dibujo libre a mano alzada, con suavizado visual y control dinámico del trazo.
- El dibujo será colaborativo entre los integrantes del equipo, sincronizado a través de un backend en VPS.

Interacción de dibujo
---------------------

- Click izquierdo (presionado): dibuja sobre el lienzo
- Click derecho (presionado): actúa como goma (borra el dibujo)

El trazo debe ser:
------------------

- Continuo (sin segmentos visibles)
- Suavizado (no deben notarse “líneas rectas” entre puntos)
- Independiente de la velocidad del mouse

Se debe implementar un mecanismo propio de:
-------------------------------------------

- Interpolación de puntos
- Suavizado del trazo
- Color del trazo: se selecciona con teclas numéricas 1 al 9

- Debe generarse una interpolación de colores entre:

  - RGB inicial: (192, 19, 76)
  - RGB final: (24, 233, 199)
  - El cambio debe ser progresivo

- Grosor del trazo:

  - Se controla con la rueda del mouse (scroll)
  - Debe afectar tanto al lápiz como a la goma
  
- Interfaz gráfica

  - Debe existir una barra superior (tipo menú o toolbar) sobre el lienzo
  - Incluir un botón Guardar con estilo visual tipo Metro de Windows

- Implementar un endpoint en el VPS que permita:

  - Guardar el estado del dibujo
  - Recuperar el dibujo actual
  - Funcionalidad:

    - Al presionar Guardar, se envía el dibujo al servidor
    - Al iniciar la aplicación:

      - Se debe recuperar el dibujo almacenado
      - Permitir continuar editando
      - Colaboración en tiempo real
      - El dibujo es compartido entre los integrantes del equipo
      - Reglas:

        - Si un usuario guarda → actualiza el estado en el servidor
        - Los demás usuarios deben poder:

          - Ver los cambios realizados por otros
          - Sin perder lo que están dibujando localmente

      - Condición clave:
      
        - No se debe perder información al guardar

- Se debe implementar una estrategia de:

  - Fusión de trazos (merge)
  - Modelo incremental de dibujo

Arquitectura (obligatoria)
--------------------------

Se debe implementar al menos:

- Una clase para el modelo de dibujo (almacenamiento de trazos)
- Una clase para la vista (renderizado con paintEvent)
- Una clase para la lógica de sincronización (API / VPS)


