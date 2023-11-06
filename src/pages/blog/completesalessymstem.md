---
layout: ../../layout/MarkdownLayout.astro
title: "Sistema completo de ventas"
description: "A través de una web app para tablet, el cliente hace pedidos en un restaurante, una vez completado el pedido, se genera un número de pedido, se envía ticket a cocina y notificación sms al cliente."
pubDate: 2022-12-12
tags: ["Strapi", "React.js", "Twilio", "Epson SDK", "Javascript"]
---

# Sistema de ventas completo para restaurante

Este proyecto incluye una webapp para hacer pedidos desde una tablet en restaurante, un panel de administración
para la gestión de stocks, creación y edición de productos, conexión con impresora térmica ubicada en la cocina y notificación por sms a cliente.

### Tecnologías utilizadas para este proyecto

> - Strapi (Backend)
> - React.js (Frontend)
> - PostgreSQL (Base de datos)
> - SQLite (Base de datos DEV)
> - Twilio (Notificación por sms)
> - Epson SDK (Envío de tickets a cocina)

### Despliegue, infraestructura y herramientas

> - FL0 (Despliegue de la parte backend)
> - Netlify (Despliegue web para administración)
> - Servidor (Alojado en el restaurante, contiene conexiones y aplicación)
> - Epson TM-T20III-002 (Impresora térmica en cocina)

### Diseño
El diseño de banners, iconos, patrones, backgrounds, etc, han sido desarrollados por una empresa externa, hemos ido adaptando la WebApp a los diseños y a las necesidades de cliente.

### Flujo
El usuario entra en el restaurante y dispone de una tablet donde se aloja la app, en esta app puede personalizar menús, añadir entrantes, bebidas y postres entre otros productos, puede personalizar el tamaño de algunos productos y las cantidades. Una vez finalizado el pedido puede elegir acordárse de su número de pedido que se mostrará en pantalla o recibirlo por sms, el pedido viaja a cocina creando un ticket con el total de productos, número de pedido y precio. El cliente espera en su mesa hasta que lo llaman para recoger su comida a través de su número de pedido.

### Panel principal App

![Panel principal](../../../images/nacionpanel1.PNG)

### Carrito resumen App

![Carrito resumen](../../../images/nacioncarrito1.PNG)

### A tener en cuenta

> - Se tiene en cuenta que un menú de niños no tiene capacidad de personalización de tamaño o elección de cafés.
> - Todos los precios se ven modificados en función de las cantidades y tamaños elegidos.
> - El administrador podrá modificar precios y stocks, si un producto se marca sin stock no será añadible y se mostrará una advertencia.

### Administrador (Edición de bowls)
![Edición de bowls](../../../images/nacionadministrador1.PNG)
Aquí podrá editar ingredientes, descripción y precio entre otras acciones. Los ingredientes marcados en rojo sirven como aviso de que alguno de sus productos se encuentra sin stock.

### Administrador (Edición de productos)
![Edición de productos](../../../images/nacionadministrador2.PNG)
En este panel podrá editar productos según su categoría, descripción, tamaño si procede, precio si procede y stock en otras acciones.

#### ¿Por qué no añadir precio o tamaño?
En esta panel se muestran TODOS los productos, tales como bebidas, ingredientes de bowls, etc.
Si un ingrediente como por ejemplo, zanahoria supone un extra de precio a la hora de configurar un bowl, podrá añadir un precio.
Sin embargo, si por ejemplo la categoría es bebidas, todos los productos si llevarán precio.

El tamaño es algo opcional, añadir tacos de pollo a tu bowl no debería necesitar un tamaño, sin embargo un postre, una bebida u otro producto si podría llevar un tamaño por necesidad.

### Seguridad
Tanto el sistema de administración como la WebApp restaurante requiren de inicio de sesión y son cuentas con permisos diferentes.

La WebApp solo funciona en una red privada dentro del restaurante separada de la red wifi de clientes y por tanto no es accesible desde fuera. Aún así, todas las llamadas son identificadas mediante JWT, la WebApp solo tendrá permisos de lectura.

El panel de administración si está desplegado en Netlify, require de inicio de sesión, tiene permisos de lectura y escritura con tiempos de revocación de JWT mucho más rápidos.

### Levantar el sistema en restaurante
Cada vez que abren en local, el servidor se inicia y ejecuta un script como tarea programada que levanta la app en local para que esta esté disponible en la tablet accesible a cliente.

### Actualización
Se dispone de un acceso directo en el panel de administración que ejecuta un script que actualiza la app si se han hecho cambios tales como correción de errores, actualizaciones de código, etc.

### Soporte de emergencia
Se instala un gestor remoto para acceder en remoto al servidor si ocurriese alguna incidencia durante un servicio.

### Configuración de impresora térmica y conexión
Epson facilita un SDK en su documentación que permite apuntar a una impresora térmica a la que enviar el pedido.

La configuración es simple, conectar la impresora a red a través de cable RJ45 (por ejemplo), esta imprimirá una IP entre otros parámetros, con esta IP accedes a la configuración de la impresora en local, añades un certificado de seguridad y desde la WebApp apuntas a esta dirección para imprimir los tickets.
Haremos un post en mi blog hablando sobre esta configuración ya que me he encontrado un poco de todo sobre este tema.

### Despliegue contínuo
Cualquier cambio pusheado sobre la rama desplegada en FL0 o Netlify analizará y desplegará los cambios directamente.

### Desarrollo
Todo desarrollo se hace en una rama develop que permite desplegar los cambios para efectuar un pequeño QA antes de hacer una PR y mergear a master para su despliegue.

### Testing
Queda pendiente añadir testing y herramientas para analizar el código a desplegar antes de cada subida.