<template>
    <van-address-edit
            :area-list="areaList"
            show-delete
            @save="onSave"
            @delete="onDelete"
    />
</template>



<script>
    import { Toast } from 'vant';
    import AreaList from '../api/area'
    export default {
        name:"AddressNew",
        data() {
            return {
                areaList:AreaList

            };
        },
        methods: {
            onSave(item) {
               // console.log(item)
               let instance=Toast("修改成功");
               setTimeout(()=>{
                   instance.close();
                   this.$router.push('/addressList')
               },1000)
            },
            onDelete() {
                history.go(-1)
            },

        },
    };</script>