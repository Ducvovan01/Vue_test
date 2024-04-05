<script setup lang="ts">
import { Checkbox,Image} from 'ant-design-vue';
import { ref } from 'vue';
import { CaretUpOutlined,CaretDownOutlined} from '@ant-design/icons-vue';
const props = defineProps<{
  imageList: { id: number; url: string }[];
}>();

const checkedSellectall = ref(false);


</script>
<template>
    <div class="homepage">
    <div class="homepage_container">
        <div class="homepage_controller">
            <Checkbox v-model:checked="checkedSellectall" :style="{width: '400px', padding:'0 50px', marginRight:'50px'}">Sellect all</Checkbox>
            <div class="homepage_sort">
                <p class="homepage_sort-name">Name</p>
                <div class="homepage_sort-icon">
                    <CaretUpOutlined :style="{fontSize: '10px'}"/>
                    <CaretDownOutlined :style="{fontSize: '10px'}"/>
                </div>
            </div>
            <div class="homepage_sort">
                <p class="homepage_sort-name">Dimmension</p>
                <div class="homepage_sort-icon">
                    <CaretUpOutlined :style="{fontSize: '10px'}"/>
                    <CaretDownOutlined :style="{fontSize: '10px'}"/>
                </div>
            </div>
            <div class="homepage_sort">
                <p class="homepage_sort-name">Size</p>
                <div class="homepage_sort-icon">
                    <CaretUpOutlined :style="{fontSize: '10px'}"/>
                    <CaretDownOutlined :style="{fontSize: '10px'}"/>
                </div>
            </div>
        </div>
    
        <div class="homepage_list" v-for="image in props.imageList">
            <div class="homepage_item" :key="image.id">
                <div class="homepage_item-element image">
                    <Checkbox v-model:checked="checkedSellectall" :style="{width: '20px'}"></Checkbox>
                    <img
                    class="homepage_item-img"
                    :src="image.link" 
                  />
                </div>
                <div class="homepage_item-element">
                    <p class="homepage_column-name">{{image.name}}</p>
                </div>
                <div class="homepage_item-element">
                    <p class="homepage_column-imageSize">{{image.imageSize}}</p>
                </div>
                <div class="homepage_item-element">
                    <p class="homepage_column-physicalSize">{{image.physicalSize}}</p>
                </div>  
            </div>
        </div>
    </div>
    </div>

</template>

<style scoped>
.homepage_controller{
    display:flex;
}
.homepage_item-img{
    width: 300px;
    height: 120px;
    object-fit: cover;
    margin-right: 50px;
    border-radius: 10px;
}
.homepage{
    padding:0 50px;
}

.homepage_sort{
    display: flex;
    width: 200px;
}
.homepage_sort-icon{
    display: flex;
    flex-direction: column;
    padding-left: 3px;
    padding-top: 3px;
}
.homepage_list{

}
.homepage_item{
    display: flex;
    padding:20px 50px;
    cursor: pointer;
    border-radius: 5px;
}
.homepage_item:hover{
    background-color: #f7f4f4;
}
.homepage_item:hover .homepage_column-name{
    text-decoration: underline;
}
.homepage_item-element{
    width: 200px;
    display:flex;
    align-items: center;
}
.homepage_item-element.image{
    width: 400px;
    display: flex;

}
.homepage_column-name,.homepage_column-physicalSize,.homepage_column-imageSize{
    font-weight: 600;
    font-size: 18px;
}
</style>
