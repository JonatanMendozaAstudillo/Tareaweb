<template>
  <div class="card">
    <div class="card-header">
      <div class="d-flex justify-content-between">
        <span class="container-nameList">Listado de Usuarios</span>
        <div class="btn btn-primary px-5" v-on:click='viewForm = true, resetInputs()'>Agregar usuario</div>
      </div>
      
    </div>
    <div class="card-body">
      <div v-if='viewForm'>
        <div class="row">
          <div class="col-3">
            <input type="text" v-model='user.nombre' class='ph-center form-control' placeholder='nombre'>
          </div>
          <div class="col-3">
            <input type="text" v-model='user.apellidos' class='ph-center form-control' placeholder='apellidos'>
          </div>
          <div class="col-3">
            <input type="text" v-model='user.telefono' class='ph-center form-control' placeholder='telefono'>
          </div>
          <div class="col-3">
            <input type="text" v-model='user.correo' class='ph-center form-control' placeholder='correo'>
          </div>
        </div>

        <div class="d-flex mt-4 mb-5">
          <div class="me-3">
            <div class="btn btn-info py-1 px-5" @click='store()' v-if='create'>Guardar</div>
            <div class="btn btn-info py-1 px-5" @click='update()' v-else>Actualizar</div>
          </div>
          <div class="">
            <div class="btn btn-danger py-1 px-5" @click='viewForm = false'>Cancelar</div>
          </div>
        </div>
      </div>

      <div v-if='users.length == 0'>
        <div class="no-users d-flex justify-content-center align-items-center">
          Aun no hay usuarios agregados
        </div>
      </div>

      <div v-else>
        <table class="table table-striped mt-2">
          <thead class="table-head">
            <tr>
              <th class="table-tittle">Opciones</th>
              <th class="table-tittle">Nombre</th>
              <th class="table-tittle">Telefono</th>
              <th class="table-tittle">Correo</th>
            </tr>
          </thead>
          <tbody class="table-body">
            <tr v-for="user in users" :key='user'>
              <td>
                <fas icon="edit" class="iconEdit" @click="edit(user)"/>
                <fas icon="trash" class="iconTrash" @click="erase(user.id)"/>
              </td>
              <td>{{ completeName( user ) }}</td>
              <td>{{ user.telefono }}</td>
              <td>{{ user.correo }}</td>
            </tr>
          </tbody>
        </table>
      </div> 
      
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      viewForm: false,
      users: [],
      user: {
        nombre: '',
        apellidos: '',
        telefono: '',
        correo: ''
      },
      create: true,
      userEditID: 0,
    }
  },
  methods: {
    completeName (el) {
      let datoNombre = el.nombre.split(' ')
      //console.log(datoNombre);
      
      var element
      var nombres = ""

      for (let i = 0; i < datoNombre.length; i++) {
        element = `${datoNombre[i].charAt(0).toUpperCase()}${datoNombre[i].slice(1)}${' '}`
        nombres += element
        //console.log(nombres)
      }

      let datoApellido = el.apellidos.split(' ')
      //console.log(datoApellido);
      var element2
      var apellidos = ""

      for (let i = 0; i < datoApellido.length; i++) {
        element2 = `${datoApellido[i].charAt(0).toUpperCase()}${datoApellido[i].slice(1)}${' '}`
        apellidos += element2
        //console.log(apellidos)
      }
      
      // let nombre = `${el.nombre.charAt(0).toUpperCase()}${el.nombre.slice(1)}`,
      //     apellidos = el.apellidos.charAt(0).toUpperCase() + el.apellidos.slice(1)
          
      return `${nombres} ${apellidos}`
    },
    store() { 
      let newUser = {
        id: this.users.length+1,
        nombre: this.user.nombre,
        apellidos: this.user.apellidos,
        telefono: this.user.telefono,
        correo: this.user.correo
      }
      this.users.push( newUser)
      
    }
   
  }
}
</script>
