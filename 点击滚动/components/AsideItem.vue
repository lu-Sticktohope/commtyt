<template>
  <div :class="index===selectIndex?'aside_item_conatainer_active':'aside_item_conatainer'"
  v-on:click="onClick">
    <div :class="index===selectIndex?'aside_item_line_active':'aside_item_line'"></div>
    <div :class="index===selectIndex?'aside_item_title_active':'aside_item_title'">{{this.item.categorry_name}}</div>
  </div>
</template>

<script>
export default {
  props:{
    item:Object,
    index:Number,
    selectIndex:Number
  },
  methods:{
    onClick(){
      this.$emit("selectItem",this.index);
    }
  }
}
</script>

<style scoped>
.aside_item_conatainer
{
  width: 99%;
  /* border: 1px solid blue; */
  height: 60px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
}

.aside_item_line
{
  display: none;
}

.aside_item_title
{
  width: 90%;
  font-size: 16px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
}

.aside_item_conatainer_active
{
  width: 99%;
  /* border: 1px solid blue; */
  background-color: white;
  height: 60px;
  display: inline-flex;
  justify-content: flex-start;
  align-items: center;
}

.aside_item_title_active
{
  width: 90%;
  font-size: 20px;
  font-weight: 600;
  display: inline-flex;
  justify-content: center;
  align-items: center;
}

.aside_item_line_active
{
  width: 4px;
  height: 20px;
  background-color: red;
  display: block;
}

</style>