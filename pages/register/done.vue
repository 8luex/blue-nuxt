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
                    <div class="set-padding">
                        <img class="mt-12" src="~/assets/9814.jpg" alt="" width="220">
                        <h1 class="text-title mt-2">Welcome, {{ firstname }}</h1>
                        <p class="mt-7 pl-6 pr-6">Welcome to the event, Tons of workshop are waiting for you. We hope you have a good time here.</p>
                        <v-btn rounded color="primary" dark class="w-100 mt-10 my-btn" @click="workshop">
                            Register Workshop
                        </v-btn>
                        <div class="w-100 my-btn text-primary outlined mt-5" @click="close">Close</div>
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
            firstname: this.$store.getters.getRegister.firstname
        }
    },
    methods: {
        workshop() {
            this.$router.push('/workshop')
        },
        close() {
            liff.closeWindow();
        }
    }
}
</script>
