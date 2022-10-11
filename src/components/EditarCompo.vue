<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Editar Empleados</div>
      <div class="card-body">
        <form v-on:submit.prevent="actualizarRegistro">
          <div class="form-group">
            <label for="nombre">Nombre</label>
            <input
              type="text"
              class="form-control"
              name="nombre"
              id="nombre"
              required
              v-model="empleado.nombre"
              aria-describedby="helpId"
              placeholder=""
            />
            <small id="helpId" class="form-text text-muted"
              >Escribe el nombre del empleado</small
            >
          </div>
          <div class="form-group">
            <label for="correo">Correo</label>
            <input
              type="email"
              class="form-control"
              name="correo"
              id="correo"
              required
              v-model="empleado.correo"
              aria-describedby="helpId"
              placeholder=""
            />
            <small id="helpId" class="form-text text-muted"
              >Escribe el correo del empleado</small
            >
          </div>
          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-primary">Modificar</button>
            <router-link :to="{ name: 'Listar' }" class="btn btn-warning"
              >Cancelar</router-link
            >
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      empleado: [],
    };
  },
  created: function () {
    this.obtenerInformacionID();
  },
  methods: {
    obtenerInformacionID() {
      fetch(
        "http://localhost/back-empleados/?consultar=" + this.$route.params.id
      )
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
          if (typeof datosRespuesta[0].success === "undefined") {
            this.empleado = datosRespuesta[0];
          }
        })
        .catch((e) => console.log(e));
    },
    actualizarRegistro() {
      var datosEnviar = {
        id: this.$route.params.id,
        nombre: this.empleado.nombre,
        correo: this.empleado.correo,
      };
      fetch("http://localhost/back-empleados/?actualizar="+this.$route.params.id, {
        method: "POST",
        body: JSON.stringify(datosEnviar),
      })
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
          console.log(datosRespuesta);
          window.location.href = "../listar";
        });
    },
  },
};
</script>
