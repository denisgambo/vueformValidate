<template>
    <div class="container">
        <div class="card">
            <div class="card-header">
                <h3 class="card-title">Registration</h3>
            </div>
            <div class="card-body">
                <form @submit.prevent="onSubmit">
                    <div class="form-group">
                        <label>Your name</label>
                        <input v-model="v$.form.name.$model" type="text" class="form-control">
                        <div class="pre-icon os-icon os-icon-user-male-circle"></div>

                        <!-- Error Message -->
                        <div class="input-errors" v-for="(error, index) of v$.form.name.$errors" :key="index">
                            <div class="error-msg">{{ error.$message }}</div>
                        </div>
                    </div>

                    <div class="form-group" :class="{ error: v$.form.email.$errors.length }">
                        <label>Your email</label>
                        <input type="email" class="form-control" placeholder="your email" v-model="v$.form.email.$model">
                        <div class="pre-icon os-icon os-icon-user-male-circle"></div>

                        <!-- error message -->
                        <div class="input-errors" v-for="(error, index) of v$.form.email.$errors" :key="index">
                            <div class="error-msg">{{ error.$message }}</div>
                        </div>
                    </div>



                    <div class="form-group" :class="{ error: v$.form.password.$errors.length }">
                        <label>Your password</label>
                        <input type="password" class="form-control" placeholder="Enter your password"
                            v-model="v$.form.password.$model">
                        <div class="pre-icon os-icon os-icon-fingerprint"></div>

                        <!-- error message -->
                        <div class="input-errors" v-for="(error, index) of v$.form.password.$errors" :key="index">
                            <div class="error-msg">{{ error.$message }}</div>
                        </div>
                    </div>

                    <div class="form-goup">
                        <button :disabled="v$.form.$invalid" class="btn btn-primary"> Send</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import useVuelidate from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'

export function validName(name) {
    let validNamePattern = new RegExp("^[a-zA-Z]+(?:[-'\\s][a-zA-Z]+)*$");
    if (validNamePattern.test(name)) {
        return true;
    }
    return false;
}

export default {
    name: 'Registration',

    setup() {
        return { v$: useVuelidate() }
    },
    data() {
        return {
            form: {
                name: '',
                email: '',
                password: '',
            },

        }
    },

    methods: {
        onSubmit() {
            console.log("Validated")
        }
    },
    validations() {
        return {
            form: {
                name: {
                    required, name_validation: {
                        $validator: validName,
                        $message: 'Invalid Name. Valid name only contain letters, dashes (-) and spaces'
                    }
                },
                email: {
                    required, email
                },

                password: {
                    required,
                    min: minLength(6)
                },
            },
        }
    },
}
</script>