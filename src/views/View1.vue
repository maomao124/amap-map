<template>
    <div>
        <div id="container"></div>
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
    methods: {},
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
