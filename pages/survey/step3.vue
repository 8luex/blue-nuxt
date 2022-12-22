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
                        Step 3 of 3
                    </div>
                </v-col>
                <v-col cols="10" class="text-center mt-1">
                    <h2 class="text-main">Finally, would you recommend our event to a friend?</h2>
                </v-col>
                <v-col cols="11" class="mt-1">
                    <div class="select" :class="form.survey3 == 1 ? 'active' : ''" @click="form.survey3 = 1">
                        <h1>Of course!</h1>
                        <p>Definitely I'll join next event.</p>
                        <v-icon>check</v-icon>
                    </div>
                    <div class="select" :class="form.survey3 == 2 ? 'active' : ''" @click="form.survey3 = 2">
                        <h1>Not sure</h1>
                        <p>Let me think again next time.</p>
                        <v-icon>check</v-icon>
                    </div>
                    <div class="select" :class="form.survey3 == 3 ? 'active' : ''" @click="form.survey3 = 3">
                        <h1>No, thanks</h1>
                        <p>It's not my type.</p>
                        <v-icon>check</v-icon>
                    </div>
                </v-col>
                <v-col cols="12" class="text-center">
                    <div class="set-padding">
                        <v-btn rounded color="primary" dark class="w-100 mt-5 my-btn" @click="submit">
                            Submit
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
                survey3: this.$store.getters.getSurvey.survey3
            }
        }
    },
    methods: {
        submit() {
            this.$store.dispatch('setSurvey', this.form)
            this.$axios.patch(`https://blue-nuxt-default-rtdb.firebaseio.com/survey/line:001.json`, this.form).then((res) => {
                this.$router.push('/survey/done')
            }).catch(e => console.log(e))
        },
        back() {
            this.$store.dispatch('setSurvey', this.form) //BLUE
            this.$router.push('/survey/step2')
        },
    }
}
</script>

<style lang="scss" scoped>
.select {
    border-bottom: 1px solid #BDBDBD;
    padding-bottom: 25px;
    color: #BDBDBD;
    position: relative;
    &.select {
        margin-top: 20px;
    }
    &.active {
        color: #C397FF;
        .v-icon {
            color: #C397FF;
            display: block;
        }
    }
    h1 {
        font-size: 20px;
    }
    p {
        font-size: 18px;
        margin-bottom: 0;
    }
    .v-icon {
        position: absolute;
        right: 0;
        bottom: 25px;
        display: none;
    }
}
</style>