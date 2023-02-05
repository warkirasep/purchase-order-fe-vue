<template>
  <div class="container">
    <h2>Dynamic Form Purchase Order <small>Please Click Add For Add New Item</small></h2>
      <button class="add-item" @click="addNewItem">Add New Item</button>
      <ul class="responsive-table">
        <li class="table-header">
          <div class="col col-2">Product Name</div>
          <div class="col col-1">QTY</div>
          <div class="col col-2">Price</div>
        </li>
        <li class="table-row" v-for="po in formdata.purchase_order">
          <div class="col col-2" data-label="Product Name">
            <input type="text" v-model="po.product_name">
          </div>
          <div class="col col-1" data-label="QTY">
            <input type="text" v-model="po.qty">
          </div>
          <div class="col col-2" data-label="Price">
            <input type="text" v-model="po.price"/>
            <a href="" class="delete-item">Delete</a>
          </div>
        </li>
      </ul>
    <button class="add-item" @click="saveItem">Save Item</button>
  </div>

</template>
<script>
  import axios from 'axios'
  export default {
    data(){
      return {
        formdata: {
          purchase_order: [
            {
              product_name: null,
              qty: null,
              price: null
            }
          ]
        }
      }
    },
    methods: {
      addNewItem(){
        let data = {
          product_name: null,
          qty: null,
          price: null
        }

        this.purchase_order.push(data);
      },
      saveItem(){
        axios.post('http://127.0.0.1:8000/api/purchase-order', this.formdata);
      }
    }
  }
</script>

<style scoped lang="scss">
input[type="text"],
input[type="password"],
.btn-sinkronisasi {
  width: 70%;
  margin-bottom: 25px;
  height: 40px;
  border-radius: 5px;
  outline: 0;
}

input[type="text"],
input[type="password"] {
  border: 1px solid #bbb;
  // padding: 0 0 0 10px;
  font-size: 14px;
}

input[type="text"]:focus,
input[type="password"]:focus {
  border: 1px solid #3498db;
}


.add-item {
  margin: 40px;
  background: green;
  border: none;
  color: white;
  font-size: 18px;
  font-weight: 200;
  cursor: pointer;
  transition: box-shadow .4s ease;
}

.delete-item{
  margin: 10px;
  background: red;
  border: none;
  color: white;
  font-size: 18px;
  font-weight: 200;
  cursor: pointer;
  transition: box-shadow .4s ease;
}
.add-item:hover {
  box-shadow: 1px 1px 5px #555;
}
.add-item:active {
  box-shadow: 1px 1px 7px #222;
}


body {
  font-family: 'lato', sans-serif;
}
.container {
  max-width: 1000px;
  margin-left: auto;
  margin-right: auto;
  padding-left: 10px;
  padding-right: 10px;
}

h2 {
  font-size: 26px;
  margin: 20px 0;
  text-align: center;
  small {
    font-size: 0.5em;
  }
}

.responsive-table {
  li {
    border-radius: 3px;
    padding: 25px 30px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 25px;
  }
  .table-header {
    background-color: #95A5A6;
    font-size: 14px;
    text-transform: uppercase;
    letter-spacing: 0.03em;
  }
  .table-row {
    background-color: #ffffff;
    box-shadow: 0px 0px 9px 0px rgba(0,0,0,0.1);
  }
  .col-1 {
    flex-basis: 10%;
  }
  .col-2 {
    flex-basis: 40%;
  }
  .col-3 {
    flex-basis: 25%;
  }
  .col-4 {
    flex-basis: 25%;
  }
  
  @media all and (max-width: 767px) {
    .table-header {
      display: none;
    }
    .table-row{
      
    }
    li {
      display: block;
    }
    .col {
      
      flex-basis: 100%;
      
    }
    .col {
      display: flex;
      padding: 10px 0;
      &:before {
        color: #6C7A89;
        padding-right: 10px;
        content: attr(data-label);
        flex-basis: 50%;
        text-align: right;
      }
    }
  }
}
</style>
