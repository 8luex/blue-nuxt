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
                    <div class="set-padding">
                        <img class="mt-12" src="~/assets/7566.jpg" alt="" width="235">
                        <h1 class="text-title mt-2">Thank you</h1>
                        <p class="mt-7 pl-6 pr-6">Thanks for completing this survey. your feedback will help us improve the next event.</p>
                        <div class="w-100 my-btn text-primary outlined mt-14" @click="close">Close</div>
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
        }
    },
    methods: {
        close() {
            liff.closeWindow();
        }
    }
}
</script>
