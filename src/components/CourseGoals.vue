<template>
<div class="goalsMain">
    <div>
    <h1 class="coursegoalheading">Vue Course <br> Goals</h1>
    <div class="mcgoals">
        <h2>My Course Goals</h2>
        <input v-model="typedGoal" type="text" placeholder="Type Goal">
        <button v-on:click="addGoal()" class="addgoalbutton">Add Goal</button>
        <br>
        <br>
        <p v-if="goals.length===0">No goals have been added yet. <br> Start adding some.</p>
        <!-- <br>
        <br> -->
        <ul v-else>
            <li @click="removeGoal(index)" class="goalbutton" v-for="(goal,index) in goals" :key=goal> {{index+1}}) {{goal}} <input @click.stop type="text" name="" id=""> </li>
        </ul>
    </div>
    </div>
</div>
<br>
<br>
<br>
<br>
</template>

<script>
export default {
    name: "CourseGoals",
    data() {
        return {
            goals: [],
            typedGoal: "",
        }
    },
    methods: {
        addGoal() {
            this.typedGoal != "" && this.goals.push(this.typedGoal)
        },
        removeGoal(index){
            this.goals.splice(index,1)
            console.log(this.goals)
        }
    }
}
</script>

<style scoped>
.goalsMain {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    
}
.goalsMain>div{
    background-color: rgba(89, 89, 89, 0.364);
    padding: 2rem 4rem;
    border-radius: 26px;

}
.coursegoalheading {
    text-align: center;
    background-color: rgb(71, 120, 71);
    padding: 2.5rem;
    color: white;
    border-radius: 18px;
}

.mcgoals {
    border-radius: 18px;
    padding: 20px;
    border: 6px solid rgb(50, 118, 72);
    /* background-color: aquamarine; */
}

.mcgoals>h2 {
    color: rgb(72, 104, 72);
    font-weight: bolder;
    font-size: 32px;
}

.mcgoals>input {
    color: rgb(72, 104, 72);
    font-weight: bolder;
    font-size: 22px;
    border: 2px solid gray;
    padding: 6px;

}

.addgoalbutton {
    background-color: rgb(210, 56, 81);
    color: white;
    font-size: 22px;
    border: none;
    padding: 6px;
}

.goalbutton {
    padding: 1rem 5rem 1rem 5rem;
    font-size: 24px;
    color: white;
    background-color: rgba(53, 161, 53, 0.533);
    color: black;
    border-radius: 40px;
}
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

li {
  margin: 0;
  padding: 0;
  margin-bottom: 20px;
}

</style>
