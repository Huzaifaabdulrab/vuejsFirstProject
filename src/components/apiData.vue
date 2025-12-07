<template>
  <div>
    <h1>Phone</h1>
    <div class="cards">
      <div class="card" v-for="item in phones" :key="item._id">
        <img :src="item.image" alt="" class="apiImage">  
        <h2>{{ item.title }}</h2>
        <p>{{ item.description }}</p>

        <p>
          <strong>Price:</strong> ${{ item.price }}
        </p>

        <p v-if="item.previousPrice">
          <del>Old Price: ${{ item.previousPrice }}</del>
        </p>

        <p><strong>Category:</strong> {{ item.category }}</p>

      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    name : "ApiData",

    data(){
      return{
        phones : [],
      };
    },
    created(){
      this.fetchPhoneData()
    },

    methods:{
      async fetchPhoneData(){
        try {
          const response = await axios.get("https://jsonserver.reactbd.com/phone")
          this.phones = response.data;
        } catch (error) {
          alert("Data Not fetch something went wronge")
        }
      }
    }
  }
</script>


<style>
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
.apiImage{
  width: 300px;
}
.card {
  padding: 15px;
  border-radius: 10px;
  border: 1px solid #ddd;
}
</style>
