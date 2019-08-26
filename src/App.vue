<template>
  <div id="app">
    <img alt="App logo" src="./assets/itba.png">
    <h1>{{ title }}</h1>
    <br>
    <div class="container">
      <section class="form">
        <form action="">
          <div class="form-row">
            <!-- Formulario producto-->
            <div class="col">
              <input v-model="selected.name" class="form-control" placeholder="Nombre">
            </div>
            <div class="col">
              <input v-model="selected.description" placeholder="Descripcion" class="form-control">
            </div>
            <div class="col">
                <input v-model.number="selected.amount" placeholder="Cantidad" class="form-control">
            </div>
            <div class="col">
              <input v-model.number="selected.price" placeholder="Precio" class="form-control">
            </div>
            <div class="col">
              <!-- Botón para añadir -->
              <input v-on:click="add" type="button" value="Add Product" class="btn btn-success">
            </div>
          </div>
        </form>
      </section>
      <br>
      <!-- Tabla donde se muestran los datos -->
      <section class="data">
        <table class="table table-striped table-hover">
          <thead class="thead-dark">
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nombre</th>
              <th scope="col">Descripcion</th>
              <th scope="col">Cantidad</th>
              <th scope="col">Precio Unitario</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(product, index) in products" v-bind:key="product.id">
              <td>{{ product.id }}</td>
              <td>
                <span v-if="edit_mode && edited.id === index">
                  <!-- Input para editar -->
                  <input v-model="edited.name" class="form-control">
                </span>
                <span v-else>{{ product.name }}</span>
              </td>
              <td>
                <span v-if="edit_mode && edited.id === index">
                  <!-- Input para editar -->
                  <input v-model="edited.description" class="form-control">
                </span>
                <span v-else>{{ product.description }}</span>
              </td>
              <td>
                <span v-if="edit_mode && edited.id === index">
                  <!-- Input para editar -->
                  <input v-model.number="edited.amount" type="number" class="form-control">
                </span>
                <span v-else>{{ product.amount }}</span>
              </td>
              <td>
                <span v-if="edit_mode && edited.id === index">
                  <!-- Input para editar -->
                  <input v-model.number="edited.price" type="number" class="form-control">
                </span>
                <span v-else>$ {{ product.price }}</span>
              </td>
              <td>
                <!-- Botón para confirmar edición -->
                <span v-if="edit_mode && edited.id === index">
                  <button v-on:click="update(index)" class="btn btn-secondary">Guardar</button>
                </span>
                <span v-else>
                  <!-- Botón para mostrar modo edición -->
                  <button v-on:click="edit(index)" class="btn btn-info">Actualizar</button>
                  <!-- Botón para eliminar productos -->
                  <button v-on:click="remove(index)" class="btn btn-danger">Borrar</button>
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </section>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        title: 'My Awesome App!',
        selected: {},
        edit_mode: false,
        edited: {},
        products: [
          {
            id: 34,
            name: 'Producto Ejemplo 1',
            description: 'Descripción producto 1',
            amount: 4,
            price: 21.50
          },
          {
            id: 89,
            name: 'Producto Ejemplo 2',
            description: 'Descripción producto 2',
            amount: 8,
            price: 200
          },
          {
            id: 456,
            name: 'Producto Ejemplo 3',
            description: 'Descripción producto 3',
            amount: 7,
            price: 1200
          }
        ]
      }
    },
    methods: {
      add: function () {
        this.products.push({
          id: Math.floor(Math.random()*500 + 1),
          name: this.selected.name,
          description: this.selected.description,
          amount: this.selected.amount,
          price: this.selected.price
        });
        this.selected = {};
      },
      edit: function (index) {
        this.edit_mode = true;

        this.edited.id = index;
        this.edited.name = this.products[index].name;
        this.edited.description = this.products[index].description;
        this.edited.amount = this.products[index].amount;
        this.edited.price = this.products[index].price;
      },
      update: function (index) {
        this.edit_mode = false;
        this.products[index].name = this.edited.name;
        this.products[index].description = this.edited.description;
        this.products[index].amount = this.edited.amount;
        this.products[index].price = this.edited.price;
      },
      remove: function (index) {
        this.products.splice(index, 1);
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
