<template>
  <div class="order">
    <van-nav-bar title="我的订单" />
    <van-tabs v-model="active" color="#1659a0"  @click="tabClickHandler">
      <van-tab title="全部"></van-tab>
      <van-tab title="待派单"></van-tab>
      <van-tab title="待接单"></van-tab> 
      <van-tab title="待服务"></van-tab>
      <van-tab title="待确认"></van-tab>
      <van-tab title="已完成"></van-tab>
    </van-tabs>
    <!-- 订单 -->
    <div>
      <briup-order-item v-for="o in orders" :key="o.id" :data="o"></briup-order-item>
    </div>
  </div>
</template>
<script>
import {mapState} from 'vuex'
import {get} from '../../http/axios'
export default {
  data(){
    return {
      status:null,
      active:'',
      orders:[],
    }
  },
  computed:{
      //计算属性
      //将状态机汇总的user对象中的info对象获取到
      //user代表命名空间
      ...mapState("user",["info"])
  },
  created(){
      //调用加载地址信息的方法
      this.loadOrders();
  },
  methods:{
    //加载我的订单
    loadOrders(){
      let url = "/order/query";
            //在提交前，将当前登录者的id作为顾客id
            // this.form.customerId = this.info.id;
      let params = {
        customerId:this.info.id,
        status:this.status
      }
            get(url,params).then((Response)=>{
                this.orders = Response.data;
            })

    },
    // 点击tab的时候执行的回调函数
    tabClickHandler(name,title){
      // this.$toast(name+":"+title)
      this.status = title === "全部" ? null :title;
      this.loadOrders();
    },
  }
}
</script>
<style scoped>
.order {
  background: #f1f1f1;
}
</style>