---
layout: post
title: "Sobre Boring Software y el Heroku Stack"
date: 2021-04-07
canonical_url: "https://elcaminodelpro.wordpress.com/2021/04/07/sobre-boring-software-y-el-heroku-stack/"
---

![Foto de oficina](https://elcaminodelpro.wordpress.com/wp-content/uploads/2021/04/jakub-kriz-aroydpuajzc-unsplash.jpg?w=1024)

Dos conceptos que guían la forma en que construimos software.

## Boring Software

La idea es simple: usar tecnologías probadas y estables en lugar de lo más nuevo. Cada tecnología nueva representa riesgos: errores, agujeros de seguridad, características incompletas.

El concepto de "tokens de innovación" lo resume bien: tu proyecto tiene tres tokens disponibles. Gastar uno implica planificación, tiempo, dinero y esfuerzo adicional. El manifiesto Boring Software propone:

- Aplicaciones de 3 capas en lugar de microservicios.
- Bases de datos relacionales en lugar de NoSQL.
- Sitios con recarga en lugar de SPAs.

## Heroku Stack

Para proyectos iniciales, Heroku o Vercel son preferibles a AWS. AWS requiere un enorme trabajo de configuración e infraestructura. Heroku solo requiere subir cambios a un repositorio.

La regla: *"Usa Heroku hasta cuando ya sea muy caro para tu software."*

El primer gran problema que quieres tener es escalabilidad. Hasta entonces, apégate a lo sencillo.
