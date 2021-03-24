<template>
    <table>
        <thead>
            <tr>
                <th v-for="headData in tableHeadDatas" :key="headData">{{headData}}</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="bodyData in tableBodyDatas" :key="bodyData._id">
                <td>{{bodyData._id}}</td>
                <td>{{bodyData.product.name}}</td>
                <td>{{bodyData.product.brand}}</td>
                <td>{{bodyData.quantity}}</td>
                <td>{{bodyData.price}}</td>
                <td>{{bodyData.client.name}}</td>
                <td>{{bodyData.client.phone}}</td>
                <td>{{bodyData.active}}</td>
                <td id="actionButtons">
                    <button id="buttonSelect" @click="$emit('select-product', bodyData._id)">Select</button>
                    <button id="buttonDelete">Delete</button>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: {
        tableHeadDatas: {
            type: Array
        },
        tableBodyDatas: {
            type: Array
        }
    }
}
</script>

<style scoped>

    table {
        display: flex;
        flex-direction: column;
        margin-top: 5vh;
        border: 1px solid #ddd;
    }

    thead tr {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        background: var(--default-orange);
        color: white;
        padding: 5px 0;
    }

    thead tr th {
        width: calc(100% / 9);
    }

    tbody {
        display: flex;
        flex-direction: column;
        overflow: auto;
    }

    tbody tr {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        margin-top: 5px;
    }

    tbody tr:nth-child(even) {
        background-color: rgb(243, 243, 243);
    }

    tbody tr td {
        width: calc(100% / 9);
        overflow: auto;
        font-size: .8rem;
        text-align: center;
        padding: 1px 5px;
    }

    #actionButtons {
        display: flex;
        justify-content: space-around;
        align-items: center;
    }

    #buttonSelect {
        background: #666;
        border: 1px solid #666;
        border-radius: 3px;
        padding: 1px 2px;
        color: white;
    }

    #buttonDelete {
        background: red;
        border: 1px solid red;
        border-radius: 3px;
        padding: 1px 2px;
        color: white;
    }

    #buttonSelect:hover {
        background: white;
        color: #666;
        transition: .3s;
        
    }

    #buttonDelete:hover {
        background: white;
        color: red;
        transition: .3s;
    }


    @media(max-width: 992px) {
        table {
            flex-direction: row;
            width: 100%;
            margin: 5vh auto;
        }

        thead tr{
            flex-direction: column;
            padding: 5px 0;
        }

        thead tr th {
            margin: 10px 0;
            width: 110px;
            font-size: .85rem;
        }

        tbody {
            flex-direction: row;
        }
        
        tbody tr{
            flex-direction: column;
            width: 110px;
            margin: 0 5px;
        }

        tbody tr td {
            width: 100%;
        }
    }

</style>