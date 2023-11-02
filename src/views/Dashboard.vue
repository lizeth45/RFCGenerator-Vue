<script>

import Divider from 'primevue/divider';
import { PrimeIcons } from 'primevue/api';

export default {
    data() {
        return {
            items: [
                {
                    label: 'Contacto',
                    items: [
                        { label: 'GitHub', icon: PrimeIcons.PLUS }
                        // ,
                        // { label: 'Open', icon: PrimeIcons.DOWNLOAD }
                    ]
                }
            ]
        };
    }
};


</script>
<template>
    <div class="grid">
        <div class="col-12 ">
            <div class="card">
                <h1 style="text-align: center;"><strong>Hola mundo🖐</strong></h1>
                <img class="rounded-image" src="/layout/images/mybanner.png" alt="Banner" width="920"/> 
                <Divider/> 
                <p class="m-10">Bienvenido a mi portafolio de Vue donde veras mis prácticas realizadas a lo largo del curso "Desarrollo Web" de la Licenciatura de Sofware de la UNACH. Esta página es una plantilla modificada de <a href="https://sakai.primevue.org/#/"><strong>Vue Templates</strong></a> para conocer los diversos componentes del framework.</p>   
                <div class="flex align-items-center justify-content-center pt-2 gap-2">
                    <a class="pi pi-github" style="font-size: 1.5rem" href="https://github.com/lizeth45"></a>
                    <a class="pi pi-linkedin" style="font-size: 1.5rem" href="https://www.linkedin.com/in/lizeth-rodriguez45"></a>
                </div>
            </div>
        </div>
    </div>
    
</template>

<style>
.rounded-image {
  width: 100%;
  height: 100%;
  border-radius: 8px;
}
</style>