<script>
import DataTable from 'primevue/datatable';
import { ref, onMounted, watch } from 'vue';
import axios from 'axios';
import Chart from 'primevue/chart';

export default {
    data() {

        const listDatos = ref([]);
        const chartDatos = ref();
        const chartOptions = ref();

        async function llenarChart() {
            const response = await axios.get(`https://eodhistoricaldata.com/api/eod/MCD.US?from=2017-01-05&to=2017-02-05&period=d&fmt=json&api_token=OeAFFmMliFG5orCUuwAKQ8l4WWFQ67YX`);
            listDatos.value = response.data;
        }

        const setChartDatos = () => {
            const documentStyle = getComputedStyle(document.documentElement);
            return {
                labels: listDatos.value.map(item => item.date),
                datasets: [
                    {
                        label: 'Cambio porcentual trimestral',
                        data: listDatos.value.map(item => item.open),
                        backgroundColor: documentStyle.getPropertyValue('--primary-500'),
                        borderColor: documentStyle.getPropertyValue('--primary-500'),
                        tension: 0.4
                    },
                ]
            };
        };

        const setChartOptions = () => {
            const documentStyle = getComputedStyle(document.documentElement);
            const textColor = documentStyle.getPropertyValue('--text-color');
            const textColorSecondary = documentStyle.getPropertyValue('--text-color-secondary');
            const surfaceBorder = documentStyle.getPropertyValue('--surface-border');
            return {
                maintainAspectRatio: false,
                aspectRatio: 0.6,
                plugins: {
                    legend: {
                        labels: {
                            color: textColor
                        }
                    }
                },
                scales: {
                    x: {
                        ticks: {
                            color: textColorSecondary
                        },
                        grid: {
                            color: surfaceBorder
                        }
                    },
                    y: {
                        ticks: {
                            color: textColorSecondary
                        },
                        grid: {
                            color: surfaceBorder
                        }
                    }
                }
            };
        }

        watch(listDatos, () => {
            chartDatos.value = setChartDatos();
        });

        onMounted(() => {
            llenarChart();
        });
        
        return { 
            llenarChart,
            listDatos, 
            chartDatos,
            chartOptions
		}
}
}
// const { layoutConfig } = useLayout();
// let documentStyle = getComputedStyle(document.documentElement);
// let textColor = documentStyle.getPropertyValue('--text-color');
// let textColorSecondary = documentStyle.getPropertyValue('--text-color-secondary');
// let surfaceBorder = documentStyle.getPropertyValue('--surface-border');

// const lineData = ref(null);
// const pieData = ref(null);
// const polarData = ref(null);
// const barData = ref(null);
// const radarData = ref(null);

// const lineOptions = ref(null);
// const pieOptions = ref(null);
// const polarOptions = ref(null);
// const barOptions = ref(null);
// const radarOptions = ref(null);

// const setColorOptions = () => {
//     documentStyle = getComputedStyle(document.documentElement);
//     textColor = documentStyle.getPropertyValue('--text-color');
//     textColorSecondary = documentStyle.getPropertyValue('--text-color-secondary');
//     surfaceBorder = documentStyle.getPropertyValue('--surface-border');
// };

// const setChart = () => {
//     barData.value = {
//         labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
//         datasets: [
//             {
//                 label: 'My First dataset',
//                 backgroundColor: documentStyle.getPropertyValue('--primary-500'),
//                 borderColor: documentStyle.getPropertyValue('--primary-500'),
//                 data: [65, 59, 80, 81, 56, 55, 40]
//             },
//             {
//                 label: 'My Second dataset',
//                 backgroundColor: documentStyle.getPropertyValue('--primary-200'),
//                 borderColor: documentStyle.getPropertyValue('--primary-200'),
//                 data: [28, 48, 40, 19, 86, 27, 90]
//             }
//         ]
//     };
//     barOptions.value = {
//         plugins: {
//             legend: {
//                 labels: {
//                     fontColor: textColor
//                 }
//             }
//         },
//         scales: {
//             x: {
//                 ticks: {
//                     color: textColorSecondary,
//                     font: {
//                         weight: 500
//                     }
//                 },
//                 grid: {
//                     display: false,
//                     drawBorder: false
//                 }
//             },
//             y: {
//                 ticks: {
//                     color: textColorSecondary
//                 },
//                 grid: {
//                     color: surfaceBorder,
//                     drawBorder: false
//                 }
//             }
//         }
//     };

