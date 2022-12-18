<template>
    <div>
        <v-app-bar
            color="primary accent-4"
            dense
            flat
            dark
        >
        <v-toolbar-title>Register</v-toolbar-title>
        </v-app-bar>
        <v-container class="pt-0 pb-0">
            <v-row>
                <v-col cols="12" class="text-center">
                    <div class="mt-5 mb-0 text-primary text-title">
                        20 December 2022
                    </div>
                </v-col>
                <v-col cols="12">
                    <Card
                        :active="selectedWorkshop==1"
                        v-on:moreDetail="moreDetail"
                        v-on:chooseWorkshop="chooseWorkshop(1)"
                    />
                    <Card
                        :active="selectedWorkshop==2"
                        v-on:moreDetail="moreDetail"
                        v-on:chooseWorkshop="chooseWorkshop(2)"
                    />
                </v-col>
                <v-col cols="12" class="text-center">
                    <div class="set-padding">
                        <v-btn rounded color="primary" dark class="w-100 mt-1 my-btn" @click="next">
                            Next
                        </v-btn>
                    </div>
                </v-col>
            </v-row>
            <v-dialog v-model="dialog" max-width="290">
                <v-card class="dialog-card">
                    <v-img
                        class="white--text align-end"
                        height="200px"
                        src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
                    >
                    </v-img>
                    <v-card-title class="headline">Design Thinking 1</v-card-title>
                    <v-card-text>
                        <p>Time: 13:00 - 16:00</p>
                        <p>Place: Room 101</p>
                        <p class="detail">Design Thinking is a design methodology that provides a solution-based approach to solving problems. We will focus on the five-stage Design Thinking model. Empathise, Define (th problem), Ideate, Prototype and Test.</p>
                        <p>Speaker <br/>-Mr. John David <br/>-Mr. David Round</p>
                    </v-card-text>
                    <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn class="text-primary" text @click="dialog = false">
                            OK
                        </v-btn>
                    </v-card-actions>
                </v-card>
            </v-dialog>
        </v-container>
    </div>
</template>

<script>
import Card from '~/components/Card'
export default {
    components: {
        Card
    },
    data() {
        return {
            dialog: false,
            selectedWorkshop: 0
        }
    },
    methods: {
        next() {

        },
        moreDetail() {
            this.dialog = true
        },
        chooseWorkshop(id) {
            this.selectedWorkshop = id
        }
    }
}
</script>

<style lang="scss" scoped>
.dialog-card {
    p {
        margin-bottom: 0;
    }
    .v-card__title.headline {
        font-size: 20px !important;
    }
    .v-card__text {
        padding-bottom: 0;
    }
    .detail {
        margin: 10px 0;
    }
}
</style>