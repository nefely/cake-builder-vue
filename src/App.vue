<template>
  <div id="main-app">
    <div class="wrapper">
      <h1>Total Price: ${{totalPrice}}</h1>
    </div>
    <div class="wrapper df">
      <cake-render class="cake-render" :myCake="myCake" @decreaseHeightApp="decreaseHeightApp" @increaseHeightApp="increaseHeightApp"/>
      <cake-builder class="cake-builder" :myCake="myCake" @addLayerApp="addLayerApp" @removeLayerApp="removeLayerApp"/>
    </div>
  </div>
</template>

<script>
import CakeBuilder from "@/components/CakeBuilder";
import CakeRender from "@/components/CakeRender";
export default {
  name: 'App',
  data(){
    return {
      price: [
        {
          type: "cream",
          value: 3,
        },
        {
          type: "chocolate",
          value: 2,
        },
        {
          type: "fruit",
          value: 10,
        },
      ],
      myCake: [
        {
          type: "chocolate",
          layerHeight: 1,
        },
        {
          type: "cream",
          layerHeight: 2,
        },
        {
          type: "fruit",
          layerHeight: 3,
        },
        {
          type: "cream",
          layerHeight: 2,
        },
      ],
      totalPrice: 0,
    }
  },
  components: {
    CakeBuilder,
    CakeRender,
  },
  methods: {
    removeLayerApp(id) {
      this.myCake = this.myCake.filter((item, index) => {
        return index !== id ? item : null
      })
    },  
    addLayerApp() {
      this.myCake.push({
        type: "cream",
        layerHeight: 1,
      })
    }, 
    decreaseHeightApp(id) {
      if (this.myCake[id].layerHeight > 1) {
        this.myCake[id].layerHeight = Number(this.myCake[id].layerHeight) - 1
      }
    },
    increaseHeightApp(id) {
      if (this.myCake[id].layerHeight < 10) {
        this.myCake[id].layerHeight = Number(this.myCake[id].layerHeight) + 1
      }
    },
    countPrice() {
      // this.totalPrice = 0
      // for (var i in this.myCake) {
      //   for (var j in this.price) {
      //     if (this.myCake[i].type === this.price[j].type) {
      //       this.totalPrice += (this.myCake[i].layerHeight * this.price[j].cost)
      //     }
      //   }
      // }
      this.totalPrice = this.myCake.reduce((a , b) => a += (b.layerHeight * this.price.filter((c) => c.type === b.type ? c.value : null)[0].value), 0)
    }
  },
  mounted() {
    this.countPrice()
  },
  watch: {
    myCake: {
      handler: function() {
        this.countPrice()
      },
      deep: true
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  outline: none;
}
body * {
  font-size: 16px;
  line-height: 1.4em;
  color: #151515;
  font-family: sans-serif;
  border: 0;
}
h1 {
  font-size: 32px;
}
.wrapper {
  width: calc(100% - 40px);
  max-width: 1200px;
  margin: 20px auto;
}
.df {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
}
input,
select {
  padding: 5px 10px;
  color: inherit;
  height: 40px;
}
input[type="range"] {
  padding: 0px;
  border: 1px solid #ccc;
}
select {
  border: 1px solid #ccc;
}
button {
  padding: 5px 10px;
  font: inherit;
  border-radius: 6px;
  cursor: pointer;
}
button.red {
  background: #dc3545;
  color: #fff;
}
button.blue {
  background: #0d6efd;
  color: #fff;
}
button.green {
  background: #198754;
  color: #fff;
}
.cake-builder,
.cake-render {
  width: calc(50% - 10px);
}

@media screen and (max-width: 991px) {
  .wrapper {
    max-width: 600px;
  }
  .cake-render {
    margin-bottom: 20px;
  }
  .cake-builder,
  .cake-render {
    width: 100%;
  }
}
</style>
