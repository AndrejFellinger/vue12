<template>

    <div class="container">
        <div>
            <h1>Your Tasks</h1>
            <div id="todo-hdr">
                <router-link class="hdr-link hrd-link-active" to="">Active</router-link>
                <router-link class="hdr-link" to="/deleted">Deleted</router-link>
            </div>
        </div>


        <!-- <ul> -->
            <li v-for="(kokos, index) in list">
            
                {{ kokos }}

                <button class="deletebtn" @click="deleteTodo(index)">
                    <ion-icon name="trash"></ion-icon>
                </button>

            </li>
        <!-- </ul> -->
    <form action="" v-on:submit="submitForm">
        <input type="text" id="input" v-model="test" placeholder="start typing..." />
        <input class="submit" type="submit" value="ADD" name="add" @click="storeTest">
    </form>


    </div>

        <h2 v-for="(rmved, index) in deleted">

            {{ rmved }}

        </h2>



</template>


<script>
export default {
    data() {
        return {
            list: [],
            deleted: [],
            test: '',
            deletedlist: ''
        }

    },

    methods: {
        storeTest(){
            this.list.push(this.test)

        },
        submitForm : function(event){
            event.preventDefault(),
            event.target.reset()
        },
        deleteTodo(index){
            this.deleted.push(this.list.splice(index, 1)[0])

            console.log( this.deleted )
        }
    },

}
</script>

<style scoped>

    .container{
        background: white;
        display: grid;
        grid-template-columns: auto;
        color: rgb(27, 27, 27);
        padding: 20px;
        border-radius: 5px;
        justify-content: center;
        align-items: center;
        box-shadow: 0 0 15px rgba(255, 255, 255, 0.24);
        max-height: 800px;
        overflow: scroll;
    }

    h1{
        text-align: center;
        font-size: 24px;
        /* border-bottom: 1px solid rgb(212, 212, 212); */
    }

    ul{
        font-size: 18px;
        text-align: left;
        display: flex;
        list-style-type: none;
    }

    li{
        margin-top: 10px;
        border-bottom: rgb(212, 212, 212) 1px solid;
        align-items: center;
        padding: 4px;
        background: rgb(240, 240, 240);
        list-style-type: none;
        border-radius: 3px;
    }

    input{
        padding: 5px;
        outline: none;
        border: none;
        background: rgb(212, 212, 212);
        margin: 3px;
        border-radius: 3px;
        width: 100%;
    }

    #input{
        margin-top: 20px;
    }

    .submit{
        color: green;
        background: greenyellow;
        width: 100%;
        cursor: pointer;
    }

    .submit:hover{
        outline: solid green 2px;
    }

    .deletebtn{
        background: transparent;
        border: none;
        outline: none;
        font-size: 20px;
        cursor: pointer;
        color: black;
        transition: 0.3s ease;
        vertical-align: middle;
        float: right;
        margin-left: 15px;
        border-left: rgb(218, 218, 218) solid 1px;
        padding-left: 6px;
    }

    .deletebtn:hover{
        transition: 0.3s ease;
        color: red;
    }

    #todo-hdr{
        display: flex;
        justify-content: center;
        text-align: center;
        align-items: center;
    }

    .hdr-link{
        margin: 10px;
        font-size: 18px;
        background: rgb(248, 248, 248);
        padding: 5px;
        color: black;
        border-radius: 3px;
    }

    .hdr-link:hover{
        background: rgb(228, 228, 228);
    }

    .hrd-link-active{
        background: rgb(228, 228, 228);
    }

</style>