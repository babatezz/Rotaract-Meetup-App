<template>
    <v-container>
        <v-layout row v-if="error">
            <v-flex offset-sm3 sm6 xs12>
                <app @dismissed="onDismissed" :text="error"></app>
            </v-flex>
        </v-layout>
        <v-layout mt-20 row>
            <v-flex offset-sm3 sm6 xs12>
                <v-card>
                    <v-card-text>
                        <v-container>
                            <form @submit.prevent="onSignUp">
                                <v-layout row>
                                    <v-flex xs12>
                                        <v-text-field
                                        name= "email"
                                        label="Mail"
                                        id="email"
                                        v-model="email"
                                        type="email"
                                        required
                                        >
                                        </v-text-field>
                                    </v-flex>
                                </v-layout>
                                <v-layout row>
                                    <v-flex xs12>
                                        <v-text-field 
                                        type="password"
                                        v-model="password"
                                        label="Password"
                                        id="password"
                                        name= "password"
                                        required
                                        >
                                        </v-text-field>
                                    </v-flex>
                                </v-layout>
                                <v-layout row>
                                    <v-flex xs12>
                                        <v-text-field 
                                        type="password"
                                        v-model="confirmPassword"
                                        label="Confirm Password"
                                        id="confirmPassword"
                                        name= "confirmPassword"
                                        :rules="[submitProfile]"
                                        >
                                        </v-text-field>
                                    </v-flex>
                                </v-layout>
                                <v-layout row>
                                    <v-flex xs12 sm6>
                                        <v-btn 
                                        type="submit" 
                                        class="info" 
                                        v-model="onSignUp"
                                        :loading="loading"
                                        :disabled="loading"
                                        @click="loader = 'loading'"
                                        >
                                        Sign Up
                                        <span slot="loader" class="custom-loader">
                                            <v-icon light>cached</v-icon>
                                        </span>
                                        </v-btn>
                                    </v-flex>
                                </v-layout> 
                            </form>
                        </v-container>
                    </v-card-text>
                </v-card>
            </v-flex>
        </v-layout>
    </v-container>
</template> 

<script>
import app from "@/components/shared/alert"
export default {
    data () {
        return {
            email: '',
            password: '',
            confirmPassword: ''
        }
    },
    computed: {
        submitProfile () {
            return this.password === this.confirmPassword ? true : 'Passwords doesn\'t match'
        },
        user () {
            return this.$store.getters.user
        },
        error () {
            return this.$store.getters.error
        },
        loading () {
            return this.$store.getters.loading
        }
    },
    watch: {//this is a vue directive used to watch the change of state of a set of values acquired from th ecomputed property
        user (value) {
            if (value !== null && value !== undefined) {
                return this.$router.push('/')
            }
        }
    },
    methods: {
        onSignUp () {
            //dispatch the store.actions function with the information to be passed to the form within the form's page 
            this.$store.dispatch('signUserUp', {email: this.email, password: this.password})
        },
        onDismissed () {
            this.$store.dispatch('clearError')
        }
    },
    components: {
        app
    }
}
</script>

<style scoped>
.custom-loader {
    animation: loader 1s infinite;
    display: flex;
  }
  @-moz-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-webkit-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-o-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }

</style>
