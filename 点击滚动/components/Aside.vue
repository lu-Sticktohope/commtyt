<template>
  <div class="aside_container">
    <AsideItem v-for="(item,index) in category" 
    :key="index" 
    :item="item" 
    :index="index" 
    :selectIndex="selectIndex"
    v-on:selectItem="onSelectItem"/>
  </div>
</template>

<script>
import AsideItem from "../components/AsideItem";

export default {
  components:{
    AsideItem
  },
  props:{
    category:Array,
    selectIndex:Number
  },
  data(){
    return{
      // selectIndex:0
    }
  },
  methods:{
    onSelectItem(index){
      
      this.selectIndex = index;
      this.$emit("selectItem",this.selectIndex);
    }
  }
}
</script>

<style scoped>
.aside_container
{
  width: 25%;
  /* height: 800px; */
  background-color: rgb(246, 246, 246);
  position: fixed;
  top: 0px;
  left: 0px;
}
</style>