<template>
    <div>
        <div v-if="loading" class="loader d-flex justify-content-center align-items-center">
            <h2 class="text-white text-center">Creating Account</h2>
        </div>
        <div class="register-form" v-if="!loading">
            <h1 class="text-center mb-4">Registration Page</h1>
            <form method="post" @submit.prevent="register">
                <div class="form-group">
                    <label for="">Full Name</label>
                    <input type="text" v-model="form.name" class="form-control">
                </div>

                <div class="form-group">
                    <label for="">Email</label>
                    <input type="email" v-model="form.email" class="form-control">
                </div>

                <div class="form-group">
                    <label for="">Password</label>
                    <input type="text" v-model="form.password" class="form-control">
                </div>

                <div class="form-group">
                    <label for="">Confirm Password</label>
                    <input type="text" v-model="form.password_confirmation" class="form-control">
                </div>
                <button type="submit" class="btn btn-primary w-100 rounded-0">Submit</button>
            </form>
        </div>
    </div>
</template>

<script>
import api from '@/helpers/api.js'
export default {
    data(){
        return{
            loading: false,
            form:{
                name: null,
                email: null,
                password: null,
                password_confirmation: null
            }
        }
    },
    methods: {
        async register(){
            this.loading = true;
            try {
                const response = await api.register(this.form);
                console.log(response);
                alert("Account registered succesfully, please, login");
                this.$router.push('/')
            } catch (error) {
                console.log(error.response);
            }
            finally{
                this.loading = false;
                this.form.name = null;
                this.form.email = null;
                this.form.password = null;
                this.form.password_confirmation = null;
            }
        }
    }
}
</script>

<style scoped>

</style>