//     pieData.value = {
//         labels: ['A', 'B', 'C'],
//         datasets: [
//             {
//                 data: [540, 325, 702],
//                 backgroundColor: [documentStyle.getPropertyValue('--indigo-500'), documentStyle.getPropertyValue('--purple-500'), documentStyle.getPropertyValue('--teal-500')],
//                 hoverBackgroundColor: [documentStyle.getPropertyValue('--indigo-400'), documentStyle.getPropertyValue('--purple-400'), documentStyle.getPropertyValue('--teal-400')]
//             }
//         ]
//     };

//     pieOptions.value = {
//         plugins: {
//             legend: {
//                 labels: {
//                     usePointStyle: true,
//                     color: textColor
//                 }
//             }
//         }
//     };

//     lineData.value = {
//         labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
//         datasets: [
//             {
//                 label: 'First Dataset',
//                 data: [65, 59, 80, 81, 56, 55, 40],
//                 fill: false,
//                 backgroundColor: documentStyle.getPropertyValue('--primary-500'),
//                 borderColor: documentStyle.getPropertyValue('--primary-500'),
//                 tension: 0.4
//             }
//             // ,
//             // {
//             //     label: 'Second Dataset',
//             //     data: [28, 48, 40, 19, 86, 27, 90],
//             //     fill: false,
//             //     backgroundColor: documentStyle.getPropertyValue('--primary-200'),
//             //     borderColor: documentStyle.getPropertyValue('--primary-200'),
//             //     tension: 0.4
//             // }
//         ]
//     };

//     lineOptions.value = {
//         plugins: {
//             legend: {
//                 labels: {
//                     fontColor: textColor
//                 }
//             }
//         },
//         scales: {
//             x: {
//                 ticks: {
//                     color: textColorSecondary
//                 },
//                 grid: {
//                     color: surfaceBorder,
//                     drawBorder: false
//                 }
//             },
//             y: {
//                 ticks: {
//                     color: textColorSecondary
//                 },
//                 grid: {
//                     color: surfaceBorder,
//                     drawBorder: false
//                 }
//             }
//         }
//     };

//     polarData.value = {
//         datasets: [
//             {
//                 data: [11, 16, 7, 3],
//                 backgroundColor: [documentStyle.getPropertyValue('--indigo-500'), documentStyle.getPropertyValue('--purple-500'), documentStyle.getPropertyValue('--teal-500'), documentStyle.getPropertyValue('--orange-500')],
//                 label: 'My dataset'
//             }
//         ],
//         labels: ['Indigo', 'Purple', 'Teal', 'Orange']
//     };

//     polarOptions.value = {
//         plugins: {
//             legend: {
//                 labels: {
//                     color: textColor
//                 }
//             }
//         },
//         scales: {
//             r: {
//                 grid: {
//                     color: surfaceBorder
//                 }
//             }
//         }
//     };

