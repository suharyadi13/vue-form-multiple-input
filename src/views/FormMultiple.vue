<template>
  <div>
    <section class="hero">
      <div class="hero-body">
        <h1 class="title">Form Multiple Input</h1>
        <h2 class="subtitle">This Form multiple input using Vue.js</h2>
      </div>
    </section>
    <div class="container fluid">
      <form @submit.prevent="onSubmit" novalidate="true">
      <div class="row">
        <div class="col-12">
          <button class="btn btn-primary" @click="newInput">New</button>
        </div>  
      </div>
      <div class="row" v-for="(data, index) in Datas"  :key="index">
        <div class="col-md-2">
          <div class="field">
            <label class="label" for="ProductName">Product Name</label>
            <input class="input"
              id="ProductName"
              v-model.trim="data.ProductName"
              type="text"
              name="ProductName"
            >
            <FormError :errors="errors.ProductPrice" />
          </div>  
        </div>
        <div class="col-md-2">
          <div class="field">
            <label class="label" for="ProductPrice">Product Price</label>
            <input class="input"
              id="ProductPrice"
              v-model.trim="data.ProductPrice"
              type="number"
              name="ProductPrice"
              @change="calCulate"
            >
            <FormError :errors="errors.ProductPrice" />
          </div>  
        </div>
        <div class="col-md-2">
          <div class="field">
            <label class="label" for="Qty">QTY</label>
            <input class="input"
              id="Qty"
              v-model.trim="data.Qty"
              type="number"
              name="Qty"
              @change="calCulate"
            >
            <FormError :errors="errors.Qty" />
          </div>  
        </div>
        <div class="col-md-2">
          <div class="field">
            <label class="label" for="Total">Product Total</label>
            <input class="input"
              id="Total"
              v-model.trim="data.Total"
              type="text"
              disabled="true"
              name="Total"
            >
            <FormError :errors="errors.Total" />
          </div>  
        </div>
        <div class="col-md-2" v-if="index != 0">
          <button class="btn btn-danger" @click="deleteItem(index)">Delete</button>
        </div>
       </div>
       <div class="row mt-5">
       <div class="col-2 offset-6">
       <label class="label" for="GrandTotal">Grand Total</label>
        <input class="input"
              id="GrandTotal"
              v-model.trim="GrandTotal"
              type="text"
              name="GrandTotal"
            >
       </div>
       </div>
      </form>
    </div>
  </div>
</template>

<script>
import FormError from "@/components/FormError";

export default {
  name: "FormMultiple",
  components:{
    FormError
  },
  data() {
    return {
      errors:{
        ProductName:[],
        ProductPrice:[],
        Qty:[],
        Total:[]
      },
      Datas: [{
          ProductName:null,
          ProductPrice:0,
          Qty:1,
          Total:0
      }],
      GrandTotal:0
    }
  },
  methods:{
    onSubmit() {
      return this.checkForm();
    }, 
    checkForm() {
      this.resetErrors();
      
    },
    newInput(){
      var Data = {
          ProductName:null,
          ProductPrice:0,
          Qty:1,
          Total:0
      }
      this.Datas.push(Data);
    },
    resetErrors() {
      this.errors = { 
        ProductName:[],
        ProductPrice:[],
        Qty:[],
        Total:[]
      }
    },
    calCulate(){
      this.GrandTotal= 0
      this.Datas.forEach((value) => {
          value.Total = parseInt(value.Qty) * parseInt(value.ProductPrice);
          this.GrandTotal += parseInt(value.Total);
      });
    },
    deleteItem(index){
      var RemovedItem = this.Datas.splice(index,1);
      console.log(RemovedItem);
      this.GrandTotal= 0
      this.Datas.forEach((value) => {
          value.Total = parseInt(value.Qty) * parseInt(value.ProductPrice);
          this.GrandTotal += parseInt(value.Total);
      });
    }
  }
};
</script>
