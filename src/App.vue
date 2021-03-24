
<template>
  <div id="app">
    <header>
      <h1>Teste Front-end Lexart Labs</h1>
    </header>

    <div class="container">
      <section id="forms">
        <Form :props-forms="formValues" :actionForm="actionForm" @post-product="postProduct"/>
      </section>
      <section>
        <Table :table-head-datas="arrayTableHead" :table-body-datas="arrayTableBody" @select-product="getSelectedProduct"/>
      </section>
    </div>

  </div>
</template>

<script>
import Form from './components/Form'
import Table from './components/Table'

export default {
  name: 'App',
  components: {
    Form,
    Table
  },
  
  data () {
    return {
      formValues: {
        product: {
          name: '',
          brand: ''
        },
        client: {
          name: '',
          phone: ''
        },
        price: '',
        quantity:'',
        active: ''
      },

      actionForm: 'Add Product',

      baseURL: 'https://crudcrud.com/api/e60e84838b744062ae9e9c869beb38d8', // 8

      arrayTableHead: ["_Id","Product Name", "Product Brand", "Quantity", "Price", "Client Name", "Client Phone", "Active", "Actions"],

      arrayTableBody: []
    }
  },

  mounted() {
    this.getProduct()
  },

  methods: {
    async getProduct() {
      const req = new Request (
        `${this.baseURL}/stock`,
        {
          method: 'GET',
          mode: 'cors'
        }
      )

      const res = await fetch(req)
      const data = await res.json()

      this.arrayTableBody = data
      console.log(data)
      console.log(this.arrayTableBody)
    },

    async getSelectedProduct(idSelected) {
      const req = new Request (
        `${this.baseURL}/stock/${idSelected}`,
        {
          method: 'GET',
          mode: 'cors'
        }
      )

      const res = await fetch(req)
      const selectedProduct = await res.json()

      console.log(selectedProduct)

      this.formValues = selectedProduct
    },

    async postProduct(formInfos) {
      const headers = new Headers ()

      headers.append(
        'Content-type',
        'application/json;charset=utf-8'
      )

      const req = new Request (
        `${this.baseURL}/stock`,
        {
          method: 'POST',
          body: JSON.stringify(formInfos),
          headers,
          mode: 'cors',
          cache: 'default'
        }
      )

      const res = await fetch(req)
      const data = await res.json()

      console.log(data)
      await this.getProduct()
    }

  },
}
</script>

<style>

  :root {
    --default-orange: rgb(231,150,0)
  }

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    color: #2c3e50;
  }

  header {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 6vh;
    font-size: .8rem;
    widows: 100%;
    background-color: var(--default-orange);
    color: white;
  }

  .container {
    max-width: 1250px;
    margin: auto;
    padding: 0 8px;
  }

  @media(max-width:768px) {
    html {
      font-size: 14px;
    }
  }

</style>
