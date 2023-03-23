<template>

<div id="holder">
    <div class="views-cont" id="active">
        <h2>Active Tasks</h2>
        <div id="notaskmsg">{{ notaskmsg }}</div>
            <li v-for="(kokos, index) in dataGlobal">
                
                    {{ kokos.title }}

                    <button class="deletebtn" @click="deleteTodo(index)">
                        <ion-icon name="trash"></ion-icon>
                    </button>

            </li>
        <form action="" v-on:submit="submitForm">
            <input type="text" id="input" v-model="test" placeholder="start typing..." />
            <input class="submit" type="submit" value="ADD" name="add" @click="storeTest">
        </form>


        </div>

                <div class="views-cont" id="deleted">
                <h2>Deleted Tasks</h2>
                <div id="normvmsg">{{ normvmsg }}</div>
                
            <li v-for="(rmved, index) in deleted">
                {{ rmved }}
            </li>
    </div>
</div>




</template>


<script>
import axios from 'axios';

// window.axios = require('axios');

export default {

    data() {
        return {
            list: [],
            deleted: [],
            test: '',
            deletedlist: '',
            notaskmsg: 'There are no active tasks...',
            normvmsg: 'There are no deleted tasks...',
            dataGlobal: [],
        }

    },

    mounted() {
        // // this.LoadData(
        // fetch('https://jsonplaceholder.typicode.com/posts')
        // .then((response) => response.json())
        // .then((json) => console.log(json));

        let dataGlobal;

        const getData = async () => {
            const response = await fetch("https://jsonplaceholder.typicode.com/todos/");
            const data = await response.json();
            dataGlobal = data.title;
            this.dataGlobal = data
            return data;
        };

        (async () => {
        await getData();
        console.log(dataGlobal);
        })();

        this.dataGlobal = dataGlobal;

        if (dataGlobal == null){
            document.getElementById('notaskmsg').style = "display: block;"
        }
        // this.storeTest()
    },

    methods: {

        

        storeTest(){
            if(this.test == ''){
                return(console.log('reloaded page or empty field'))
            }
            this.dataGlobal.push(this.test)
            this.test = ''
            document.getElementById('notaskmsg').style = "display: none;"
            
            localStorage.setItem("todos", JSON.stringify(this.list));
            // this.list = JSON.parse(localStorage.getItem("todos"));
            // this.LoadTodo()
            console.log(list)


        },
        submitForm : function(event){
            event.preventDefault(),
            event.target.reset()
        },
        deleteTodo(index){
            this.deleted.push(this.dataGlobal.splice(index, 1)[0])
            this.test = ''
            document.getElementById('normvmsg').style = "display: none;"

            localStorage.setItem("deleted", JSON.stringify(this.deleted));
            // this.deleted = JSON.parse(localStorage.getItem("deleted"));
            // this.LoadDeleted()
        },
        LoadData(){
            this.deleted = JSON.parse(localStorage.getItem("deleted"));
            this.list = JSON.parse(localStorage.getItem("todos"));
            this.storeTest()
            this.deleteTodo()
            this.console.log(test, deletedlist)
        }
        
    },

    

}
</script>

<style scoped>

    #notaskmsg {
        display: none !important;
    }

    #holder{
        display: grid;
        grid-template-columns: auto auto;
    }

    .container1{
        margin: 15px;
    }

    .views-cont{
      margin: 20px;
      background: rgb(19, 19, 19);
      border-radius: 5px;
      padding: 15px;
      min-width: 400px;
      height: fit-content;
    }

    .views-cont h2{
      border-bottom: 1px solid rgb(32, 32, 32);
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
        color: black;
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

    #deleted li{
        background: rgb(58, 0, 0);
        color: rgb(255, 168, 168);
        border-bottom: 1px solid rgb(31, 0, 0);
    }

</style>