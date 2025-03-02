<template>
    <div class="container p-5">
        <h3>Tiquete #{{ tiquete.id }}</h3>
        <div class="mb-3">
            <label for="nombre" class="form-label">Nombre</label>
            <input ref="inputNombre" v-model="tiqueteMutable.nombre" type="text" class="form-control" id="nombre" name="nombre" placeholder="Nombre Completo">
        </div>
        <div class="mb-3">
            <label for="categoria" class="form-label">Categoria</label>
            <select v-model="tiqueteMutable.categoria" class="form-select" id="categoria" name="categoria">
            <option value="">Solicitud de equipo</option>
            <option value="">Problema Tecnico</option>
            <option value="">Acceso</option>
            <option value="">Consulta</option>
            <option value="">Otro</option>
            </select>
        </div>
        <div class="mb-3">
            <label for="estado" class="form-label">Estado</label>
            <select v-model="tiqueteMutable.estado" class="form-select" name="estado" id="estado">
            <option value="">Pendiente</option>
            <option value="">En progreso</option>
            <option value="">Completado</option>
            <option value="">Cerrado</option>
        </select>
        </div>
        <div class="mb-3">
            <label for="asunto" class="form-label">Asulto</label>
            <input type="text" v-model="tiqueteMutable.asunto" class="form-control" id="asunto" name="asunto" placeholder="Asunto">
        </div>
        <div class="mb-3 row">
            <div class="col-2">
                <button type="button" @click="guardarCambios" class="btn btn-primary col">Guardar Cambios</button>
            </div>
            <div class="col">
                <button type="button" @click="cerrarFormulario" class="btn btn-outline-second col">Cerrar Formulario</button>
            </div>
        </div>
    </div>
</template>

<script>
import { cloneDeep, uniqueId } from 'lodash';
export default {
    name: 'FormularioTiquete',
    data() {
        return {
            tiqueteMutable: undefined
        }
    },
    watch:{
        tiquete: {
            handler(){
                this.tiqueteMutable = cloneDeep(this.tiquete);
            },
            deep: true,
            immediate: true,
        }
    },
    methods: {
        cerrarFormulario() {
            this.$emit('clickCerrar');
        },
        guardarCambios(){
            if(!this.tiqueteMutable.id){
                this.tiqueteMutable.id = uniqueId();
            }
            this.$emit('clickGuardar', this.tiqueteMutable);
        }
    },
    beforeCreate() {
        console.log('1. beforeCreate');
    },
    created(){
        console.log('2. created');
    },
    mounted(){
        this.$refs.inputNombre.focus();
        console.log('3. mounted');
    },
    beforeUpdate(){
        console.log('4. beforeUpdate');
    },
    updated() {
        console.log('5. updated');
    },
    beforeUnmount() {
        console.log('6. beforeUnmount');
    },
    unmounted() {
        console.log('7. unmounted');
    },
    props: ['tiquete']
}
</script>