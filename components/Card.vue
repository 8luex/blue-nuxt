<template>
    <v-card class="mx-auto" :class="active == true ? 'active': ''" max-width="400">
        <v-img
            class="white--text align-end"
            height="200px"
            src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
        >
            <div class="more-detail" @click="$emit('moreDetail')">More Detail</div>
        </v-img>
        <div class="card-content">
            <div>
                <v-card-text class="text--primary">
                    <h1>{{ session.title }}</h1>
                </v-card-text>
                <v-card-subtitle class="pt-0">{{ session.spaker }}</v-card-subtitle>
            </div>
            <v-btn class="circle" @click="$emit('chooseWorkshop')">
                <v-icon>check</v-icon>
            </v-btn>
        </div>
    </v-card>
</template>

<script>
export default {
    props: ['active', 'session']
}
</script>


<style lang="scss" scoped>
.circle {
    width: 32px !important;
    height: 32px !important;
    min-width: auto !important;
    border-radius: 50%;
    color: white;
    background: rgba($color: #C397FF, $alpha: 0.3) !important;
    align-self: center;
}
.card-content {
    display: flex;
    justify-content: space-between;
    padding: 15px;
}
.more-detail {
    font-size: 12px;
    color: #C397FF;
    border-radius: 25px;
    background-color: white;
    padding: 10px 20px;
    font-weight: bold;
    display: inline;
    position: absolute;
    bottom: 10px;
    right: 10px;
}
.v-card__subtitle {
    padding: 0;
}
.v-card__text {
    padding: 0;
    padding-bottom: 5px;
    h1 {
        font-size: 24px;
    }
}
.v-card+.v-card {
    margin-top: 25px;
}
.v-card.active {
    .circle {
        background: #C397FF !important;
    }
    .v-image {
        &::before {
            width: 100%;
            height: 100%;
            content: 'Selected';
            font-weight: bold;
            font-size: 24px;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #C397FF;
        }
    }
}
</style>