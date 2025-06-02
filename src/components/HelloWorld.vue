<template>
<div>
    <v-card class="mx-auto mt-5" width="900" elevation="5">
        <v-card-title class="bg-primary white--text">EJEMPLO TABLA CON FILTROS <v-btn class="bg-primary" @click=" reiniciarFiltros()"><v-icon>mdi-refresh</v-icon></v-btn></v-card-title>
        <v-card-text>

            <v-table>
                <thead>
                    <tr>
                        <th>Id</th>
                        <th>
                            <v-menu width="200" :close-on-content-click="false" v-model="menuCabeceraFecha">
                                <template v-slot:activator="{ props }">
                                    <span v-bind="props">Fecha
                                        <v-icon size="small" color="primary">mdi-filter</v-icon>
                                        <v-icon size="small" color="info" v-if="mostrarCheckFiltroFechaRevisar">mdi-check</v-icon>
                                    </span>
                                </template>

                                <v-card elevation="3">
                                    <v-card-actions class=" text-center">
                                        <v-btn class="bg-info" size="small" @click="inicializarListaDeFiltroCabeceraTabla(bandera_opcion_1 = !bandera_opcion_1, 1 )">
                                            <v-icon size="large">mdi-filter-remove-outline</v-icon>
                                        </v-btn>
                                        <v-btn size="small" class="bg-primary" @click="ordenarListaDeFiltroCabeceraTabla(1)">
                                            <v-icon size="large">mdi-order-alphabetical-ascending</v-icon>
                                        </v-btn>
                                        <v-btn size="small" class="bg-primary" @click="ordenarListaDeFiltroCabeceraTabla(2)">
                                            <v-icon size="large">mdi-order-alphabetical-descending</v-icon>
                                        </v-btn>
                                    </v-card-actions>
                                    <v-divider></v-divider>
                                    <v-container fluid>
                                        <span v-for="item  in valoresUnicosFecha" :key="item" value="item">
                                            <label>
                                                <input type="checkbox" :value="item" :label="item" v-model="seleccionadosFecha" density="compact" /> &nbsp; <span id="checkFecha">{{ item }} </span> <br />
                                            </label>
                                        </span>
                                    </v-container>
                                    <v-divider></v-divider>
                                    <v-card-actions>
                                        <v-spacer></v-spacer>
                                        <v-btn @click="menuCabeceraFecha = false" elevation="5" density="compact">
                                            Cancelar
                                        </v-btn>
                                        <v-btn color="primary" @click="filterItemsNuevo(seleccionadosFecha),menuCabeceraFecha = false " elevation="5" density="compact" v-if="seleccionadosFecha.length!=0">
                                            OK
                                        </v-btn>
                                        <v-btn color="primary" disabled elevation="5" density="compact" v-else>
                                            OK
                                        </v-btn>
                                    </v-card-actions>
                                </v-card>

                            </v-menu>
                        </th>

                        <th>
                            <v-menu width="200" :close-on-content-click="false" v-model="menuCabeceraColor">
                                <template v-slot:activator="{ props }">
                                    <span v-bind="props">Color
                                        <v-icon size="small" color="primary">mdi-filter</v-icon>
                                        <v-icon size="small" color="info" v-if="mostrarCheckFiltroColorRevisar">mdi-check</v-icon>
                                    </span>
                                </template>

                                <v-card elevation="3">
                                    <v-card-actions class=" text-center">
                                        <v-btn class="bg-info" size="small" @click="inicializarListaDeFiltroCabeceraTabla(bandera_opcion_2 = !bandera_opcion_2, 2 )">
                                            <v-icon size="large">mdi-filter-remove-outline</v-icon>
                                        </v-btn>
                                        <v-btn size="small" class="bg-primary" @click="ordenarListaDeFiltroCabeceraTabla(3)">
                                            <v-icon size="large">mdi-order-alphabetical-ascending</v-icon>
                                        </v-btn>
                                        <v-btn size="small" class="bg-primary" @click="ordenarListaDeFiltroCabeceraTabla(4)">
                                            <v-icon size="large">mdi-order-alphabetical-descending</v-icon>
                                        </v-btn>
                                    </v-card-actions>
                                    <v-divider></v-divider>
                                    <v-container fluid>
                                        <span v-for="item  in valoresUnicosColor" :key="item" value="item">
                                            <label>
                                                <input type="checkbox" :value="item" :label="item" v-model="seleccionadosColor" density="compact" /> &nbsp; <span id="checkFecha">{{ item }} </span> <br />
                                            </label>
                                        </span>
                                    </v-container>
                                    <v-divider></v-divider>
                                    <v-card-actions>
                                        <v-spacer></v-spacer>
                                        <v-btn @click="menuCabeceraColor = false" elevation="5" density="compact">
                                            Cancelar
                                        </v-btn>
                                        <v-btn color="primary" @click="filterItemsNuevo2(seleccionadosColor),menuCabeceraColor = false " elevation="5" density="compact" v-if="seleccionadosColor.length!=0">
                                            OK
                                        </v-btn>
                                        <v-btn color="primary" disabled elevation="5" density="compact" v-else>
                                            OK
                                        </v-btn>
                                    </v-card-actions>
                                </v-card>

                            </v-menu>
                        </th>
                        <th>variedad</th>

                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in elementosPackingOrigenFiltradosTemporal" :key="item.id">
                        <td>{{ item.id }}</td>
                        <td>{{ item.fecha }}</td>
                        <td>{{ item.color }}</td>
                        <td>{{ item.variedad }}</td>
                    </tr>
                </tbody>
            </v-table>
        </v-card-text>
    </v-card>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'HelloWorld',

    data: () => ({

        menuCabeceraFecha: false,
        menuCabeceraColor: false,
        mostrarCheckFiltroFechaRevisar: false,
        mostrarCheckFiltroColorRevisar: false,
        bandera_opcion_1: false,
        bandera_opcion_2: false,
        seleccionadosFecha: [],
        seleccionadosColor: [],
        valoresUnicosFecha: [],
        valoresUnicosColor: [],
        /////////////////////////////////////
        cabeceraTest: [{
                title: 'Id',
                key: 'id'
            },
            {
                title: 'fecha',
                key: 'fecha'
            },
            {
                title: 'color',
                key: 'color'
            },
            {
                title: 'variedad',
                key: 'variedad'
            }
        ],
        elementosPackingOrigenFiltrados: [{
                id: '1',
                fecha: '01-01-2025',
                color: 'Azul',
                variedad: 'A'
            },
            {
                id: '2',
                fecha: '01-01-2025',
                color: 'Azul',
                variedad: 'A'
            },
            {
                id: '3',
                fecha: '02-01-2025',
                color: 'Azul',
                variedad: 'A'
            },
            {
                id: '4',
                fecha: '03-01-2025',
                color: 'Amarillo',
                variedad: 'B'
            },
            {
                id: '5',
                fecha: '03-01-2025',
                color: 'Amarillo',
                variedad: 'B'
            },
            {
                id: '6',
                fecha: '03-01-2025',
                color: 'Amarillo',
                variedad: 'B'
            },
            {
                id: '7',
                fecha: '03-01-2025',
                color: 'Amarillo',
                variedad: 'B'
            },
            {
                id: '8',
                fecha: '04-01-2025',
                color: 'Rojo',
                variedad: 'C'
            },
            {
                id: '9',
                fecha: '04-01-2025',
                color: 'Rojo',
                variedad: 'C'
            },
            {
                id: '10',
                fecha: '05-01-2025',
                color: 'Rojo',
                variedad: 'C'
            }
        ],
        elementosPackingOrigenFiltradosTemporal: [],

    }),
    created() {
        this.cccc()
    },

    methods: {
        ordenarListaDeFiltroCabeceraTabla(opcion) {
            /////////////////////// ORDENA DE A - Z Ó DE Z - A /////////////////
            ///////////////////// SE REALIZA POR N COLUMNAS DE LA TABLA PRINCIPAL 
            switch (opcion) {
                case 1:
                    const res1 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => a.fecha.localeCompare(b.fecha));
                    this.elementosPackingOrigenFiltradosTemporal = res1
                    this.menuCabeceraFecha = false
                    break;
                case 2:
                    const res2 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => b.fecha.localeCompare(a.fecha));
                    this.elementosPackingOrigenFiltradosTemporal = res2
                    this.menuCabeceraFecha = false
                    break;
                case 3:
                    const res3 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => a.color.localeCompare(b.color));
                    this.elementosPackingOrigenFiltradosTemporal = res3
                    this.menuCabeceraColor = false
                    break;
                case 4:
                    const res4 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => b.color.localeCompare(a.color));
                    this.elementosPackingOrigenFiltradosTemporal = res4
                    this.menuCabeceraColor = false
                    break;
                case 5:
                    const res5 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => a.variedad.localeCompare(b.variedad));
                    this.elementosPackingOrigenFiltradosTemporal = res5
                    this.menuCabeceraVariedad = false
                    break;
                case 6:
                    const res6 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => b.variedad.localeCompare(a.variedad));
                    this.elementosPackingOrigenFiltradosTemporal = res6
                    this.menuCabeceraVariedad = false
                    break;
                case 7:
                    const res7 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => a.long.localeCompare(b.long));
                    this.elementosPackingOrigenFiltradosTemporal = res7
                    this.menuCabeceraLongitud = false
                    break;
                case 8:
                    const res8 = this.elementosPackingOrigenFiltradosTemporal.sort((a, b) => b.long.localeCompare(a.long));
                    this.elementosPackingOrigenFiltradosTemporal = res8
                    this.menuCabeceraLongitud = false
                    break;

                default:
                    break;
            }
        },

        inicializarListaDeFiltroCabeceraTabla(bandera_opcion, oo) {
            /////////////////////// FUNCIO PARA SELECCIONAR TODO Y DESELECCIONAR TODOS LOS CAMPOS DEL FILTRO  /////////////////
            ///////////////////// SE REALIZA POR N COLUMNAS DE LA TABLA TEMPORAL DE CABECERAS
            switch (oo) {
                case 1:
                    if (bandera_opcion) {
                        this.seleccionadosFecha = []
                    } else {
                        this.seleccionadosFecha = this.valoresUnicosFecha
                    }
                    break;
                case 2:
                    if (bandera_opcion) {
                        this.seleccionadosColor = []
                    } else {
                        this.seleccionadosColor = this.valoresUnicosColor
                    }
                    break;
                case 3:
                    if (bandera_opcion) {
                        this.seleccionadosVariedad = []
                    } else {
                        this.seleccionadosVariedad = this.valoresUnicosVariedad
                    }
                    break;
                case 4:
                    if (bandera_opcion) {
                        this.seleccionadosLongitud = []
                    } else {
                        this.seleccionadosLongitud = this.valoresUnicosLongitud
                    }
                    break;

                default:
                    break;
            }
        },
        filtrarUltimaTotal() {
            if (this.mostrarCheckFiltroFechaRevisar) {
                const filtroDesdeTabla = this.elementosVectorFiltroFechaTemporal
                const elementosFiltrar = this.elementosPackingOrigenFiltradosTemporal

                function filtrarTabla(array, filtro) {
                    return array.filter(elem => filtro.includes(elem.fecha))
                }
                this.elementosPackingOrigenFiltradosTemporal = filtrarTabla(elementosFiltrar, filtroDesdeTabla)

                console.log("Fecha2")
                console.log(this.elementosPackingOrigenFiltradosTemporal)
                console.log("Fecha2")
            }
            if (this.mostrarCheckFiltroColorRevisar) {
                const filtroDesdeTabla2 = this.elementosVectorFiltroColorTemporal
                const elementosFiltrar2 = this.elementosPackingOrigenFiltradosTemporal

                function filtrarTabla2(array2, filtro2) {
                    return array2.filter(elem => filtro2.includes(elem.color))
                }
                this.elementosPackingOrigenFiltradosTemporal = filtrarTabla2(elementosFiltrar2, filtroDesdeTabla2)
                console.log("Color2")
                console.log(this.elementosPackingOrigenFiltradosTemporal)
                console.log("Color2")
            }
            if (this.mostrarCheckFiltroVariedadRevisar) {
                const filtroDesdeTabla2 = this.elementosVectorFiltroVariedadTemporal
                const elementosFiltrar2 = this.elementosPackingOrigenFiltradosTemporal

                function filtrarTabla2(array2, filtro2) {
                    return array2.filter(elem => filtro2.includes(elem.variedad))
                }
                this.elementosPackingOrigenFiltradosTemporal = filtrarTabla2(elementosFiltrar2, filtroDesdeTabla2)
                console.log("variedad2")
                console.log(this.elementosPackingOrigenFiltradosTemporal)
                console.log("variedad2")
            }
            if (this.mostrarCheckFiltroLongitudRevisar) {
                const filtroDesdeTabla2 = this.elementosVectorFiltroLongitudTemporal
                const elementosFiltrar2 = this.elementosPackingOrigenFiltradosTemporal

                function filtrarTabla2(array2, filtro2) {
                    return array2.filter(elem => filtro2.includes(elem.long))
                }
                this.elementosPackingOrigenFiltradosTemporal = filtrarTabla2(elementosFiltrar2, filtroDesdeTabla2)
                console.log("Long2")
                console.log(this.elementosPackingOrigenFiltradosTemporal)
                console.log("Long2")
            }
        },
        filterItemsNuevo2: function (arr2) {
            if (arr2.length == 0) {
                this.elementosVectorFiltroColorTemporal = []
                this.mostrarCheckFiltroColorRevisar = false
                //this.filtrarUltimaTotalOtroInicioNuevo()
            } else {
                this.elementosVectorFiltroColorTemporal = arr2
                this.mostrarCheckFiltroColorRevisar = true
                const filtroDesdeTabla = arr2
                const elementosFiltrar = this.elementosPackingOrigenFiltrados

                function filtrarTabla(array, filtro) {
                    return array.filter(elem => filtro.includes(elem.color))
                }
                this.elementosPackingOrigenFiltradosTemporal = filtrarTabla(elementosFiltrar, filtroDesdeTabla)
                //   this.filtroNuevo(1, this.elementosPackingOrigenFiltradosTemporal)
                this.filtrarUltimaTotal()
            }
        },

        filterItemsNuevo: function (arr2) {
            if (arr2.length == 0) {
                this.elementosVectorFiltroFechaTemporal = []
                this.mostrarCheckFiltroFechaRevisar = false
                //this.filtrarUltimaTotalOtroInicioNuevo()
            } else {
                this.elementosVectorFiltroFechaTemporal = arr2
                this.mostrarCheckFiltroFechaRevisar = true
                const filtroDesdeTabla = arr2
                const elementosFiltrar = this.elementosPackingOrigenFiltrados

                function filtrarTabla(array, filtro) {
                    return array.filter(elem => filtro.includes(elem.fecha))
                }
                this.elementosPackingOrigenFiltradosTemporal = filtrarTabla(elementosFiltrar, filtroDesdeTabla)
                //   this.filtroNuevo(1, this.elementosPackingOrigenFiltradosTemporal)
                this.filtrarUltimaTotal()
            }
        },

        filtroNuevo(opcion, vector) {
            switch (opcion) {
                case 1:
                    let elementosVectorUnicoFecha = [],
                        elementosVectorUnicoColor = [],
                        elementosVectorUnicoVariedad = [],
                        elementosVectorUnicoLong = []

                    var doubles = vector.map(function (x) {
                        elementosVectorUnicoFecha.push(x.fecha)
                        elementosVectorUnicoColor.push((x.color).trim())
                        elementosVectorUnicoVariedad.push(x.variedad)
                        elementosVectorUnicoLong.push(x.long)
                    });

                    function onlyUniqueArray(value, index, self) {
                        return self.indexOf(value) === index;
                    }
                    var valoresUnicosFecha = elementosVectorUnicoFecha.filter(onlyUniqueArray);
                    var valoresUnicosColor = elementosVectorUnicoColor.filter(onlyUniqueArray);
                    var valoresUnicosVariedad = elementosVectorUnicoVariedad.filter(onlyUniqueArray);
                    var valoresUnicosLong = elementosVectorUnicoLong.filter(onlyUniqueArray);

                    this.valoresUnicosFecha = valoresUnicosFecha
                    this.valoresUnicosColor = valoresUnicosColor
                    this.valoresUnicosVariedad = valoresUnicosVariedad
                    this.valoresUnicosLongitud = valoresUnicosLong

                    this.seleccionadosFecha = this.valoresUnicosFecha
                    this.seleccionadosColor = this.valoresUnicosColor
                    this.seleccionadosVariedad = this.valoresUnicosVariedad
                    this.seleccionadosLongitud = this.valoresUnicosLongitud

                    break;

                default:
                    break;
            }
        },
        reiniciarFiltros() {
            this.mostrarCheckFiltroFechaRevisar = false
            this.mostrarCheckFiltroColorRevisar = false
            this.mostrarCheckFiltroVariedadRevisar = false
            this.mostrarCheckFiltroLongitudRevisar = false

            this.seleccionadosFecha = []
            this.seleccionadosColor = []
            this.seleccionadosVariedad = []
            this.seleccionadosLongitud = []
            this.elementosPackingOrigenFiltradosTemporal = this.elementosPackingOrigenFiltrados
            this.filtroNuevo(1, this.elementosPackingOrigenFiltrados)
        },
        cccc() {
            this.elementosPackingOrigenFiltradosTemporal = this.elementosPackingOrigenFiltrados
            this.filtroNuevo(1, this.elementosPackingOrigenFiltrados)
        },

        /////////////////////////////////
        traerLista() {
            axios.get('')
                .then(res => {
                    console.log(res)
                })
                .catch(err => {
                    console.error(err);
                })
        },

    },
}
</script>
