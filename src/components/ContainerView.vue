<template>
    <div v-if="step == 0">
        <post-view :data="item" v-for="(item, index) in data" :key="index"></post-view>
    </div>
    <!-- 필터선택페이지 -->
    <div v-if="step == 1">
        <div class="upload-image" :style="{ backgroundImage: `url(${ imgUrl }` }"></div>
        <div class="filters">
            <filter-box :filter="item" :imgUrl="imgUrl" v-for="item in filterList" :key="item">
                   {{ item }}
            </filter-box>
        </div>
    </div>

    <!-- 글작성페이지 -->
    <div v-if="step == 2">
        <div class="upload-image" :style="{ backgroundImage: `url(${ imgUrl })` }"></div>
        <div class="write">
            <textarea @input="$emit('write', $event.target.value)" class="write-box">write!</textarea>
        </div>
    </div>
</template>

<script>
import PostView from './PostView.vue'
import FilterBox from './FilterBox.vue'

export default {
    name : 'ContainerView',
    props: ['data', 'step', 'imgUrl'],
    data() {
        return {
            filterList: [ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", 
            "inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", 
            "reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"]
        }
    },
    components: {
        PostView,
        FilterBox,
    },
}
</script>

<style>
    .upload-image{
        width: 100%;
        height: 450px;
        background: cornflowerblue;
        background-size : cover;
    }
    .filters{
        overflow-x:scroll;
        white-space: nowrap;
    }
    .filter-1 {
        width: 100px;
        height: 100px;
        background-color: cornflowerblue;
        margin: 10px 10px 10px auto;
        padding: 8px;
        display: inline-block;
        color : white;
        background-size: cover;
    }
    .filters::-webkit-scrollbar {
        height: 5px;
    }
    .filters::-webkit-scrollbar-track {
        background: #f1f1f1; 
    }
    .filters::-webkit-scrollbar-thumb {
        background: #888; 
        border-radius: 5px;
    }
    .filters::-webkit-scrollbar-thumb:hover {
        background: #555; 
    }
    .write-box {
        border: none;
        width: 90%;
        height: 100px;
        padding: 15px;
        margin: auto;
        display: block;
        outline: none;
    }
</style>