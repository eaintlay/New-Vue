<template>
  <div class="container">
    <div class="row my-3">
      <div class="col-md-12">
        <h2>Item Detail / Show</h2>
      </div>
    </div>
    
    <div class="row">
      <div class="col-md-12">
        <div class="card mb-3" v-if="item">
          <div class="row no-gutters">
            <div class="col-md-4">
              <img :src="item.item_photo" class="img-fluid">
            </div>
            <div class="col-md-8">
              <div class="card-body text-left">
                <h5 class="card-title">{{item.item_name}}</h5>
                <p class="card-text">{{ item.item_desc }} This is a wider card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                <p>
                  <span class="mr-2" v-if="item.brand"> <b-icon icon="tag-fill" variant="info"></b-icon> {{item.brand.brand_name}}</span>
                  <span v-if="item.subcategory"> <b-icon icon="tag-fill" variant="dark"></b-icon> {{item.subcategory.subcategory_name}}</span>
                </p>

                <p>Price: <strong class="text-danger">{{item.item_price}} MMK</strong></p>
                
                <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>

                <input type="number" name="qty" v-model="qty" class="form-control w-25 d-inline-block" min="1">

                <button class="ml-3 btn btn-info" @click="addToCart()">Add To Cart</button>

              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  import ItemService from '@/services/ItemService.js'

  export default{
    data(){
      return{
        qty: 1,
        item : {}
      }
    },
    created(){
      let id = this.$route.params.id;
      ItemService.getItem(id)
        .then(response => {
          this.item = response.data.item
        })
        .catch(error => {
          console.log('There was an error:',error.response)
        })
    },
    methods: {
      addToCart() {
        let item = {id:this.item.item_id,name:this.item.item_name,price:this.item.item_price,qty:this.qty};
        this.$store.dispatch('addToCart', item)
      }
    }
  }
</script>

<style type="text/css">
  
</style>