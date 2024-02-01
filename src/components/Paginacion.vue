<template>
    <div>
        <b-breadcrumb :items="items"></b-breadcrumb>
        <p>Paginación </p>

        <b-container class="mt-5">
            <b-table id="my-table" :items="vehiculos" :per-page="perPage" :current-page="currentPage" :fields="fields"
                :sort-by.sync="sortBy" :sort-desc.sync="sortDesc" label-sort-asc="" label-sort-desc="" small sortable>
            </b-table>
            <div class="overflow-auto">
                <b-pagination v-model="currentPage" :total-rows="vehiculos.length" :per-page="perPage"
                    aria-controls="my-table"></b-pagination>

                <p class="mt-3">Current Page: {{ currentPage }}</p>
            </div>
        </b-container>
    </div>
</template>
   
<script>
import vehiculoService from '../services/Vehiculo';

export default {
    data() {
        return {
            items: [

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

            ],
            sortBy: "brand",
            sortDesc: false,
            perPage: 3,
            currentPage: 1,
            vehiculos: [],
            fields: [
                { key: "brand", label: "Brand", sortable: true },
                { key: "model", label: "Model", sortable: true },
                { key: "serie", label: "Serie", sortable: true },
                { key: "year", label: "Year", sortable: true },

            ],
        }

    },
    mounted() {
        this.obtenerVehiculo();
    },
    methods: {
        async obtenerVehiculo() {
            try {
                const data = await vehiculoService.obtenerVehiculosPaginadas(
                    parseInt(this.currentPage),
                    parseInt(this.perPage),
                    this.sortBy
                );
                this.personas = data.content;
            } catch (error) {
                console.error(error);
                // Manejar errores (puedes mostrar un mensaje de error al usuario, por ejemplo)
            }
        },
    },
}
</script>
   
   
<style></style>