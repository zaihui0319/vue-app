<template>
  <div class="home">
    <!-- 头部图片 -->
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
    <!-- 内容区域 -->
    <div>
      <!-- 分类 6个 -->
      <van-grid :column-num="3">
        <van-grid-item
          v-for="value in categories"
          :key="value.id"
          :icon="value.icon"
          :text="value.name"
        />
      </van-grid>
      <!-- 产品n个 -->
      <briup-product-item 
      v-for="p in products" 
      :key="p.id" 
      :data="p" 
      @click="toBuyHandler(p)">
      </briup-product-item>
    </div>
   
  </div>
</template>
<script>
// import {mapState, mapActions} from 'vuex'
//状态机被干掉
import {get,post} from '../../http/axios';
// import {get} from '../../http/axios';
export default {
  data(){
    return{
      categories:[],
      products:[]
    }
  },
  
  created(){
    //查询栏目信息
    this.loadCategories();
    //查询产品
    this.loadProducts();
  },
  methods:{
    toBuyHandler(p){
      // 跳转到订单确认页面并且携带数据p
      this.$router.push({
        path:"/manager/order_confirm",
        query:p
      })
    },
    //加载栏目信息
    loadCategories(){
      let url="/category/findAll"
     get(url).then((response)=>{
       this.categories=response.data.slice(0,6);
      })
    },
    loadProducts(){
      let url = "/product/query"
      let params = {
        page:0,
        pageSize:100
      }
      post(url,params).then((response)=>{
        this.products = response.data.list;
      })
      
    },

  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>