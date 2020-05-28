<template>
  <div class="home">
    <Aside :category="category"
    v-on:selectItem="onSelectItem"
    :selectIndex="selectIndex"/>
    <div class="right_container">
      <div v-for="(item,i) in category"
      :key="i"
      ref="category">
       <div class="title">{{i}}</div>
       <div class="category_container">
          <div v-for="(categoryItem,j) in category[i].categorry_items"
        :key="j"
        class="category_item_container">
          <img :src="categoryItem.item_icon"/>
          <div>{{categoryItem.item_name}}</div>
        </div>
       </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Aside from "../components/Aside";

export default {
  name: 'Home',
  components: {
    Aside
  },
  data(){
    return{
      category:[],
      selectIndex:0,
      categoryItems:[]
    }
  },
  methods:{
    onSelectItem(index){
      window.console.log("当前选中下标：",index);
      // this.selectIndex = index;
      // this.categoryItems = this.category[this.selectIndex].categorry_items;
      // window.console.log(this.$refs.category)
      var elements = this.$refs.category;
      var offSetTop = elements[index].offsetTop

      // document.documentElement.scrollTo(c);
      window.scrollTo({
        top:offSetTop,
        behavior:'smooth'
      })
    
    
    }
  },
  mounted(){
    axios.get("http://localhost:8080/category.json").then((response)=>{
      window.console.log(response);
      this.category = response.data;
      this.categoryItems = this.category[this.selectIndex].categorry_items
    }).catch((error)=>{
      window.console.log(error)
    });


    
    

    window.addEventListener("scroll",()=>{

      // window.console.log(document.documentElement.scrollHeight)
      // window.console.log(document.documentElement.scrollTop)
      //获取当前滚动的距离
      var elements = this.$refs.category;
      var scrollTop = document.documentElement.scrollTop;
      elements.forEach((element,index)=>{
         if (scrollTop >= element.offsetTop) {
             this.selectIndex = index
         }
      })

    })
  }
}
</script>

<style scoped>
.home
{
  display: inline-flex;
  justify-content: flex-end;
  align-items: flex-start;
  width: 100%;
}

.right_container
{
  width: 75%;
  /* height: 800px; */
  background-color: yellow;
}

img
{
  width: 80px;
  height: 80px;
}

.category_container
{
  width: 100%;
  /* height: 200px; */
  border: 1px solid black;
  display: inline-flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
}

.category_item_container
{
  width: 120px;
  height: 120px;
  border: 1px solid blue;
  margin-bottom: 10px;
}

.title
{
  width: 100%;
  height: 40px;
  background: orange;
  font-size: 20px;
}
</style>
