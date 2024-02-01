<template>
    <div>
        <b-breadcrumb :items="items"></b-breadcrumb>
        <p>Formulario </p>

        <form @submit.prevent="submitForm">
            <div>
                <label for="marca">Marca:</label>
                <input type="text" id="brand" v-model="brand" required>
            </div>
            <div>
                <label for="modelo">Modelo:</label>
                <input type="text" id="model" v-model="model" required>
            </div>
            <div>
                <label for="anio">Año de Fabricación:</label>
                <input type="number" id="year" v-model="year" required>
            </div>
            <div>
                <label for="numeroSerie">Número de Serie:</label>
                <input type="text" id="serie" v-model="serie" required>
            </div>
            <button type="submit">Enviar</button>
        </form>
    </div>
</template>
   
<script>
import vehiculoService from "../services/Vehiculo";

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
                    text: "Paginación",
                    href: "#",
                    to: "paginacion"
                },
                {
                    text: "",
                    href: "#",
                    to: ""
                },

            ],

            brand: '',
            model: '',
            year: null,
            serie: ''
        }
    },
    methods: {
        async submitForm() {
            // Realizar validaciones
            if (!this.validarMarcaModelo()) {
                alert('La marca y el modelo deben ser alfanuméricos sin signos.');
                return;
            }
            if (!this.validarAnio()) {
                alert('El año de fabricación no puede ser mayor al actual.');
                return;
            }
            if (!this.validarNumeroSerie()) {
                alert('El número de serie debe tener el formato correcto: XXXX000-00XX');
                return;
            }

            // Enviar datos al servicio
            try {
                await vehiculoService.obtenerVehiculosPaginadas(
                    this.pageNum,
                    this.size,
                    this.sort,
                    this.brand,
                    this.model,
                    this.year,
                    this.serie
                );
                alert('Datos del formulario enviados correctamente.');
            } catch (error) {
                console.error('Error al enviar datos del formulario:', error);
                alert('Ocurrió un error al enviar los datos del formulario.');
            }
        },
        validarMarcaModelo() {
            const regex = /^[a-zA-Z0-9\s]+$/;
            return regex.test(this.brand) && regex.test(this.model);
        },
        validarAnio() {
            const currentYear = new Date().getFullYear();
            return this.year <= currentYear;
        },
        validarNumeroSerie() {
            const regex = /^[a-zA-Z]{4}\d{3}-\d{2}[a-zA-Z]{2}$/;
            return regex.test(this.serie);
        }
    }
}
</script>
   
   
<style></style>