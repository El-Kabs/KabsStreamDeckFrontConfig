<template>
  <div class="center">
    <div class="grid deck">
      <vs-row class="fila">
          <vs-col w="2" v-for="boton in botonesU" :key="boton.boton">
            <vs-button class="boton" floating color="#3F618C" border>
              <div v-if="boton.imagen !== undefined">
                  <img class="imagen" v-bind:src="'http://localhost:5000/' + boton.imagen" alt="" :key="boton.imagen"/>
              </div>
            </vs-button>
          </vs-col>
      </vs-row>

      <vs-row class="fila">
        <vs-col w="2" v-for="boton in botonesD" :key="boton.boton">
          <vs-button class="boton" floating color="#3F618C" border>
            <div v-if="boton.imagen !== undefined">
              <img
                class="imagen"
                v-bind:src="'http://localhost:5000/' + boton.imagen"
                alt=""
              />
            </div>
          </vs-button>
        </vs-col>
      </vs-row>

      <vs-row class="fila">
        <vs-col w="2" v-for="boton in botonesT" :key="boton.boton">
          <vs-button class="boton" floating color="#3F618C" border>
            <div v-if="boton.imagen !== undefined">
              <img
                class="imagen"
                v-bind:src="'http://localhost:5000/' + boton.imagen"
                alt=""
              />
            </div>
          </vs-button>
        </vs-col>
      </vs-row>
    </div>
    <vs-button class="b1" floating color="#3F618C" icon @click="perfil(1)">
      1
    </vs-button>
    <vs-button class="b2" floating color="#3F618C" icon @click="perfil(2)">
      2
    </vs-button>
    <vs-button class="b3" floating color="#3F618C" icon @click="perfil(3)">
      3
    </vs-button>
    <vs-button class="b4" floating color="#3F618C" icon @click="perfil(4)">
      4
    </vs-button>
    <vs-button class="b5" floating color="#3F618C" icon @click="perfil(5)">
      5
    </vs-button>
  </div>
</template>

<script>
export default {
  name: "Deck",
  data: () => ({
    active: 0,
    botones: [],
    botonesU: [],
    botonesD: [],
    botonesT: [],
    perfilNum: 1
  }),
  mounted: function () {
    const _this = this;
    var perf = _this.perfilNum;
    fetch("http://localhost:5000/botones?perfil=" + perf)
      .then((response) => response.json())
      .then((data) => {
        _this.botones = data;
        _this.botonesU = data.slice(0, 5);
        _this.botonesD = data.slice(5, 10);
        _this.botonesT = data.slice(10, 15);
      });
      document.title = 'Config - Stream Deck'
  },
  methods: {
    perfil(numPerfil) {
      const _this = this;
      _this.perfilNum = numPerfil;
      fetch("http://localhost:5000/botones?perfil=" + numPerfil)
        .then((response) => response.json())
        .then((data) => {
          _this.botones = data;
          _this.botonesU = data.slice(0, 5);
          _this.botonesD = data.slice(5, 10);
          _this.botonesT = data.slice(10, 15);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.boton {
  width: 108px;
  height: 108px;
  background: transparent !important;
}

.deck {
  margin: 0 auto;
  margin-left: 350px;
}

.fila {
  margin-top: 100px;
}

.imagen {
  max-width: 108px !important;
  max-height: 108px !important;
}

.b1 {
  width: 35px;
  height: 35px;
  position: absolute;
  top: 200px;
  right: 40px;
}

.b2 {
  width: 35px;
  height: 35px;
  position: absolute;
  top: 250px;
  right: 40px;
}

.b3 {
  width: 35px;
  height: 35px;
  position: absolute;
  top: 300px;
  right: 40px;
}

.b4 {
  width: 35px;
  height: 35px;
  position: absolute;
  top: 350px;
  right: 40px;
}

.b5 {
  width: 35px;
  height: 35px;
  position: absolute;
  top: 400px;
  right: 40px;
}

</style>
