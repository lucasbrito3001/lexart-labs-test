<template>
    <form @submit.prevent="sendFormAction">
        <div id="inputs">
            <fieldset>
                <legend>Product</legend>
                <label for="product-name">Name :</label> <br>
                <input type="text" id="product-name" v-model="propsForms.product.name"> <br>
                <label for="product-brand">Brand :</label> <br>
                <input type="text" id="product-brand" v-model="propsForms.product.brand"> <br>
            </fieldset>
            
            <fieldset>
                <legend>Client</legend>
                <label for="client-name">Name :</label> <br>
                <input type="text" id="client-name" v-model="propsForms.client.name"> <br>
                <label for="client-phone">Phone :</label> <br>
                <input type="text" id="client-phone" v-model="propsForms.client.phone">
            </fieldset>
            <fieldset>
                <legend>Infos</legend>
                <label for="price">Price :</label> <br>
                <input type="number" id="price" v-model="propsForms.price"> <br>
                <label for="quantity">Quantity :</label> <br>
                <input type="number" id="quantity" v-model="propsForms.quantity"> <br>
                <label for="active">Active :</label> <br>
                <input type="text" id="active" v-model="propsForms.active">
            </fieldset>
        </div>
        <div id="submit">
            <input type="submit" :value="actionForm" id="submitButton">
        </div>
    </form>
</template>

<script>
export default {
    props : {
        propsForms: {
            type: Object,
        },
        actionForm: {
            type: String
        }
    },

    methods: {
        sendFormAction() {
            if (this.actionForm == 'Add Product') {
                this.$emit('post-product', this.propsForms)
            } else if (this.actionForm == 'Update Product') {
                this.$emit('put-product', this.propsForms)
            }
        }
    }
}
</script>

<style scoped>

    form {
        display: flex;
        flex-direction: column;
        margin-top: 2vh;
    }

    #inputs {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        width: 100%;
    }

    #submit {
        margin: 10px auto;
    }

    #submitButton {
        width: fit-content;
        background: var(--default-orange);
        color: white;
        border: 1px solid var(--default-orange);
    }

    #submitButton:hover {
        background: white;
        color: var(--default-orange);
    }

    fieldset {
        padding: 5px;
        width: 30%;
        border-radius: 3px;
        border: 1px solid var(--default-orange);
        color: var(--default-orange);
    }

    input {
        border: 1px solid #ddd;
        border-radius: 3px;
        font-size: 1rem;
        padding: 2px 5px;
        width: 100%;
    }

    @media(max-width: 768px) {
        #inputs {
            flex-direction: column;
        }

        fieldset {
            width: 95%;
            margin: auto;
        }
    }

</style>