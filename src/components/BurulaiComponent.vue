<template>
  <div>
      <h1>Home Work</h1>
    <div class="container">
      <div class="container">
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Name</label>
          <input type="text" class="form-control" v-model="name" id="name" placeholder="name">
        </div>
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Number</label>
          <input type="text" class="form-control" v-model="number" id="number" placeholder="number">
        </div>
        <div class="mb-3">
          <label for="description" class="form-label">Example textarea</label>
          <textarea class="form-control" id="description" v-model="description" rows="3"></textarea>
        </div>
        <button @click="createUser" class="btn btn-primary">Create</button>
      </div>
    </div>
    <div class="container">
      <table class="table">
        <thead>
        <tr>
          <th scope="col">№</th>
          <th scope="col">Name</th>
          <th scope="col">Number</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="item in lists" :key="item.id">
          <th scope="row">{{item.id}}</th>
          <td>{{item.name}}</td>
          <td>{{ item.number }}</td>
        </tr>
        </tbody>
      </table>
    </div>

  </div>
</template>


<script>
  export default {
    name: 'BurulaiComponent',
    data(){
      return {
        lists: null,
        name: '',
        number: '',
        description: ''
      }
    },
    methods:{
      getData(){
          let url = "http://127.0.0.1:8000/api/get/all";
        fetch(url)
            .then(response => response.json())
            .then(data => {
              this.lists = data;
            });
      },
      createUser()
      {
        let url = "http://127.0.0.1:8000/api/create";
        let data = new FormData();
        data.append('name', this.name);
        data.append('number', this.number);
        data.append('description', this.description);
        this.name = '';
        this.number = '';
        this.description = '';
        fetch(url, {
          method: 'POST',
          body: data
        })
            .then(response => response.json())
            .then(data => {
              this.lists = data;
            });
      },
    },
    mounted() {
      this.getData();
    }
  }

</script>


<style scoped>

</style>