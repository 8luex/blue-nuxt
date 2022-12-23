<template>
    <div>
        <v-app-bar
            color="primary accent-4"
            dense
            flat
            dark
        >
        <v-toolbar-title>Reward Card</v-toolbar-title>
        </v-app-bar>
        <v-container class="pt-0 pb-0">
            <v-row>
                <v-col cols="12" class="text-center">
                    <v-card class="mt-8">
                        <v-card-text>
                            <div class="d-flex">
                                <div>
                                    <v-avatar size="40px">
                                        <img v-if="getLine.pictureUrl == ''" src="~/assets/profile.jpg" alt="" width="40">
                                        <img v-else :src="getLine.pictureUrl" alt="" width="40">
                                    </v-avatar>
                                </div>
                                <div class="align-self-center">
                                    <h2 class="text-main name text-primary">{{ getProfile.firstname }} {{ getProfile.lastname }}</h2>
                                </div>
                            </div>
                        </v-card-text>
                        <div class="stamp-zone">
                            <div class="stamp" v-for="(obj, index) in stamps" :key="index">
                                <div class="circle" :class="obj.value == true ? 'active' : ''" v-if="index != Object.keys(stamps).length-1">
                                    <span>{{ index+1 }}</span>
                                    <v-icon>gavel</v-icon>
                                </div>
                                <div class="circle end" :class="obj.value == true ? 'active' : ''" v-else>
                                    <span>GOAL</span>
                                    <v-icon>gavel</v-icon>
                                </div>
                            </div>
                        </div>
                    </v-card>
                </v-col>
                <v-col cols="12" class="text-center">
                    <div class="set-padding">
                        <v-btn v-if="isCompleted == false" rounded color="primary" dark class="w-100 mt-6 my-btn" @click="scan">
                            <svg class="mr-2" xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 28 28"><defs><style>.a{fill:#fff;}</style></defs><path class="a" d="M1.641,1.641H6.563V0H0V6.563H1.641Zm0,0"/><path class="a" d="M392,0V1.641h4.922V6.563h1.641V0Zm0,0" transform="translate(-370.563)"/><path class="a" d="M396.922,396.922H392v1.641h6.563V392h-1.641Zm0,0" transform="translate(-370.563 -370.563)"/><path class="a" d="M1.641,392H0v6.563H6.563v-1.641H1.641Zm0,0" transform="translate(0 -370.563)"/><path class="a" d="M61,60v8.2h8.2V63.281h1.641V61.641H69.2V60Zm6.563,6.563H62.641V61.641h4.922Zm0,0" transform="translate(-57.664 -56.719)"/><path class="a" d="M280.844,279.844v-8.2h-3.281V270h-1.641v1.641H271v1.641h1.641v1.641H271v1.641h1.641v3.281Zm-6.563-6.563H279.2V278.2h-4.922Zm0,0" transform="translate(-256.18 -255.234)"/><path class="a" d="M65.922,241.641H69.2V240H61v1.641h3.281v1.641H62.641v1.641h1.641V248.2H62.641v1.641h1.641v1.641h8.2v-1.641H70.844V248.2H69.2v1.641H65.922V248.2h1.641v-1.641H65.922Zm0,0" transform="translate(-57.664 -226.875)"/><path class="a" d="M121,120h1.641v1.641H121Zm0,0" transform="translate(-114.383 -113.438)"/><path class="a" d="M361,120h1.641v1.641H361Zm0,0" transform="translate(-341.258 -113.438)"/><path class="a" d="M305.922,68.2H309.2V60H301v8.2h3.281v1.641h1.641Zm-3.281-1.641V61.641h4.922v4.922Zm0,0" transform="translate(-284.539 -56.719)"/><path class="a" d="M394.281,241.641V240H391v1.641Zm0,0" transform="translate(-369.617 -226.875)"/><path class="a" d="M361,360h1.641v1.641H361Zm0,0" transform="translate(-341.258 -340.313)"/><path class="a" d="M241,330h1.641v1.641H241Zm0,0" transform="translate(-227.82 -311.953)"/><path class="a" d="M181,303.281h1.641V300H181Zm0,0" transform="translate(-171.102 -283.594)"/><path class="a" d="M211,270h1.641v1.641H211Zm0,0" transform="translate(-199.461 -255.234)"/><path class="a" d="M62.641,330H61v3.281h1.641Zm0,0" transform="translate(-57.664 -311.953)"/><path class="a" d="M61,420h1.641v1.641H61Zm0,0" transform="translate(-57.664 -397.031)"/><path class="a" d="M241,60h1.641v1.641H241Zm0,0" transform="translate(-227.82 -56.719)"/><path class="a" d="M241,123.281h1.641V120H241Zm0,0" transform="translate(-227.82 -113.438)"/><path class="a" d="M242.641,211.641V210H241v3.281h6.563v-1.641Zm0,0" transform="translate(-227.82 -198.516)"/></svg>
                            Scan to collect
                        </v-btn>
                        <div v-if="isCompleted == false" class="w-100 my-btn-disabled text-disabled outlined mt-5">Redeem Reward</div>
                        <v-btn v-if="isCompleted == true" rounded color="grey lighten-1" dark class="w-100 mt-6 my-btn">
                            <svg class="mr-2" xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 28 28"><defs><style>.a{fill:#fff;}</style></defs><path class="a" d="M1.641,1.641H6.563V0H0V6.563H1.641Zm0,0"/><path class="a" d="M392,0V1.641h4.922V6.563h1.641V0Zm0,0" transform="translate(-370.563)"/><path class="a" d="M396.922,396.922H392v1.641h6.563V392h-1.641Zm0,0" transform="translate(-370.563 -370.563)"/><path class="a" d="M1.641,392H0v6.563H6.563v-1.641H1.641Zm0,0" transform="translate(0 -370.563)"/><path class="a" d="M61,60v8.2h8.2V63.281h1.641V61.641H69.2V60Zm6.563,6.563H62.641V61.641h4.922Zm0,0" transform="translate(-57.664 -56.719)"/><path class="a" d="M280.844,279.844v-8.2h-3.281V270h-1.641v1.641H271v1.641h1.641v1.641H271v1.641h1.641v3.281Zm-6.563-6.563H279.2V278.2h-4.922Zm0,0" transform="translate(-256.18 -255.234)"/><path class="a" d="M65.922,241.641H69.2V240H61v1.641h3.281v1.641H62.641v1.641h1.641V248.2H62.641v1.641h1.641v1.641h8.2v-1.641H70.844V248.2H69.2v1.641H65.922V248.2h1.641v-1.641H65.922Zm0,0" transform="translate(-57.664 -226.875)"/><path class="a" d="M121,120h1.641v1.641H121Zm0,0" transform="translate(-114.383 -113.438)"/><path class="a" d="M361,120h1.641v1.641H361Zm0,0" transform="translate(-341.258 -113.438)"/><path class="a" d="M305.922,68.2H309.2V60H301v8.2h3.281v1.641h1.641Zm-3.281-1.641V61.641h4.922v4.922Zm0,0" transform="translate(-284.539 -56.719)"/><path class="a" d="M394.281,241.641V240H391v1.641Zm0,0" transform="translate(-369.617 -226.875)"/><path class="a" d="M361,360h1.641v1.641H361Zm0,0" transform="translate(-341.258 -340.313)"/><path class="a" d="M241,330h1.641v1.641H241Zm0,0" transform="translate(-227.82 -311.953)"/><path class="a" d="M181,303.281h1.641V300H181Zm0,0" transform="translate(-171.102 -283.594)"/><path class="a" d="M211,270h1.641v1.641H211Zm0,0" transform="translate(-199.461 -255.234)"/><path class="a" d="M62.641,330H61v3.281h1.641Zm0,0" transform="translate(-57.664 -311.953)"/><path class="a" d="M61,420h1.641v1.641H61Zm0,0" transform="translate(-57.664 -397.031)"/><path class="a" d="M241,60h1.641v1.641H241Zm0,0" transform="translate(-227.82 -56.719)"/><path class="a" d="M241,123.281h1.641V120H241Zm0,0" transform="translate(-227.82 -113.438)"/><path class="a" d="M242.641,211.641V210H241v3.281h6.563v-1.641Zm0,0" transform="translate(-227.82 -198.516)"/></svg>
                            Scan to collect
                        </v-btn>
                        <v-btn v-if="isCompleted == true" rounded color="primary" dark class="w-100 mt-6 my-btn" @click="redeem">Redeem Reward</v-btn>
                    </div>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
