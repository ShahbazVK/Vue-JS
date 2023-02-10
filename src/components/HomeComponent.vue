<template>
    <div>
        <h2>Home component</h2>
        <h2>{{email}}</h2>
        <h2>{{name}}</h2>
        <h2>{{getName("Rizwan")}}</h2>
    </div>
</template>

<script>
export default {
    name:'HomeComponent',
    data(){
        return {
            email:"shahbazalivk@gmail.com",
            name:"Shahbaz",
            getName(a){
                return a
            }
        }
    }
}
</script>