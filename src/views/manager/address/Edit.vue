<template>
    <briup-fulllayout title="新增地址">
    <div>
    <van-cell-group>
    <van-field  v-model="form.telephone" placeholder="请输入手机号" />
    </van-cell-group>
    <van-cell-group>
    <van-field  v-model="form.province" placeholder="省" />
    </van-cell-group>
    <van-cell-group>
    <van-field  v-model="form.city" placeholder="市" />
    </van-cell-group>
    <van-cell-group>
     <van-field  v-model="form.area" placeholder="区" />
    </van-cell-group>
     <van-cell-group>
    <van-field  v-model="form.address" placeholder="详情信息" />
    </van-cell-group>
    <van-button block type="primary" @click="submitHandler">保存
    </van-button>
    </div>
    </briup-fulllayout>
</template>
<script>
import {post} from "../../../http/axios"
import {mapState} from "vuex";
export default {
    computed:{//计算属性
        ...mapState("user",["info"])
    },
    data(){
        return{
            form:{}
        }
    },
    methods:{
        submitHandler(){
            let url = "/address/saveOrUpdate"
            this.form.customerId=this.info.id;
            post(url,this.form).then((response)=>{
                //返回上一级页面
                this.$router.go(-1);
                //显示成功信息
                  this.$toast.success(response.message);
            })
        }
    }
}
</script>