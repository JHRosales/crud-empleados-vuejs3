<template>
  <div class="container">
    Crear Jhimi Rosales.
    <div class="card">
      <div class="card-header">Agregar Nuevos Empleados</div>
      <div class="card-body">
        <form v-on:submit.prevent="agregarRegistro">
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
            <button type="submit" class="btn btn-primary">Agregar</button>
            <router-link :to="{name:'Listar'}" class="btn btn-warning">Cancelar</router-link>
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
  methods: {
    agregarRegistro() {
      console.log(this.empleado);
      var datosEnviar = {
        nombre: this.empleado.nombre,
        correo: this.empleado.correo,
      };
      fetch("http://localhost/back-empleados/?insertar=1", {
        method: "POST",
        body: JSON.stringify(datosEnviar),
      })
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
          console.log(datosRespuesta);
          window.location.href = "listar";
        });
    },
  },
};
</script>
