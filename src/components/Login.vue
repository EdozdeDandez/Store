<template>
    <div class='container'>
        <div class="row">
            <div class="medium-6 columns ">
                <div class="primary callout border">
                    <form @submit.prevent="login()">
                        <div class="row">
                            <label>Name:
                                <input type="text" name="name" id="name" required v-model="name">
                            </label>
                            <label>Password:
                                <input type="password" name="password" id="password" required v-model="password">
                            </label>
                            <button type="submit" class="button">Login</button>
                            <a href="#" class="button clear">Cancel</a>
                        </div>
                    </form>
                    <div class="row">
                        Don't have account? <router-link :to="{ name: 'Register' }">Register</router-link> one now!
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'login',
        data(){
            return {
                name: '',
                password: '',
                errors: []
            }
        },
        methods: {
            login () {
                this.$store.dispatch('login', {
                    user: {
                        name: this.name,
                        password: this.password
                    }
                }).then(() => {
                    this.$router.push('/items')
                }).catch(e => {
                    this.errors.push(e)
                    console.log(e)
                })
            },
            authenticate (provider) {
                this.$store.dispatch('authenticate', { provider }).then(() => {
                    this.$router.push('/items')
                })
            }
        }
    }
</script>
<style lang="scss">
    .border {
        width: 95%;
        margin-left: auto;
        margin-right: auto;
    }
</style>