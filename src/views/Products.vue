<template> 
  <div class="aling-center"> 
    <h1>Products</h1> 
    <div v-for="p in Products" :key="p.id" class="cart"> 
      <img :src="p.Images[0].imageURL" alt=""> 
      <p>{{ p.title }}</p> 
      <p>{{ p.description }}</p> 
      <p>{{ p.price }}</p> 
      <button @click="move(p.id)">click</button> 
    </div> 
  </div> 
</template> 
 
<script> 
import gql from "graphql-tag"; 
export default { 
  apollo: { 
    Products: { 
      query: gql` 
        query products($limit: Int!) { 
          Products(limit: $limit) { 
            id 
            title 
            description 
            price 
            Images { 
              imageURL 
            } 
          } 
        } 
      `, 
      variables() { 
        return { 
          limit: this.limit, 
        }; 
      }, 
    }, 
  }, 
  data() { 
    return { 
      limit: 10, 
    }; 
  }, 
methods:{ 
  move(id){ 
    this.$router.push("/products/" + id) 
  }, 
} 
}; 
</script> 
 
<style scoped> 
  .cart {
    border: 1px solid black;
    display: flex;
    justify-content: center; 
   align-items: center;
    margin: 5%;
    padding: 5%; 
}
  .cart p{
    font-size: 125%;
  }
  .cart img {
    width: 10%;
  }
</style>