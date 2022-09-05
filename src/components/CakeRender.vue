<template>
    <div>
        <h3>Cake Render</h3>

        <div class="cake-layers">
            <div v-for="(layer , index) in myCake" :key="index" :class="layer.type" :style="{height:layer.layerHeight + 'cm'}">
                <p>{{index + 1}} : {{layer.type}}</p>

                <div class="cake-control">
                    <button class="blue" @click="decreaseHeightCakeRender(index)"><span>-</span></button>
                    <button class="blue" @click="increaseHeightCakeRender(index)"><span>+</span></button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    name: "cake-render",
    data() {
    },
    props: {
        myCake: {
            type: Array,
            required: true,
        },
    },
    methods: {
        decreaseHeightCakeRender(id) {
            this.$emit("decreaseHeightApp" , id)
        },
        increaseHeightCakeRender(id) {
            this.$emit("increaseHeightApp" , id)
        }
    },
}
</script>


<style scoped>
h3 {
    margin-bottom: 20px;
}
.cake-layers > * {
    min-height: 1cm;
    transition: 0.2s;
    border: 2px solid #000;
    position: relative;
}
.cake-layers > *:not(:last-child) {
    border-bottom: 0;
}
.cream {
    background: #FFEAD7;
}
.chocolate {
    background: #341717;
}
.fruit {
    background: #D9A6B9;
}
p {
    position: absolute;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    padding: 0 10px;
    background: #0d6efd;
    height: 25px;
    color: #fff;
    font-size: 12px;
    line-height: 12px;
    top: 0;
    left: 0;
}
.cake-control {
    position: absolute;
    right: 0;
    top: 0;
}
.cake-control button {
    border-radius: 0;
    padding: 0;
    width: 25px;
    height: 25px;
    font-size: 20px;
    line-height: 0;
    position: relative;
}
.cake-control > button:not(:last-child) {
    margin-right: 2px;
}
.cake-control > button:not(:last-child):after {
    content: "";
    right: -2px;
    top: 0;
    position: absolute;
    display: block;
    height: 100%;
    width: 2px;
    background: #3f9fff;
}
.cake-control button span {
    color: #fff;
}
.cake-control button.red span {
    display: block;
    transform: translateY(-1px);
}
</style>