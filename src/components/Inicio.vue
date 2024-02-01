<template>
<div>
    <b-breadcrumb :items="items"></b-breadcrumb>
    <p>Inicio</p>
    <b-button :to="{ name: 'inicio'}" variant="info">Inicio</b-button>
    <b-button :to="{ name: 'formulario'}" variant="success" >Formulario</b-button>
    <b-button :to="{ name: 'paginacion'}" variant="danger" >Paginación</b-button>
</div>

</template>
  
  <script>
  export default {
    data() {
        return {
            items: [
            {
            text: "Inicio",
            href: "#",
            to: "inicio"
          },
          {
            text: "Formulario",
            href: "#",
            to: "formulario"
          },
          {
            text: "",
            href: "#",
            to: ""
          },
                
            ]
        }
    }
}
  </script>
  
  <style>
  </style>