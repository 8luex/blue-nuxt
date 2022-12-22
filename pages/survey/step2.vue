<template>
    <div>
        <v-app-bar
            color="primary accent-4"
            dense
            flat
            dark
        >
        <v-toolbar-title>Survey</v-toolbar-title>
        </v-app-bar>
        <v-container class="pt-0 pb-0">
            <v-row justify="center">
                <v-col cols="12" class="text-center">
                    <div class="mt-8 text-primary text-title">
                        Step 2 of 3
                    </div>
                </v-col>
                <v-col cols="10" class="text-center mt-1">
                    <h2 class="text-main">Which parts of the event did you enjoy?</h2>
                </v-col>
                <v-col cols="10" class="text-center">
                    <v-textarea
                        clearable
                        clear-icon="cancel"
                        label="Comments"
                        v-model="form.survey2"
                        :value="form.survey2"
                        color="deep-purple accent-1"    
                    >
                    </v-textarea>
                </v-col>
                <v-col cols="12" class="text-center">
                    <div class="set-padding">
                        <v-btn rounded color="primary" dark class="w-100 mt-15 my-btn" @click="next">
                            Next
                        </v-btn>
                        <div class="w-100 my-btn text-primary" @click="back">Back</div>
                    </div>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
export default {
    data() {
        return {
            form: {
                survey2: this.$store.getters.getSurvey.survey2
            }
        }
    },
    methods: {
        next() {
            this.$store.dispatch('setSurvey', this.form)
            this.$axios.patch(`https://blue-nuxt-default-rtdb.firebaseio.com/survey/line:001.json`, this.form).then((res) => {
                this.$router.push('/survey/step3')
            }).catch(e => console.log(e))
        },
        back() {
            this.$store.dispatch('setSurvey', this.form) //BLUE
            this.$router.push('/survey')
        },
    }
}
</script>