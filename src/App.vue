
<template>
  <div id="app">
    <header>
      <h1>Teste Front-end Lexart Labs</h1>
    </header>

    <section id="forms">
      <Form :props-forms="formValues" :actionForm="actionForm" @post-product="postProduct"/>
    </section>

  </div>
</template>

<script>
import Form from './components/Form'

export default {
  name: 'App',
  components: {
    Form,
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
      const { data } = await res.json()

      this.arrayTableBody = data

      console.log(this.arrayTableBody)
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

  @media(max-width:768px) {
    html {
      font-size: 14px;
    }
  }

</style>
