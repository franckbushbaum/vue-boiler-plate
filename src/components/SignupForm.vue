<template>
    <div>
    <form @submit="handleSubmit">

        <label>Email:</label>
        <input type="email" required v-model="email">

        <label>Password:</label>
        <input type="password" required v-model="password">

        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills:</label>
        <input type="text" v-model="temporarySkill" @keyup="addSkill" />
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill(skill)">{{ skill }}</span>
        </div>

        

        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>
    </form>
    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms Accepted: {{ terms }}</p>
    <p>Names: {{ names }}</p>
    </div>
</template>

<script>
export default {
    data(){
        return {
            email: 'mario',
            password: '',
            role: '',
            terms: false,
            temporarySkill: '',
            skills: [],
        }
    },
    methods: {
        addSkill(e){
            console.log('what is e.key?', e.key) 
            if (e.key === ',' && this.temporarySkill) {
                if(!this.skills.includes(this.temporarySkill)){
                    console.log('what is skill', this.temporarySkill.slice( 0, -1 ))
                    this.skills.push(this.temporarySkill.slice(0 , -1))
                }
            this.temporarySkill = ''
            }
        },
        deleteSkill(skill){
            this.skills = this.skills.filter((item) => {
    // if item matches skill passed down as prop we want to remove it.
    // return if skill in skills array is not equal to item. 
                return skill !== item
            })
        },
        handleSubmit(){
            console.log('form submitted')
        },
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
  }
  button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit {
    text-align: center;
}

</style>