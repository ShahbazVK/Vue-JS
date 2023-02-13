<template>
<section id="app">
    <ul>
        <li v-for="(friend,index) in friends" :key='index'>

            <h2>{{friend.name}}</h2>
            <button @click="toggleDetails(index)">{{friend.show?'Hide':'Show'}} Details</button>
            <ul v-if="friend.show">
                <li><strong>Phone:</strong> {{friend.phone}}</li>
                <li><strong>Email:</strong> {{friend.email}}</li>
            </ul>
        </li>
    </ul>
</section>
</template>

<script>
export default {
    name: "FriendsApp",
    data() {
        return {
            friends: [{
                    id: 0,
                    name: "Shahbaz",
                    phone: "832 238 3484",
                    email: "shahbazali@localhost.com",
                    show:false
                },
                {
                    id: 1,
                    name: "Ali",
                    phone: "895 5438 3484",
                    email: "ali@localhost.com",
                    show:false

                },
                {
                    id: 2,
                    name: "Shahzad",
                    phone: "804 453 3484",
                    email: "shahzad@localhost.com",
                    show:false

                },
            ],
            // detailsAreVisible:false
        }
    },
    methods: {
        toggleDetails(index){
            // this.detailsAreVisible=!this.detailsAreVisible
            this.friends[index].show=!this.friends[index].show
        },
    }
}

</script>

<style scoped>
* {
    box-sizing: border-box;
}

html {
    font-family: 'Jost', sans-serif;
}

body {
    margin: 0;
}

header {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    margin: 3rem auto;
    border-radius: 10px;
    padding: 1rem;
    background-color: #58004d;
    color: white;
    text-align: center;
    width: 90%;
    max-width: 40rem;
}

#app ul {
    margin: 0;
    padding: 0;
    list-style: none;
}

#app li {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    margin: 1rem auto;
    border-radius: 10px;
    padding: 1rem;
    text-align: center;
    width: 90%;
    max-width: 40rem;
}

#app h2 {
    font-size: 2rem;
    border-bottom: 4px solid #ccc;
    color: #58004d;
    margin: 0 0 1rem 0;
}

#app button {
    font: inherit;
    cursor: pointer;
    border: 1px solid #ff0077;
    background-color: #ff0077;
    color: white;
    padding: 0.05rem 1rem;
    box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
    background-color: #ec3169;
    border-color: #ec3169;
    box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}
</style>
