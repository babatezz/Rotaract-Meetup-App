<template>
    <v-container fluid style="width: 100%">
        <v-layout>
            <v-flex xs12 class="text-xs-center">
                <v-progress-circular
                    :size="70"
                    :width="7"
                    color="amber"
                    indeterminate
                    v-if="loading"
                ></v-progress-circular>
            </v-flex>
        </v-layout>
        <v-layout 
            row 
            wrap  
            v-if="!loading"
            class="carousel-push">
            <v-flex xs12>
                <v-carousel align-center style="cursor: pointer;">
                    <v-carousel-item
                    v-for="meetup in meetups"
                    :src="meetup.imageUrl"
                    :key="meetup.id"
                    :perPage=1
                    @click="onLoadMeetup(meetup.id)"
                    reverse-transition="fade"
                    transition="fade"
                    style="height: 600px">
                    <div class="slide-title">
                        {{ meetup.title }}
                    </div>
                    </v-carousel-item>
                </v-carousel>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-flex>
                <v-card>
                    <v-card-title primary-title>
                        <div  class="attach">
                            <h3>THIS ARE THE ATTACHED MEETUPS</h3>
                        </div>
                    </v-card-title>
                </v-card>
            </v-flex>
        </v-layout>
        <v-layout row wrap mt-3>
            <v-flex xs12 sm6 class="text-xs-center text-sm-right">
                <v-btn large router to="/meetup" dark color="orange darken-2">EXPLORE MEETUPS</v-btn>
            </v-flex>
            <v-flex xs12 sm6 class="text-xs-center text-sm-left">
                <v-btn large router to="/meetup/new" dark color="red darken-1">ORGANISE MEETUPS</v-btn>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
export default {
    computed: {
        meetups () {
            return this.$store.getters.featuredMeetups
        },
        loading () {
            return this.$store.getters.loading
        }
    },
    methods: {
        onLoadMeetup (id) {
            this.$router.push('/meetup/' + id)
        }
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Open+Sans');

    .slide-title{
        text-align: center;
        background-color: rgba(0, 0, 0, 0.5);
        font-size: 2em;
        color: beige;
        position: absolute;
        bottom: 50px;
        padding: 20px;
    }

    .attach {
        margin: auto;
        text-align: center;
        font-size: 1.2em;
        font-family: 'Times New Roman', Times, serif;
        font-weight: bold;
    }

    .carousel-push {
        width: 100%;                                                                                                                                                                                                                                                                                                                                                                                                                
    }
</style>
