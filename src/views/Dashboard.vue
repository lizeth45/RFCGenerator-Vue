<script>

import Divider from 'primevue/divider';


</script>
<template>
    <div class="grid">
        <div class="col-12 ">
            <div class="card">
                <h1 style="text-align: center; color: rgb(30, 120, 255);"><strong>Hola mundo🖐</strong></h1>
                <div class="flex align-items-center justify-content-center">
                <img class="rounded-image" src="/layout/images/contacto.png" alt="Banner" /> 
                </div>
                <Divider/> 
                <p class="m-10">Somos estudiantes de la Lic. en Ingeniería en Desarollo de Tecnologías y Software, con una gran pasión compartida por la tecnología y una innata dedicación a la resolución de problemas de manera innovadora. Este es nuestro portafolio de Vue donde veras nuestras prácticas realizadas a lo largo del curso "Desarrollo Web". Esta página es una plantilla modificada de <a href="https://sakai.primevue.org/#/"><strong>Vue Templates</strong></a> para conocer los diversos componentes del framework.</p>   
                <div class="flex align-items-center justify-content-center pt-2 gap-2">
                    <a class="pi pi-github" style="font-size: 1.5rem" href="https://github.com/lizeth45"></a>
                    <a class="pi pi-linkedin" style="font-size: 1.5rem" href="https://www.linkedin.com/in/lizeth-rodriguez45"></a>
                    <p>Lizeth Rodriguez</p>
                </div>
                <div class="flex align-items-center justify-content-center pt-2 gap-2">
                    <a class="pi pi-github" style="font-size: 1.5rem" href="https://github.com/Michelle-AV"></a>
                    <a class="pi pi-linkedin" style="font-size: 1.5rem" href="https://www.linkedin.com/in/michelle-av/"></a>
                    <p>Michelle Vazquez</p>
                </div>
            </div>
        </div>
    </div>
    
</template>

<style>
.rounded-image {
  width: 50%;
  height: 50%;
}
</style>