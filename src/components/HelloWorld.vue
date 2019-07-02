<template>
  <div class="container">
    <section>
      <b-tabs>
        <b-tab-item label="Calcular fuerza eléctrica">
          <br>
          <div class="columns">
            <div class="column is-4">
              <b-field label="Cantidad de cargas">
                <b-input
                  v-model="cantidadCargas"
                  placeholder="Obligatorio"
                  required
                  type="number"
                  min="1"
                  max="100"
                ></b-input>
              </b-field>
              <b-button type="is-primary" @click="addCargas">Ingresar cargas</b-button>
            </div>
            <div class="column">
              <b-message title="Resultado" v-if="selected && resultObject">
                <b>Fx</b>
                : {{resultObject.fuerzaComponenteX}} N
                <b>Fy</b>
                : {{resultObject.fuerzaComponenteY}} N
                <b>Fz</b>
                : {{resultObject.fuerzaComponenteZ}} N
                <b>Fe</b>
                : {{resultObject.fuerzaElectricaCargaSeleccionada}} N
              </b-message>
            </div>
          </div>
          <div class="columns">
            <div class="column">
              <b-table :data="cargas" :selected.sync="selected">
                <template slot-scope="props">
                  <b-table-column label="Nombre" width="40">{{ props.row.nombre }}</b-table-column>
                  <b-table-column label="Valor" width="40">
                    <b-input
                      v-model="props.row.valor"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="X" width="40">
                    <b-input
                      v-model="props.row.coordernadas[0]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="Y" width="40">
                    <b-input
                      v-model="props.row.coordernadas[1]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="Z" width="40">
                    <b-input
                      v-model="props.row.coordernadas[2]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                </template>
              </b-table>
            </div>
          </div>
          <b-button type="is-primary" v-if="cargas.length && selected" @click="calcular">Calcular FE</b-button>
        </b-tab-item>
        <b-tab-item label="Calcular campo eléctrico">
          <br>
              <div class="columns">
            <div class="column is-4">
              <b-field label="Punto en x">
                <b-input
                  v-model="coordernadasPunto[0]"
                  placeholder="Obligatorio"
                  required
                  type="number"
                ></b-input>
              </b-field>
            </div>
            <div class="column is-4">
              <b-field label="Punto en y">
                <b-input
                  v-model="coordernadasPunto[1]"
                  placeholder="Obligatorio"
                  required
                  type="number"
                ></b-input>
              </b-field>
            </div>
            <div class="column is-4">
              <b-field label="Punto en z">
                <b-input
                  v-model="coordernadasPunto[2]"
                  placeholder="Obligatorio"
                  required
                  type="number"
                ></b-input>
              </b-field>
            </div>
          </div>
          <div class="columns">
            <div class="column is-4">
              <b-field label="Cantidad de cargas">
                <b-input
                  v-model="cantidadCargas2"
                  placeholder="Obligatorio"
                  required
                  type="number"
                  min="1"
                  max="100"
                ></b-input>
              </b-field>
            </div>
            <div class="column">
              <b-message title="Resultado" v-if="resultObject2">
                <b>Ex</b>
                : {{resultObject2.campoElectricoX}} N/C
                <b>Ey</b>
                : {{resultObject2.campoElectricoY}} N/C
                <b>Ez</b>
                : {{resultObject2.campoElectricoZ}} N/C
                <b>E</b>
                : {{resultObject2.campoElectrico}} N/C
              </b-message>
            </div>
          </div>
      
          <b-button type="is-primary" @click="addCargas2">Ingresar cargas</b-button>

          <div class="columns">
            <div class="column">
              <b-table :data="cargas2">
                <template slot-scope="props">
                  <b-table-column label="Nombre" width="40">{{ props.row.nombre }}</b-table-column>
                  <b-table-column label="Valor" width="40">
                    <b-input
                      v-model="props.row.valor"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="X" width="40">
                    <b-input
                      v-model="props.row.coordernadas[0]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="Y" width="40">
                    <b-input
                      v-model="props.row.coordernadas[1]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="Z" width="40">
                    <b-input
                      v-model="props.row.coordernadas[2]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                </template>
              </b-table>
            </div>
          </div>
          <b-button type="is-primary" v-if="cargas2.length" @click="calcular2">Calcular E</b-button>
        </b-tab-item>

         <b-tab-item label="Calcular energía potencial">
          <br>
          <div class="columns">
            <div class="column is-4">
              <b-field label="Cantidad de cargas">
                <b-input
                  v-model="cantidadCargas3"
                  placeholder="Obligatorio"
                  required
                  type="number"
                  min="1"
                  max="100"
                ></b-input>
              </b-field>
              <b-button type="is-primary" @click="addCargas3">Ingresar cargas</b-button>
            </div>
            <div class="column">
              <b-message title="Resultado" v-if="resultObject3">
                <b>U</b>
                : {{resultObject3}} J
              </b-message>
            </div>
          </div>
          <div class="columns">
            <div class="column">
              <b-table :data="cargas3" >
                <template slot-scope="props">
                  <b-table-column label="Nombre" width="40">{{ props.row.nombre }}</b-table-column>
                  <b-table-column label="Valor" width="40">
                    <b-input
                      v-model="props.row.valor"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="X" width="40">
                    <b-input
                      v-model="props.row.coordernadas[0]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="Y" width="40">
                    <b-input
                      v-model="props.row.coordernadas[1]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                  <b-table-column label="Z" width="40">
                    <b-input
                      v-model="props.row.coordernadas[2]"
                      placeholder="Obligatorio"
                      required
                      type="number"
                    ></b-input>
                  </b-table-column>
                </template>
              </b-table>
            </div>
          </div>
          <b-button type="is-primary" v-if="cargas3.length" @click="calcular3">Calcular U</b-button>
        </b-tab-item>
      </b-tabs>
    </section>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      cargas: [],
      cantidadCargas: null,
      selected: null,
      resultObject: null,

      cargas2: [],
      coordernadasPunto: [0, 0, 0],
      cantidadCargas2: null,
      selected2: null,
      resultObject2: null,

      cargas3: [],
      cantidadCargas3: null,
      resultObject3: null,

      k: 8.99 * Math.pow(10, 9),
      kEnergiaPotencial: 9 * Math.pow(10, -1)
    };
  },
  methods: {
    calcular() {
      if (this.selected) {
        this.resultObject = this.calcularFuerzaElectrica(
          this.cargas,
          this.selected
        );
      }
    },
     calcular2() {
      this.resultObject2 = this.calcularCampoElectrico(
        this.cargas2,
        this.coordernadasPunto
      );
    },
    calcular3() {
      this.resultObject3 = this.calcularEnergiaPotencial(
        this.cargas3,
        this.selected
      );
    },
    addCargas() {
      this.cargas = [];
      for (let i = 1; i <= this.cantidadCargas; i++) {
        this.cargas.push({
          nombre: "Q" + i,
          valor: 0,
          coordernadas: [0, 0, 0]
        });
      }
    },
    addCargas2() {
      this.cargas2 = [];
      for (let i = 1; i <= this.cantidadCargas2; i++) {
        this.cargas2.push({
          nombre: "Q" + i,
          valor: 0,
          coordernadas: [0, 0, 0]
        });
      }
    },
     addCargas3() {
      this.cargas3 = [];
      for (let i = 1; i <= this.cantidadCargas3; i++) {
        this.cargas3.push({
          nombre: "Q" + i,
          valor: 0,
          coordernadas: [0, 0, 0]
        });
      }
    },

    calcularCampoElectrico(cargasInfo, puntoParaCalcular) {
      let campoElectricoX = 0,
        campoElectricoY = 0,
        campoElectricoZ = 0;

      for (var i = 0; i < cargasInfo.length; i++) {
        let carga = cargasInfo[i];
        var coordenadaCargaActual = this.obtenerCoordsCargaSeleccionada(carga);
        var valorCargaActual = this.obtenerValodeCargaSeleccionada(carga); // assume charges in micro coulombs

        var distanciaEntreCargas = this.obtenerDistanciasEntreDosCargas(
          coordenadaCargaActual,
          puntoParaCalcular
        );
        if (distanciaEntreCargas === 0) {
          this.$toast.open({
            duration: 3000,
            message: `No se puede repetir la mismas posiciones por cargas`,
            position: "is-bottom",
            type: "is-danger"
          });
          break;
        }

        campoElectricoX +=
          (valorCargaActual / Math.pow(distanciaEntreCargas, 3)) *
          (puntoParaCalcular[0] - coordenadaCargaActual[0]);
        campoElectricoY +=
          (valorCargaActual / Math.pow(distanciaEntreCargas, 3)) *
          (puntoParaCalcular[1] - coordenadaCargaActual[1]);
        campoElectricoZ +=
          (valorCargaActual / Math.pow(distanciaEntreCargas, 3)) *
          (puntoParaCalcular[2] - coordenadaCargaActual[2]);
      }

      campoElectricoX *= this.k;
      campoElectricoY *= this.k;
      campoElectricoZ *= this.k;

      var campoElectrico = Math.sqrt(
        Math.pow(campoElectricoX, 2) +
          Math.pow(campoElectricoY, 2) +
          Math.pow(campoElectricoZ, 2)
      );

      console.info(
        campoElectricoX.toExponential(3),
        campoElectricoY.toExponential(3),
        campoElectricoZ.toExponential(3),
        campoElectrico.toExponential(3)
      );
      return {
        campoElectricoX: campoElectricoX.toExponential(3),
        campoElectricoY: campoElectricoY.toExponential(3),
        campoElectricoZ: campoElectricoZ.toExponential(3),
        campoElectrico: campoElectrico.toExponential(3)
      };
    },

    calcularFuerzaElectrica(cargasInfo, cargaACalcular) {
      let coordernadasCargaSeleccionada = this.obtenerCoordsCargaSeleccionada(
        cargaACalcular
      );
      let fuerzaComponenteX = 0,
        fuerzaComponenteY = 0,
        fuerzaComponenteZ = 0;

      let valorCargaSeleccionada = this.obtenerValodeCargaSeleccionada(
        cargaACalcular
      );
      let valorAbsCargaSeleccionada = Math.abs(valorCargaSeleccionada);

      for (var i = 0; i < cargasInfo.length; i++) {
        let carga = cargasInfo[i];

        if (
          carga.nombre !== undefined &&
          carga.nombre === cargaACalcular.nombre
        )
          continue;

        var coordenadaCargaActual = this.obtenerCoordsCargaSeleccionada(carga);
        var valorCargaActual = this.obtenerValodeCargaSeleccionada(carga); // assume charges in micro coulombs

        var distanciaEntreCargas = this.obtenerDistanciasEntreDosCargas(
          coordenadaCargaActual,
          coordernadasCargaSeleccionada
        );
        if (distanciaEntreCargas === 0) {
          this.$toast.open({
            duration: 3000,
            message: `No se puede repetir la mismas posiciones por cargas`,
            position: "is-bottom",
            type: "is-danger"
          });
          break;
        }
        var valorAbsCargaActual = Math.abs(valorCargaActual);
        var seAtraen = valorCargaSeleccionada * valorCargaActual < 0;
        fuerzaComponenteX +=
          (valorAbsCargaActual / Math.pow(distanciaEntreCargas, 3)) *
          (coordernadasCargaSeleccionada[0] - coordenadaCargaActual[0]) *
          (seAtraen ? -1 : 1);
        fuerzaComponenteY +=
          (valorAbsCargaActual / Math.pow(distanciaEntreCargas, 3)) *
          (coordernadasCargaSeleccionada[1] - coordenadaCargaActual[1]) *
          (seAtraen ? -1 : 1);
        fuerzaComponenteZ +=
          (valorAbsCargaActual / Math.pow(distanciaEntreCargas, 3)) *
          (coordernadasCargaSeleccionada[2] - coordenadaCargaActual[2]) *
          (seAtraen ? -1 : 1);
      }

      let factorComun = this.k * valorAbsCargaSeleccionada;
      fuerzaComponenteX *= factorComun;
      fuerzaComponenteY *= factorComun;
      fuerzaComponenteZ *= factorComun;

      var fuerzaElectricaCargaSeleccionada = Math.sqrt(
        Math.pow(fuerzaComponenteX, 2) +
          Math.pow(fuerzaComponenteY, 2) +
          Math.pow(fuerzaComponenteZ, 2)
      );

      console.info(
        fuerzaComponenteX.toExponential(3),
        fuerzaComponenteY.toExponential(3),
        fuerzaComponenteZ.toExponential(3),
        fuerzaElectricaCargaSeleccionada.toExponential(3)
      );

      return {
        fuerzaComponenteX: fuerzaComponenteX.toExponential(3),
        fuerzaComponenteY: fuerzaComponenteY.toExponential(3),
        fuerzaComponenteZ: fuerzaComponenteZ.toExponential(3),
        fuerzaElectricaCargaSeleccionada: fuerzaElectricaCargaSeleccionada.toExponential(
          3
        )
      };
    },
    calcularEnergiaPotencial(cargasInfo) {
      
      var valores = [];

      for (var i = 0; i < cargasInfo.length; i++) {
        let carga = cargasInfo[i];
        var coordenadaCargaActual = this.obtenerCoordsCargaSeleccionada(carga);
        var valorCargaActual = this.obtenerValodeCargaSeleccionada(carga); // assume charges in micro coulombs

        for (let y = 0; y < cargasInfo.length; y++) {
          if(i != y && i > y){
            const cargaHermana = cargasInfo[y];
            var coordenadaCargaActual2 = this.obtenerCoordsCargaSeleccionada(cargaHermana);
            var valorCargaActual2 = this.obtenerValodeCargaSeleccionada(cargaHermana); // assume charges in micro coulombs

           var distanciaEntreCargas = this.obtenerDistanciasEntreDosCargas(
              coordenadaCargaActual,
              coordenadaCargaActual2
           );
          
           var valor = (valorCargaActual * valorCargaActual2)/distanciaEntreCargas;
           
           valores.push(valor);
          }
        }
      }
      return (valores.reduce((x, y)=>{ return x + y; }, 0) * this.kEnergiaPotencial).toExponential(3);
    },

    obtenerDistanciasEntreDosCargas(carga1, carga2) {
      return Math.sqrt(
        Math.pow(carga1[0] - carga2[0], 2) +
          Math.pow(carga1[1] - carga2[1], 2) +
          Math.pow(carga1[2] - carga2[2], 2)
      );
    },

    obtenerCoordsCargaSeleccionada(cargaACalcular) {
      return cargaACalcular.coordernadas;
    },

    obtenerValodeCargaSeleccionada(cargaACalcular) {
      return cargaACalcular.valor * Math.pow(10, -6);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
