<script setup>
import { ref } from 'vue';
import Calendar from 'primevue/calendar';
import Button from 'primevue/button';
import Toast from 'primevue/toast';
import { useToast } from "primevue/usetoast";

const toast = useToast();

const calendarValue = ref(null); // inicializar la propiedad date
const nombre = ref('');
const appat = ref('');
const apmat = ref('');
const rfc = ref('');

const generarRFC = () => {
  // Aquí coloca la lógica para generar el RFC utilizando los valores de nombre, apellidoPaterno, apellidoMaterno y calendarValue.
    const dig1 = (appat.value.substring(0,2)).toUpperCase();
    const dig2 = (apmat.value.substring(0,1)).toUpperCase();
    const dig3 = (nombre.value.substring(0,1)).toUpperCase();

    if(nombre.value != "" && appat.value !="" && apmat.value !="" && calendarValue.value !=null){
        const fechaNac = calendarValue.value.toLocaleDateString('es-MX', {
            day: '2-digit',
            month: '2-digit',
            year: 'numeric'
        }).replace(/\//g, '');
        rfc.value = dig1 + dig2 + dig3 + fechaNac+ "TK0";
    }else{
        toast.add({ severity: 'warn', summary: 'Aviso', detail: 'Completa todos los campos para generar tu RFC.', life: 3000 });
    }

};

const limpiar = () => {
    nombre.value="";
    appat.value="";
    apmat.value="";
    rfc.value="";
    calendarValue.value = null;
}

</script>
<template>
    <div class="grid">
        <div class="col-12">
            <div class="card">
                <h5>Generar el RFC de una persona</h5>
                <div class="p-fluid formgrid grid">
                    <div class="field col-12 md:col-12">
                        <label for="firstname">Nombre(s):</label>
                        <InputText v-model="nombre" type="text" id="firstname" />
                    </div>
                    <div class="field col-12 md:col-12">
                        <label for="appat">Apellido Paterno:</label>
                        <InputText v-model="appat" type="text" id="appat" />
                    </div>
                    <div class="field col-12 md:col-12">
                        <label for="apmat">Apellido Materno:</label>
                        <InputText v-model="apmat" type="text" id="apmat" />
                    </div>

                    <div class="field col-6">
                        <label >Fecha de Nacimiento:</label>
                        <Calendar  :showIcon="true" :showButtonBar="true" v-model="calendarValue" dateFormat="dd/mm/yy" placeholder="dd/mm/aaaa"></Calendar>
                    </div>
                    <div class="field col-12 md:col-6">
                        <label style="color:white">*</label>
                        <Button @click="generarRFC" label="GENERAR" />
                    </div>
                    <div class="field col-12 md:col-6">
                        <label for="rfc"><strong>RFC:</strong></label>
                        <InputText v-model="rfc" type="text" id="rfc"/>
                    </div>
                    <div class="field col-12 md:col-6">
                        <label style="color:white">*</label>
                        <Button @click="limpiar" label="Limpiar" severity="info" text />
                    </div>
                    <Toast />
                </div>
            </div>
        </div>
    </div>
</template>
