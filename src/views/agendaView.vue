<template>
   <div>
      <h1>{{ titulo }}</h1>
      <div>
        Filtro:<input v-model="buscador" type="text" placeholder="Buscar contacto">
        <ul>
          <li v-for="contacto in contactosFiltrados" :key="contacto.id">
            {{ contacto.nombre }}
          </li>
        </ul>
      </div>
      
      <table>
        <thead>
            <tr>
                <th>id</th>
                <th>nombre</th>
                <th>email</th>
                <th>direccion</th>
                <th>telefono</th>
                <th>pais</th>
                <th>ciudad</th>
                <th></th>
            </tr>
            <tr>
                <th><input type="text" v-model="contactoNuevoOb.id"></th>
                <th><input type="text" v-model="contactoNuevoOb.nombre"></th>
                <th><input type="text" v-model="contactoNuevoOb.email"></th>
                <th><input type="text" v-model="contactoNuevoOb.direccion"></th>
                <th><input type="text" v-model="contactoNuevoOb.telefono"></th>
                <th><input type="text" v-model="contactoNuevoOb.pais"></th>
                <th><input type="text" v-model="contactoNuevoOb.ciudad"></th>
                <th><button @click="guardarNuevo()">Agregar</button></th>
            </tr>
            <tr v-if="indexParaEditar != null">
                <th><input type="text" v-model="contactoEdicionOb.id"></th>
                <th><input type="text" v-model="contactoEdicionOb.nombre"></th>
                <th><input type="text" v-model="contactoEdicionOb.email"></th>
                <th><input type="text" v-model="contactoEdicionOb.direccion"></th>
                <th><input type="text" v-model="contactoEdicionOb.telefono"></th>
                <th><input type="text" v-model="contactoEdicionOb.pais"></th>
                <th><input type="text" v-model="contactoEdicionOb.ciudad"></th>
                <th><button @click="guardarEdicion()">Actualizar</button></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(contacto, index) in contactos" :key="contacto.id">
                <td>{{ contacto.id }}</td>
                <td>{{ contacto.nombre }}</td>
                <td>{{ contacto.email }}</td>
                <td>{{ contacto.direccion }}</td>
                <td>{{ contacto.telefono }}</td>
                <td>{{ contacto.pais }}</td>
                <td>{{ contacto.ciudad }}</td>
                <td>
                  <button @click="eliminarContacto(index)">Eliminar</button>
                  <button @click="editarContacto(contacto, index)">Editar</button>
                </td>
            </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MiComponente',
    data() {
      return {
        titulo: 'Registro de Contactos',
        contactoNuevoOb: {
             id: "",
             nombre: "", 
             email: "", 
             direccion: "", 
             telefono: "", 
             pais: "", 
             ciudad: "" 
        },
        contactoEdicionOb: {
             id: "",
             nombre: "", 
             email: "", 
             direccion: "", 
             telefono: "", 
             pais: "", 
             ciudad: "" 
        },
        indexParaEditar: null,
        buscador: "",
        contactos: [
        { id: "1", nombre: "Juan Perez", email: "juan@juan.com", direccion: "av. Villazon", telefono: "65825417", pais: "Bolivia", ciudad: "Cbba" },
        { id: "2", nombre: "Yoni Salamanca", email: "yoni@yoni.com", direccion: "av. Prado", telefono: "78454417", pais: "Bolivia", ciudad: "Cbba" },
        { id: "3", nombre: "Monica Montan", email: "moni@moni.com", direccion: "av. Villarroel", telefono: "68254417", pais: "Bolivia", ciudad: "Oruro" },
        { id: "4", nombre: "Mortha Duran", email: ",martha@martha.com", direccion: "av. Villarroel", telefono: "68254417", pais: "Bolivia", ciudad: "La Paz" },
        { id: "5", nombre: "Alis Vale", email: "alis@alis.com", direccion: "av. Villarroel", telefono: "68254417", pais: "Bolivia", ciudad: "Potosi" },
        ]
      }
    },
    components: {
      // Registro de componentes que se utilizaran.
    },
    methods: {
      // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
      guardarNuevo(){
        this.contactos.push(Object.assign({},this.contactoNuevoOb));
      },
      eliminarContacto(index){
        this.contactos.splice(index, 1);
      },
      guardarEdicion(){
        // this.contactos.splice(index, 1, Object.assign({},this.contactoEdicionOb));
        this.contactos[this.indexParaEditar] = Object.assign({},this.contactoEdicionOb);
        this.indexParaEditar = null;
      },
      editarContacto(contacto, index){
        this.indexParaEditar = index;
        this.contactoEdicionOb = Object.assign({},contacto);
      },
      // filtrar(){
      //   const busqueda = this.buscador.toLowerCase();
      //   this.contactosFiltrados = this.contactos.filter(contacto =>
      //   contacto.nombre.toLowerCase().includes(busqueda)
      //   );
      // }
    },
    computed: {
      // propiedades computadas que dependen de otras propiedades reactivas
        contactosFiltrados() {
          const busqueda = this.buscador.toLowerCase();
          return this.contactos.filter(contacto =>
            contacto.nombre.toLowerCase().includes(busqueda)
          );
        }
    },
    props: {
      // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
  }
  </script>
  
  <style scope>
    h1 {
      color: #42b983;
    }
  
    table {
      width: 100%;
      border-collapse: collapse;
      }
      th, td {
          border: 1px solid #ddd;
          padding: 8px;
      }
      th {
          background-color: #f2f2f2;
          text-align: left;
      }
      button {
          background-color: #4CAF50;
          border: none;
          border-radius: 0.5em;
          color: white;
          padding: 8px 16px;
          text-align: center;
          text-decoration: none;
          display: inline-block;
          font-size: 14px;
          margin: 4px 2px;
          cursor: pointer;
    }
  </style>