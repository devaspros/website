---
name: Lupita
description: Historia Clinica para Neonatos
class_name: lupita
image: /images/projects-logos/lupita-logo.png

layout: default
---

<section class="projects-page">
  <div class="container text-center">
    <h1 class="text-shadow">
      {{ page.name }}
    </h1>
  </div>
</section>

<section class="projects-list">
  <div class="container">
    <div class="row">
      <div class="col-md-8">
        {{ page.description }}
      </div>
      <div class="col-md-4">
        <img src="{{ page.image }}" />
      </div>
    </div>
  </div>
</section>
