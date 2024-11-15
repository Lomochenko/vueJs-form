<template>

    <form @submit.prevent="handleSubmit">
        <!-- email -->
        <label>Email:</label>
        <input type="email" v-model="email" required>
        <!-- password -->
        <label>Password:</label>
        <input type="password" v-model="password" required>
        <div v-if="passwordError" class="error">{{ passwordError }}</div>
        <!-- job type -->
        <label>Job:</label>
        <select v-model="role">
            <option value="developer">web developer</option>
            <option value="designer">web designer</option>
        </select>
        <!-- skills -->
        <label>Skills</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill">
        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="deleteSkill">{{ skill }}</span>
        </div>
        <!-- terms & conditions -->
        <div class="terms">
            <input type="checkbox" v-model="terms" required>
            <label>accept terms & conditions</label>
        </div>
        <!-- submit btn -->
        <div class="submit">
            <button>create an account</button>
        </div>
    </form>

    <p>Email: {{ email }}</p>
    <p>Password: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Terms: {{ terms }}</p>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'developer',
            terms: true,
            tempSkill: '',
            skills: [],
            passwordError: '',
        }
    },
    methods: {
        addSkill(e) {
            if (e.key == ',' && this.tempSkill) {
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        deleteSkill() {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
        handleSubmit() {
            // validate password
            this.passwordError = this.password.length > 5 ?
                '' : 'password must be more than 5 characters'

            if(!this.passwordError){
                console.log('email', this.email)
                console.log('password', this.password)
                console.log('role',this.role)
                console.log('skills',this.skills)
                console.log('terms accepted', this.terms)
            }
        }
    },
}

</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background-color: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: .6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input,
select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    color: #aaa;
    border: none;
    border-bottom: 1px solid #ddd;
}

input[type='checkbox'] {
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
    background-color: #eee;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
    border-radius: 20px;
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

.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: .8em;
    font-weight: bold;
}
</style>