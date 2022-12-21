<template>
    <div>
        <v-app-bar
            color="primary accent-4"
            dense
            flat
            dark
        >
        <v-toolbar-title>Agenda</v-toolbar-title>
        </v-app-bar>
        <v-sheet elevation="6">
            <v-tabs
                grow
                v-model="tab" color="deep-purple accent-1"
            >
                <v-tab
                    v-for="item in agenda"
                    :key="item.date" 
                >
                    {{ item.date }}
                </v-tab>
            </v-tabs>
        </v-sheet>

        <v-tabs-items v-model="tab">
            <v-tab-item
                v-for="item in agenda"
                :key="item.date"
            >
                <v-container class="pt-0">
                    <v-row>
                        <v-col cols="12" v-for="session in item.sessions" :key="session.title">
                            <v-card class="agenda-card pt-0" :class="session.type == 'set' ? 'card-set': ''"> 
                                <v-card-text class="pt-2" v-if="session.type != 'set'">
                                    <p class="time mb-0 mt-0">{{ session.time }}</p>
                                    <div class="d-flex">
                                        <v-row>
                                            <v-col cols="4" class="text-center pb-0">
                                                <img :src="session.image" class="agenda-image" alt="">
                                            </v-col>
                                            <v-col cols="8" class="pb-0">
                                                <v-card-title class="pl-0 pt-0 pb-3 text-primary text-title uppercase">{{ session.title }}</v-card-title>
                                                <v-card-subtitle class="pl-0 pt-0 pb-0">{{ session.spaker }}</v-card-subtitle>
                                            </v-col>
                                        </v-row>
                                    </div>
                                    </v-card-text>
                                    <div v-else>
                                        <v-card-text v-for="sessionSet in session.sessionSet" :key="sessionSet.title">
                                            <p class="time mb-0">{{ session.time }}</p>
                                                <v-row>
                                                    <v-col cols="4" class="text-center pb-0">
                                                        <img :src="sessionSet.image" class="agenda-image" alt="">
                                                    </v-col>
                                                    <v-col cols="8" class="pb-0">
                                                        <v-card-title class="pl-0 pt-0 pb-3 text-primary text-title uppercase">{{ sessionSet.title }}</v-card-title>
                                                        <v-card-subtitle class="pl-0 pt-0 pb-0">{{ sessionSet.spaker }}</v-card-subtitle>
                                                        <p class="mb-0">{{ sessionSet.duringTime }}</p>
                                                    </v-col>
                                                </v-row>
                                            <hr v-if="sessionSet != session.sessionSet[session.sessionSet.length-1]" />
                                        </v-card-text>
                                    </div>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-container>
            </v-tab-item>
        </v-tabs-items>
    </div>
</template>

<script>
export default {
    data() {
        return {
            tab: null,
            items: [
                { tab: '20 March 20', content: 'Tab 1 Content'},
                { tab: '21 March 20', content: 'Tab 2 Content'},
            ]
        }
    },
    asyncData({ store }) {
        //apis
        return {
            agenda: store.getters.getAgenda
        }
    }
}
</script>

<style lang="scss" scoped>
.v-tabs {
    margin-bottom: 15px;
}
.v-tab {
    color: #888EA0 !important;
    font-weight: bold; 
    background: #E2E4F2;
    &.v-tab--active {
        color: #C397FF !important;
    }
    &+.v-tab {
        border-left: #B4B8C9 solid 1px;
    }
}
.agenda-card {
    .time {
        //margin-top: -8px;
        color: #C397FF !important;
        font-weight: bold; 
    }
    .agenda-image {
        width: 50px;
        height: 50px;
        object-fit: cover;
        border-radius: 50%;
    }
    &+.agenda-card {
        margin-top: 15px;
    }
    &.card-set {
        //padding-top: 5px;
        border-left: 3px solid #C397FF;
        .v-card__text.v-card__text {
            padding-top: 0 !important;
        }
    }
    hr {
        width: 90%;
        margin: 15px auto 0;
        height: 1px;
        border: 0;
        background: #E2E4F2;
    }
}
</style>
