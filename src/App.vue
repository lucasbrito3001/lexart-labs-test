
<template>
  <div id="app">
    <header>
      <h1>Teste Front-end Lexart Labs</h1>
    </header>

    <div class="container">
      <section id="forms">
        <Form :props-forms="formValues" :actionForm="actionForm" @post-product="postProduct" @put-product="updateSelectedProduct"/>
      </section>
      <section id="table">
        <h2>ABM Stock</h2>
        <Table :table-head-datas="arrayTableHead" :table-body-datas="arrayTableBody" @select-product="getSelectedProduct" @delete-product="deleteProduct"/>
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

      idToUpdate: '',

      actionForm: 'Add Product',

      crudcrudURL: 'https://crudcrud.com/api/755d6e3510194903a40c58924c9b3cdc', // link do crudcrud que vai ser utilizado para realizar as requests!

      arrayTableHead: ["_Id","Product Name", "Product Brand", "Quantity", "Price (R$)", "Client Name", "Client Phone", "Active", "Actions"],

      arrayTableBody: []
    }
  },

  mounted() {
    this.getProduct()
  },

  methods: {
    async getProduct() {
      const req = new Request (
        `${this.crudcrudURL}/stock`,
        {
          method: 'GET',
          mode: 'cors'
        }
      )

      const res = await fetch(req)
      const data = await res.json()

      this.arrayTableBody = data
    },

    async getSelectedProduct(idSelected) {

      this.idToUpdate = idSelected

      const req = new Request (
        `${this.crudcrudURL}/stock/${this.idToUpdate}`,
        {
          method: 'GET',
          mode: 'cors'
        }
      )

      const res = await fetch(req)
      const selectedProduct = await res.json()

      this.formValues = {
        product: {
            name: selectedProduct.product.name,
            brand: selectedProduct.product.brand,
        },
        client: {
            name: selectedProduct.client.name,
            phone: selectedProduct.client.phone,
        },
        price: selectedProduct.price,
        quantity: selectedProduct.quantity,
        active: selectedProduct.active
      }

      this.actionForm = 'Update Product'
    },

    async postProduct(formInfos) {

      const headers = new Headers ()

      headers.append(
        'Content-type',
        'application/json;charset=utf-8'
      )

      console.log(formInfos)

      const req = new Request (
        `${this.crudcrudURL}/stock`,
        {
          method: 'POST',
          body: JSON.stringify(formInfos),
          headers,
          mode: 'cors',
          cache: 'default'
        }
      )

      await fetch(req)

      this.getProduct()

      this.clearFormInputs()

    },

    async updateSelectedProduct(updateInfos) {

      const headers = new Headers ()
      headers.append(
        'Content-type',
        'application/json;charset=utf-8'
      )

      const req = new Request (
        `${this.crudcrudURL}/stock/${this.idToUpdate}`,
        {
          method: 'PUT',
          mode: 'cors',
          body: JSON.stringify(updateInfos),
          headers,
          cache: 'default'
        }
      )

      await fetch(req)
      
      this.getProduct()

      this.clearFormInputs()

      this.actionForm = 'Add Product'

      this.idToUpdate = ''

    },

    async deleteProduct(idDeleted) {
      try {
        const req = new Request (
        `${this.crudcrudURL}/stock/${idDeleted}`,
        {
          method: 'DELETE',
          mode: 'cors'
        }
      )

        await fetch(req)

        this.getProduct()
      } catch (error) {
        console.error('[ERROR]')
      }
    },

    clearFormInputs() {
      this.formValues.product.name = ''
      this.formValues.product.brand = ''
      this.formValues.client.name = ''
      this.formValues.client.phone = ''
      this.formValues.price = ''
      this.formValues.quantity = ''
      this.formValues.active = ''
    }

  }
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

  #table h2 {
    font-size: .8rem;
    text-align: left;
    color: var(--default-orange);
    width: fit-content;
    border-bottom: 2px solid #888;
    margin-top: 4vh;
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

  @media(max-width:350px) {
    html {
      font-size: 13.5px;
    }

    header {
      font-size: .7rem;
    }
  }

</style>
