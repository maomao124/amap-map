<template>
    <div>
        <div id="container"></div>
        <div v-show="map!=null">
            <button @click="set">设置中心点</button>
            <button @click="get">得到中心点</button>
            <button @click="setZoom">设置缩放级别</button>
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
            this.map.setCenter([100 + Math.random() * 22, 22 + Math.random() * 20])
        },
        get()
        {
            const center = this.map.getCenter()
            console.log(center)
            window.alert(center);
        },
        setZoom()
        {
            //3-20
            this.map.setZoom(3 + parseInt(Math.random() * 15 + ''))
            /*setInterval(() =>
            {
                this.map.setZoom(3 + parseInt(Math.random() * 15 + ''))
            }, 100)*/
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
    height: 90vh;
}
</style>
