<template>
  <vs-dialog
    color="#012340"
    width="100px"
    v-model="active"
    v-on:close="close"
    v-on:abrir-dialog="open"
  >
    <h3 style="color: #f4f7f8">Cambiar color</h3>
    <div class="con-form" style="">
      <vs-input
        color="#3F618C"
        v-model="titulo"
        placeholder="Titulo"
        class="inputDialog"
      >
      </vs-input>

      <input id="file" type="file" @change="fileSelected" hidden />
      <vs-button
        color="#3F618C"
        class="buttonDialog"
        @click="chooseFiles"
        border
        >Imagen</vs-button
      >

      <vs-select placeholder="Boton" v-model="boton" style="margin-top: 15px">
        <vs-option
          v-for="index in 15"
          :key="index"
          v-bind:label="index"
          v-bind:value="index"
        >
          {{ index }}
        </vs-option>
      </vs-select>
      <vs-button
        color="#3F618C"
        border
        @click="guardarBoton"
        style="margin-top: 15px"
        >Guardar</vs-button
      >
    </div>
  </vs-dialog>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    titulo: "",
    boton: 0,
    imagen: ""
  }),
  props: {
    active: {
      required: true
    }
  },
  methods: {
    fileSelected(evt) {
      var pathImagen = evt["target"]["files"][0];
      this.imagen = pathImagen;
    },
    chooseFiles() {
      document.getElementById("file").click();
    },
    async guardarBoton() {
      const _this = this;
      let data = new FormData();
      data.append("file", this.imagen);

      let config = {
        header: {
          "Content-Type": "image/png",
        },
      };
      await axios
        .post("http://localhost:5000/upload", data, config)
        .then((response) => response.data)
        .then((resp) => {
          var dataBotones = {
            pos: parseInt(_this.boton),
            data: {
              imagen: resp["path"],
              titulo: _this.titulo,
              func: "cambiarColor",
            },
          };
          axios
            .post("http://localhost:5000/botones", dataBotones)
            .then((response) => response.data)
            .then((resp) => {
              if (resp["boton"] == parseInt(_this.boton)) {
                window.location.reload();
              }
            });
        });
    },
    close() {
      this.$emit("update-close", false);
    },
    open() {
      this.active = true;
    },
  },
};
</script>

<style scoped>
.inputDialog {
  margin-top: 15px;
}
.buttonDialog {
  margin-top: 15px;
}
</style>