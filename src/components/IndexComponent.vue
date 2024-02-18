<template>
  <div>
    <div class="container">
      <table class="table">
        <thead>
        <tr>
          <th scope="col">№</th>
          <th scope="col">Name</th>
          <th scope="col">Number</th>
          <th scope="col">Edit</th>
        </tr>
        </thead>
        <tbody>
        <template v-for="item in lists" :key="item.id">
          <tr>
            <th scope="row">{{item.id}}</th>
            <td>{{item.name}}</td>
            <td>{{ item.number }}</td>
            <td><a href="#" @click.prevent="changeEditUserId(item.id, item.name, item.number, item.description)" class="btn btn-success">Edit</a></td>
          </tr>

          <tr :class="idEdit(item.id) ? '' : 'd-none'">
            <th scope="row">{{item.id}}</th>
            <td><input type="text" class="form-control" v-model="name"></td>
            <td><input type="text" class="form-control" v-model="number"></td>
            <td><input type="text" class="form-control" v-model="description"></td>
            <td><a href="#" @click.prevent="updateUser(item.id)" class="btn btn-success">Update</a></td>
          </tr>
        </template>
        </tbody>
      </table>
    </div>
  </div>
</template>


<script>

import axios from 'axios';
  export default {
    name: "IndexComponent",

    data() {
      return {
        lists: null,
        editUserId: null,
        name: '',
        number: '',
        description: '',

      }
    },

    mounted() {
      this.getData();
    },

    methods: {
      getData(){
        let url = "http://127.0.0.1:8000/api/get/all";
        fetch(url)
            .then(response => response.json())
            .then(data => {
              this.lists = data;
            });
      },

      updateUser(id){
        this.editUserId = null;
        let url = `http://127.0.0.1:8000/api/${id}`;
          axios.patch(url, {name: this.name, number: this.number, description: this.description})
              .then(response => {
                let data = response.data;
                for(let index = 0; index < this.lists.length; index++)
                {
                  if(this.lists[index].id === data.id)
                  {
                    this.lists[index] = data;
                    break;
                  }
                }
              })
      },

      changeEditUserId(id, name, number, description) {
        this.editUserId = id
        this.name = name
        this.number = number
        this.description = description
      },

      idEdit(id) {
        return this.editUserId === id
      },


    },


  }

</script>

<style scoped>

</style>