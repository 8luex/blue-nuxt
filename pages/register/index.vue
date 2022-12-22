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
                    <div class="mt-8 text-primary text-title">
                        Step 1 of 2
                    </div>
                </v-col>
                <v-col cols="12" class="text-center pb-0">
                    <v-avatar size="155px">
                        <img v-if="getLine.pictureUrl == ''" src="~/assets/profile.jpg" alt="" width="155">
                        <img v-else :src="getLine.pictureUrl" alt="" width="155">
                    </v-avatar>
                </v-col>
                <v-col cols="12" class="text-center pt-2 pb-0">
                    {{ getLine.displayName }}
                </v-col>
                <v-col cols="12" class="text-center">
                    <v-form>
                        <v-text-field
                            v-model="form.firstname"
                            dense
                            label="Firstname"
                            color="deep-purple accent-1"                   
                        >
                        </v-text-field>
                        <v-text-field
                            v-model="form.lastname"
                            dense
                            label="Lastname"
                            color="deep-purple accent-1"
                        >
                        </v-text-field>
                        <div class="gender-group d-flex mt-3">
                            <p>Gender</p>
                            <div class="circle" :class="form.gender == 1 ? 'active' : ''" @click="chooseGender(1)">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="#FFFFFF" d="M21 9c0-4.97-4.03-9-9-9s-9 4.03-9 9c0 4.632 3.501 8.443 8 8.941v2.059h-3v2h3v2h2v-2h3v-2h-3v-2.059c4.499-.498 8-4.309 8-8.941zm-16 0c0-3.86 3.14-7 7-7s7 3.14 7 7-3.14 7-7 7-7-3.14-7-7z"/></svg>
                            </div>
                            <p>Female</p>
                            <div class="circle" :class="form.gender == 2 ? 'active' : ''" @click="chooseGender(2)">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="#FFFFFF" d="M16 2v2h3.586l-3.972 3.972c-1.54-1.231-3.489-1.972-5.614-1.972-4.97 0-9 4.03-9 9s4.03 9 9 9 9-4.03 9-9c0-2.125-.741-4.074-1.972-5.614l3.972-3.972v3.586h2v-7h-7zm-6 20c-3.86 0-7-3.14-7-7s3.14-7 7-7 7 3.14 7 7-3.14 7-7 7z"/></svg>
                            </div>
                            <p>Male</p>
                        </div>
                        <v-btn rounded color="primary" dark class="w-100 mt-10 my-btn" @click="next">
                            Next
                        </v-btn>
                    </v-form>
                </v-col>
            </v-row>
        </v-container>
        
    </div>
</template>

<script>
export default {
    mounted() {
        liff.init({
            liffId: '1657670230-1nZ27ANq'
        }).then(() => {
            if(liff.isLoggedIn()) {
                liff.getProfile().then(profile => {
                    // this.profile.pictureUrl = profile.pictureUrl
                    // this.profile.displayName = profile.displayName
                    // this.profile.userId = profile.userId
                    this.$store.dispatch('setLine', profile);
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
    },
    data() {
        return {
            form: {
                firstname: this.$store.getters.getRegister.firstname,
                lastname: this.$store.getters.getRegister.lastname,
                gender: this.$store.getters.getRegister.gender
            }
        }
    },
    methods: {
        isDone() {
            this.$axios.get(`https://blue-nuxt-default-rtdb.firebaseio.com/members/${this.$store.getters.getLine.userId}/profile.json`).then((res) => {
                if(res.data != null) {
                    this.$router.push('/register/done')
                }
            }).catch(e => console.log(e))
        },
        chooseGender(gender) {
            this.form.gender = gender
        },
        validate() {
            let validated = true
            const errors = []
            //let errorMsg = ''
            const validatorField = [
                'firstname',
                'lastname'
            ]
            validatorField.forEach((field) => {
                if(this.form[field] == '') {
                    validated = false
                    errors.push(`${field} can not be null`)
                }
            })
            if(!validated) {
                this.$store.dispatch('setDialog', {
                    isShow: true,
                    title: 'Form is error',
                    message: errors.map((error) => error+'<br/>').join('')
                })
            }
            //console.log(errorMsg)
            return validated
        },
        next() {
            if(this.validate()) {
                this.$store.dispatch('setRegister', this.form)
                this.$router.push('/register/step2') 
            }
        },
    }
}
</script>


<style lang="scss" scoped>
.v-form {
    padding: 0 10px;
}
.gender-group {
    p {
        margin-bottom: 0;
        align-self: center;
        margin-right: 20px;
    }
    .circle {
        width: 45px;
        height: 45px;
        background: #E1E4F2;
        color: white;
        border-radius: 50%;
        position: relative;
        margin-right: 7px;
        &.active {
            background: #C397FF;
        }
        svg {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
    }
}
</style>