<template>
    <div>
        <h3>Cake Builder</h3>

        <div class="cake-controllers">
            <div class="cake-controller" v-for="(controller , index) in myCake" :key="index">
                <div class="layer-title">
                    <h4>Layer Number : {{index + 1}} </h4>
                    <button class="red" @click="removeLayerCakeBuilder(index)">remove</button>
                </div>
                <div class="layer-settings">
                    <div class="layer-type">
                        <p>Type: </p>
                        <select name="" v-model="controller.type">
                            <option value="cream">Cream</option>
                            <option value="chocolate">Chocolate</option>
                            <option value="fruit">Fruit</option>
                        </select>
                    </div>
                    <div class="layer-height">
                        <p>Height:</p>
                        <input type="range" min="1" max="10" v-model="controller.layerHeight">        
                    </div>
                </div>
            </div>
            <div class="add">
                <button class="blue" @click="addLayerCakeBuilder">Add Layer</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "cake-builder",
    data() {

    },
    props: {
        myCake: {
            type: Array,
            required: true,
        },
    },
    methods: {
        removeLayerCakeBuilder(id) {
            this.$emit("removeLayerApp" , id)
        },
        addLayerCakeBuilder() {
            this.$emit("addLayerApp")
        }
    }
}
</script>


<style scoped>
h3 {
    margin-bottom: 20px;
}
.cake-controllers > .cake-controller:not(:last-child){
    margin-bottom: 10px;
}
.cake-controller {
    padding: 10px;
    border: 1px solid #ccc;
}
.cake-controller > *:not(:last-child) {
    border-bottom: 1px solid #ccc;
    padding-bottom: 10px;
    margin-bottom: 10px;
}
.layer-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.layer-settings {
    display: flex;
    align-items: flex-start;
}
.layer-settings p {
    margin-bottom: 5px;
}
.layer-settings > *:not(:last-child) {
    margin-right: 20px;
}
.add {
    margin-top: 20px;
}
.add button {
    width: 100%;
}
</style>