// CommonJS require
export default {
    mounted() {
        liff.init({
            liffId: '1657670230-Leka1m9K'
        }).then(() => {
            if(liff.isLoggedIn()) {
                liff.getProfile().then(profile => {
                    // this.profile.pictureUrl = profile.pictureUrl
                    // this.profile.displayName = profile.displayName
                    // this.profile.userId = profile.userId
                    this.$store.dispatch('setLine', profile);
                    // this.$axios.get(`https://blue-nuxt-default-rtdb.firebaseio.com/members/${this.$store.getters.getLine.userId}/profile.json`).then((res) => {
                    //     this.$store.dispatch('setProfile', res.data);
                    // });
                    this.isDone();
                })
            } else {
                liff.login();
            }
        })
    },
    computed: {
        getLine() {
            return this.$store.getters.getLine;
        },
        getProfile() {
            return this.$store.getters.getProfile;
        },
        isCompleted() {
            let isCompleted = true;
            this.stamps.forEach(ele => { 
                if(ele.value === false) {
                    isCompleted = false;
                    return isCompleted;
                }
            })
            return isCompleted;
        }
    },
    methods: {
        isDone() { //not yet
            this.$axios.get(`https://blue-nuxt-default-rtdb.firebaseio.com/members/${this.$store.getters.getLine.userId}/profile.json`).then((res) => {
                if(res.data != null) {
                    this.$store.dispatch('setProfile', res.data);
                    // this.profile.firstname = res.data.firstname;
                    // this.profile.lastname = res.data.lastname;
                }
            }).catch(e => console.log(e))

            this.$axios.get(`https://blue-nuxt-default-rtdb.firebaseio.com/rewards/${this.$store.getters.getLine.userId}.json`).then((res) => {
                if(res.data != null) {
                    this.stamps = res.data
                }
            }).catch(e => console.log(e))
        },
        scan() {
            liff.scanCodeV2().then(result => { //ios
                // alert(result.value);
                this.stamps = this.stamps.map((obj) => {
                    if(obj.name == result.value) {
                        obj.value = true;
                    }
                    return obj;
                })
                this.$axios.patch(`https://blue-nuxt-default-rtdb.firebaseio.com/rewards/${this.$store.getters.getLine.userId}.json`, {...this.stamps}).then((res) => {
                }).catch(e => alert.log(e))
            }).catch(e => alert(e))
        },
        redeem() {
            this.$router.push('reward/done');
        }
    },
    data() {
        return {
            stamps: [
                {
                    name: 'stamp1',
                    value: false
                },
                {
                    name: 'stamp2',
                    value: false
                },
                {
                    name: 'stamp3',
                    value: false
                },
                {
                    name: 'stamp4',
                    value: false
                },
                {
                    name: 'stamp5',
                    value: false
                },
                {
                    name: 'stamp6',
                    value: false
                },
                {
                    name: 'stamp7',
                    value: false
                },
                {
                    name: 'stamp8',
                    value: false
                },
                
            ]
        }
    }
}
</script>

<style lang="scss" scoped>
.name {
    margin-left: 15px;
}
.v-card__text {
    padding: 15px 15px;
}
.stamp-zone {
    background: #E2E4F2;
    padding: 30px 30px 10px 40px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
.stamp {
    flex-basis: 25%;
}
.circle {
    width: 55px;
    height: 55px;
    background: white;
    border-radius: 50%;
    border: 2px solid #C397FF;
    justify-content: center;
    display: inline-flex;
    margin-bottom: 25px;
    margin-right: 15px;
    .v-icon {
        display: none;
    }
    &.active {
        background: #C397FF;
        span {
            display: none;
        }
        .v-icon {
            color: white;
            display: flex;
        }
    }
    &.end {
        background: #C397FF;
        span {
            font-size: 18px;
            color: white;
        }
    }
    span {
        align-self: center;
        font-size: 20px;
        color: #C397FF;
        font-weight: bold;
    }
}
</style>