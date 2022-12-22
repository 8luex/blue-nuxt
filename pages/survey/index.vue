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
            <v-row>
                <v-col cols="12" class="text-center">
                    <div class="mt-8 text-primary text-title">
                        Step 1 of 3
                    </div>
                </v-col>
            </v-row>
            <v-row justify="center">
                <v-col cols="10" class="text-center mt-1">
                    <h2 class="text-main">How would you rate the event overall?</h2>
                </v-col>
                <v-col cols="10">
                    <v-slider
                        class="slider"
                        v-model="form.survey1"
                        thumb-label="always"
                        :max="10"
                        :min="0"
                        track-color="grey lighten-1"
                    >
                    </v-slider>
                </v-col>
                <v-col cols="12" class="text-center">
                    <div class="set-padding">
                        <v-btn rounded color="primary" dark class="w-100 mt-15 my-btn" @click="next">
                            Next
                        </v-btn>
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
                survey1: this.$store.getters.getSurvey.survey1
            }
        }
    },
    methods: {
        next() {
            this.$store.dispatch('setSurvey', this.form)
            this.$axios.patch(`https://blue-nuxt-default-rtdb.firebaseio.com/survey/line:001.json`, this.form).then((res) => {
                this.$router.push('/survey/step2')
            }).catch(e => console.log(e))
        }
    }
}
</script>

<style lang="scss" scoped>
.slider {
    margin-top: 90px;
    ::v-deep {
        .v-slider__thumb {
            width: 15px;
            height: 15px;
        }
        .v-slider__thumb-label {
            font-size: 20px;
            width: 45px !important;
            height: 45px !important;
        }
        .v-slider__track-background {
            //
        }
        .v-slider--horizontal .v-slider__track-container {
            height: 4px;
        }
    }
}
</style>