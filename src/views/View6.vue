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
        initAMap(this, undefined, {
            pitch: 50, //地图俯仰角度，有效范围 0 度- 83 度
            viewMode: '3D', //地图模式
            rotateEnable: true, //是否开启地图旋转交互 鼠标右键 + 鼠标画圈移动 或 键盘Ctrl + 鼠标左键画圈移动
            pitchEnable: true, //是否开启地图倾斜交互 鼠标右键 + 鼠标上下移动或键盘Ctrl + 鼠标左键上下移动
            zoom: 17, //初始化地图层级
            rotation: -15, //初始地图顺时针旋转的角度
            zooms: [2, 20], //地图显示的缩放级别范围
            center: [116.333926, 39.997245] //初始地图中心经纬度
        });
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
