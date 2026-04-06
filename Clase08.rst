Clase 08 - 6 de abril de 2026
=============================

Repositorio VPS-POO (privado)
------------------------------

Tengo un repositorio privado para esta clase:

- https://github.com/cosimani/vps-poo-2026

Este repo trae un sistema minimo autocontenido con FastAPI, React, MySQL,
phpMyAdmin y Nginx, y un docker compose listo para levantar todo.

Como es privado, para poder clonar deben pedirme acceso por mail e incluir:

- Nombre completo
- Usuario de GitHub

Luego envio la invitacion y deben aceptarla en GitHub.

Despues de recibir acceso:

.. code-block:: bash

	git clone git@github.com:cosimani/vps-poo-2026.git
	cd vps-poo-2026

Resumen del README
------------------

Antes de empezar (Ubuntu):

.. code-block:: bash

	sudo apt update
	sudo apt install -y docker.io docker-compose-plugin
	sudo usermod -aG docker $USER
	newgrp docker

Luego abrir puertos 80 y 443 en el servidor.

Antes de levantar Docker, abrir .env y cambiar las credenciales.

Levantar el sistema:

.. code-block:: bash

	docker compose up -d --build

Accesos:

- App: https://TU_IP_O_DOMINIO (acepta el certificado autofirmado)
- phpMyAdmin: https://TU_IP_O_DOMINIO/poo_phpmyadmin/

Credenciales listas para usar:

- App (login): usuario/clave ver en .env (cambiar antes de usar)
- phpMyAdmin (Basic Auth): usuario/clave ver en .env (cambiar antes de usar)
- API (Basic Auth): usuario/clave ver en .env (cambiar antes de usar)
- MySQL: base vps-poo, usuario/clave ver en .env (cambiar antes de usar)

Notas cortas:

- El certificado es autofirmado por defecto.
- La base se inicializa con el SQL en db/init.sql.
- Swagger y llamadas a la API requieren Basic Auth (el frontend ya lo envia automaticamente).
- El token JWT se envia en el header X-Access-Token para no chocar con Basic Auth.
- El frontend embebe el Basic Auth al momento del build.

Lets Encrypt:

Leer primero de que se trata Lets Encrypt antes de seguir estos pasos.
Los pasos estan en el README del repo.



