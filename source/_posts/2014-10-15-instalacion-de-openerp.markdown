---
layout: post
title: "Instalación de OpenERP"
date: 2014-10-15 18:55:25 +0200
comments: true
categories: OpenERP
published: true
---

OpenERP es un sistema de ERP, Enterprise Resource Planning, horizontal que son sistemas de planificación de recursos empresariales de forma modular. <!-- more -->

#Preparación
- Creamos un usuario del sistema para ejecutar OpenERP, los usuarios del sistema no son usuarios normales logueables.
```
sudo adduser --system --home=/opt/openerp --group openerp
```

- Instalamos Postgres:
```
sudo apt-get install postgresql postgresql-client
```

- Comprobamos que se ha creado el usuario `postgres` en el sistema en la instalación: 
```
cat /etc/passwd
```

- Pasamos a trabajar con el usuario `postgres` recién creado:
```
sudo su postgres
```

- Creamos un usuario para la base de datos desde el user `postgres` y establecemos una contraseña:
```
createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt openerp
```

- Para comprobar entramos con: 
```
psql
``` 

- Y listamos los usuarios creados:
```
SELECT * FROM pg_user;
```

- Y salimos de `psql` con:
```
\q
```

- Y también salimos del usuario `postgres`: 
```
exit
```

- Ahora instalamos librerías Python requeridas por el servidor OpenERP: 
```
sudo apt-get install python-dateutil python-docutils python-feedparser python-gdata \
python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid \
python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing \
python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject \
python-webdav python-werkzeug python-xlwt python-yaml python-zsi
```

#Instalación
- Abrimos el instalador de paquetes e instalamos OpenERP. 
- Ya podremos acceder desde `http://localhost:8069/`

#Configuración
- **Contraseña maestra:** admin (por defecto)
- **Nombre de la base de datos:** -
- No cargamos datos de demostración. 
- **Idioma:** -
- **Contraseña:** -
- Y una vez cumplidos los pasos, podremos instalar los módulos que queramos. 