//     radarData.value = {
//         labels: ['Eating', 'Drinking', 'Sleeping', 'Designing', 'Coding', 'Cycling', 'Running'],
//         datasets: [
//             {
//                 label: 'My First dataset',
//                 borderColor: documentStyle.getPropertyValue('--indigo-400'),
//                 pointBackgroundColor: documentStyle.getPropertyValue('--indigo-400'),
//                 pointBorderColor: documentStyle.getPropertyValue('--indigo-400'),
//                 pointHoverBackgroundColor: textColor,
//                 pointHoverBorderColor: documentStyle.getPropertyValue('--indigo-400'),
//                 data: [65, 59, 90, 81, 56, 55, 40]
//             },
//             {
//                 label: 'My Second dataset',
//                 borderColor: documentStyle.getPropertyValue('--purple-400'),
//                 pointBackgroundColor: documentStyle.getPropertyValue('--purple-400'),
//                 pointBorderColor: documentStyle.getPropertyValue('--purple-400'),
//                 pointHoverBackgroundColor: textColor,
//                 pointHoverBorderColor: documentStyle.getPropertyValue('--purple-400'),
//                 data: [28, 48, 40, 19, 96, 27, 100]
//             }
//         ]
//     };

//     radarOptions.value = {
//         plugins: {
//             legend: {
//                 labels: {
//                     fontColor: textColor
//                 }
//             }
//         },
//         scales: {
//             r: {
//                 grid: {
//                     color: textColorSecondary
//                 }
//             }
//         }
//     };
// };

// watch(
//     layoutConfig.theme,
//     () => {
//         setColorOptions();
//         setChart();
//     },
//     { immediate: true }
// );
</script>

<template>
    <div class="grid p-fluid">
        <div class="col-12 xl:col-12">
            <div class="card">
                <h5>API de datos históricos del mercado de valores de Lyon, Francia.</h5>
                <Chart type="line" :data="chartDatos" :options="chartOptions"></Chart>
            </div>
        </div>
        <!-- <div class="col-12 xl:col-6">
            <div class="card">
                <h5>Bar Chart</h5>
                <Chart type="bar" :data="barData" :options="barOptions"></Chart>
            </div>
        </div> -->
        <!-- <div class="col-12 xl:col-6">
            <div class="card flex flex-column align-items-center">
                <h5 class="text-left w-full">Pie Chart</h5>
                <Chart type="pie" :data="pieData" :options="pieOptions"></Chart>
            </div>
        </div>
        <div class="col-12 xl:col-6">
            <div class="card flex flex-column align-items-center">
                <h5 class="text-left w-full">Doughnut Chart</h5>
                <Chart type="doughnut" :data="pieData" :options="pieOptions"></Chart>
            </div>
        </div>
        <div class="col-12 xl:col-6">
            <div class="card flex flex-column align-items-center">
                <h5 class="text-left w-full">Polar Area Chart</h5>
                <Chart type="polarArea" :data="polarData" :options="polarOptions"></Chart>
            </div>
        </div> -->
        <!-- <div class="col-12 xl:col-6">
            <div class="card flex flex-column align-items-center">
                <h5 class="text-left w-full">Radar Chart</h5>
                <Chart type="radar" :data="radarData" :options="radarOptions"></Chart>
            </div>
        </div> -->
        <div class="col-12 xl:col-10">
            <div class="card">
                <h5>Cambio porcentual por día de acciones AAPL (2017-01-05/2017-02-05).</h5>
                <DataTable class="mt-4" :value="listDatos" paginator :rows="5" :rowsPerPageOptions="[5, 10, 20, 50]" tableStyle="min-width: 50rem"
                        paginatorTemplate="RowsPerPageDropdown FirstPageLink PrevPageLink CurrentPageReport NextPageLink LastPageLink"
                        currentPageReportTemplate="{first} al {last} de {totalRecords}">
                        <template #paginatorstart>
                            <Button type="button" icon="pi pi-refresh" text @click="llenarChart()"/>
                        </template>

                    <Column field="fecha" header="Fecha">
                        <template #body="slotProps">
                            {{ slotProps.data.date }}
                        </template>
                    </Column>
                    <Column field="apertura" header="Valor Apertura" >
                        <template #body="slotProps">
                            {{ slotProps.data.open }}
                        </template>
                    </Column>
                    <Column field="cierre" header="Valor Cierre" >
                        <template #body="slotProps">
                            {{ slotProps.data.close }}
                        </template>
                    </Column>
                </DataTable>
            </div>
        </div>
    </div>
</template>
