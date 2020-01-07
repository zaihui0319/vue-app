<template>
    <briup-fulllayout title="常用地址">
    <van-list>
    <van-cell
        v-for="item in addresses"
        :key="item.id"
        :title="item.province+' '+item.city+' '+item.area+' '+item.address+' '+item.telephone"
    />
    </van-list>
    <br>
    <van-button
    block type="default"
     @click="toAddressEditHandler">
    新增地址
    </van-button>
    </briup-fulllayout>
</template>
<script>
import {get} from "../../../http/axios"//获取信息
import {mapState} from "vuex"
export default {
    data(){
        return{
            addresses:[]
        }
    },
    computed:{//计算属性
        ...mapState("user",["info"])
    },
    methods:{
        loadaddresses(){
            let id = this.info.id;//随机用户
            let url ="http://localhost:6677/address/findByCustomerId?id="+id;
            get(url).then((response)=>{
                this.addresses = response.data;
            })
        },
        toAddressEditHandler(){
            this.$router.push("/manager/address_edit")
        }

    },
    created(){
        //调用加载信息的方法
        this.loadaddresses();

    }
}
</script>


<style scoped>


</style>

