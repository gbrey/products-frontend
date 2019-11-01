<template>
  <div id="app">
    <img alt="App logo" src="./assets/itba.png">
    <h1 class="text-center">{{ title }}</h1>
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
                        <input v-model="selected.amount" placeholder="Cantidad" class="form-control">
                    </div>
                    <div class="col">
                        <input v-model="selected.price" placeholder="Precio" class="form-control">
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
                        <input v-model="edited.name" class="form-control">
                      </span>
                      <span v-else>{{ product.name }}</span>
                    </td>
                    <td>
                      <span v-if="edit_mode && edited.id === index">
                        <input v-model="edited.description" class="form-control">
                      </span>
                      <span v-else>{{ product.description }}</span>
                    </td>
                    <td>
                      <span v-if="edit_mode && edited.id === index">
                        <input v-model="edited.amount" class="form-control">
                      </span>
                      <span v-else>{{ product.amount }}</span>
                    </td>
                    <td>
                      <span v-if="edit_mode && edited.id === index">
                        <input v-model="edited.price" class="form-control">
                      </span>
                      <span v-else>{{ product.price }}</span>
                    </td>
                    <td>
                      <span v-if="edit_mode && edited.id === index">
                        <button v-on:click="update(index)" class="btn btn-secondary">Guardar</button>
                      </span>
                      <span v-else>
                        <button v-on:click="edit(index)" class="btn btn-info">Actualizar</button>
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
        title: 'Mi app de productos en GKE',
        selected: {},
        edit_mode: false,
        edited: {},
        products: [
          {
            id: 80000234,
            name: 'Apple Airpods 2',
            description: 'Apple AirPods 2da Generacion Inalam Sellados Orig Gtia 1 Año',
            amount: 2,
            price: 18000
          },
          {
            id: 80000678,
            name: 'Amazon Alexa',
            description: 'Amazon Echo Dot (3 Gen) Alexa Bluetooth Wifi Audio White Box',
            amount: 5,
            price: 7000
          }
        ]
      }
    },
    methods: {
      add: function(){
        this.products.push({
            id: Math.floor(Math.random()*500+1),
            name: this.selected.name,
            description: this.selected.description,
            amount: this.selected.amount,
            price: this.selected.price
        });
        this.selected = {};
      },
      remove: function(index){
        this.products.splice(index, 1);
      },
      edit: function(index){
        this.edit_mode = true;

        this.edited.id = index;
        this.edited.name = this.products[index].name;
        this.edited.description = this.products[index].description;
        this.edited.amount = this.products[index].amount;
        this.edited.price = this.products[index].price;
      },
      update: function(index){
        this.edit_mode = false;

        this.products[index].name = this.edited.name;
        this.products[index].description = this.edited.description;
        this.products[index].amount = this.edited.amount;
        this.products[index].price = this.edited.price;
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
