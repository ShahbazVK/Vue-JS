<template>
<div>
    <h2>Home component</h2>
    <h2>{{email}}</h2>
    <h2>{{name}}</h2>
    <h2>{{getName("Rizwan")}}</h2>
    <h4>{{getData().name}}</h4>
    <h4>{{getData().emailOfAsif}}</h4>
    <br>
    <br>
    <br>
    <button @click="addCount()">Add 1</button>
    <button @click="subtractCount()">Subtract 1</button>
    <button v-on:click="resetCount">Reset count</button>
    <h2>Count: {{getCount()}}</h2>
    <h2 v-once>V-once------------ Count: {{count}}</h2><!-- //value change ni hogi -->
    <input type="text" v-model="count">
    <br>
    <br>
    <h1 v-if="show">IF CONDITION</h1>
    <h1 v-else>Else CONDITION</h1>
    <button @click="changeCondition()">Change Condition</button>
    <h1>FOR Loop</h1>
    <ul>
        <li v-for="item in technology" :key="item">Name is {{item}}</li>
    </ul>
    <h1>Parent to child pass <p class="greenapple">{{fruit}}</p></h1>
    <button v-on:click="counter=counter+1">Add counter by JS code(NOT WORKING)</button>
    <h1>New way of showing or saving input data after v-model</h1>
    <input type="text" v-on:input="setName" placeholder="Type and it will appear">
    <h3>{{nameInput}}</h3>
    <h3>Submitting form by preventing default</h3>
    <form v-on:submit.prevent="submitForm">
        <input type="text" name="" id="">
        <input type="submit" value="Submit Form">
    </form>
<h1>Dynamic Styling</h1>
    <div>
        <div v-on:click="boxClick('A')" class="demobox" :class="selectedbox=='A'? 'activeBox':''"></div>
        <div v-on:click="boxClick('B')" class="demobox" :class="selectedbox=='B'? 'activeBox':''"></div>
        <div v-on:click="boxClick('C')" class="demobox" :class="selectedbox=='C'? 'activeBox':''"></div>
    </div>
    

</div>
</template>

<script>
export default {
    name: 'HomeComponent',
    props:{
        fruit: String
    },
    data() {
        return {
            email: "shahbazalivk@gmail.com",
            name: "Shahbaz",
            count: 10,
            show:true,
            technology:["Java","JavaScript","Python"],
            nameInput:'',
            selectedbox:"",
            // getName(a) {
            //     return a
            // }
        }
    },
    watch:{
        count(value){
            value>15 && console.log("Value > 15")
        }
    },
    methods: {
        getName(name) {
            return name
        },
        getData() {
            return {
                name: "Asif",
                emailOfAsif: this.email,
            }
        },
        getCount() {
            return this.count
        },
        addCount() {
            this.count+=1
        },
        subtractCount() {
            this.count-=1
        },
        changeCondition(){
            this.show=!this.show
        },
        setName(event){
            this.nameInput=event.target.value
        },
        submitForm(){
            alert("Submitted")
        },
        resetCount(){
            this.count=0
        },
        boxClick(box){
            this.selectedbox=box
            // console.log(this.selectedbox)
        }
    }
}
</script>
<style scoped>
.greenapple{
    color: green;
    display: inline;
}
.demobox{
    height: 6rem;
    width: 6rem;
    border: 2px dotted red;
    margin-top: 5px;
    margin-bottom: 5px;
}
.activeBox{
    background-color: orange;
    border: 2px solid rgb(112, 92, 56);
}
</style>