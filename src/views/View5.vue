<template>
    <div>
        <div id="container"></div>
        <div v-show="map!=null">
            <button @click="set">更改样式</button>
        </div>
    </div>
</template>

<script>
import {initAMap, destroy} from '../utils/amapUtils'

export default {
    name: "View1",
    data()
    {
        return {
            map: null,
            styleList: ["amap://styles/normal",
                "amap://styles/dark",
                "amap://styles/light",
                "amap://styles/whitesmoke",
                "amap://styles/fresh",
                "amap://styles/grey",
                "amap://styles/graffiti",
                "amap://styles/macaron",
                "amap://styles/blue",
                "amap://styles/darkblue",
                "amap://styles/wine"],
            styleIndex: 0,
        }
    },
    watch:
        {
            map(map)
            {
                console.log("map对象变化")
                map.on('complete', function ()
                {
                    //地图图块加载完成后触发
                    console.log("加载完成")
                });
            }
        },
    methods: {
        set()
        {
            if (this.styleIndex === this.styleList.length)
            {
                this.styleIndex = 0;
            }
            this.map.setMapStyle(this.styleList[this.styleIndex++]);
        }
    },
    created()
    {
        console.log("初始化")
        initAMap(this);
    },
    beforeDestroy()
    {
        console.log("销毁")
        destroy(this.map)
    },
}
</script>

<style scoped>
#container {
    padding: 0px;
    margin: 0px;
    width: 100%;
    height: 87vh;
}
</style>
