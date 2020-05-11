<template>
    <van-address-edit
            :area-list="areaList"
            show-delete
            :address-info="addressInfo"
            save-button-text="修改"
            @save="onSave"
            @delete="onDelete"
    />
</template>



<script>
    import { Toast } from 'vant';
    import AreaList from '../api/area'
    export default {
        name:"AddressEdit",
        created() {
           let data=JSON.parse(this.$route.query.item)

           this.addressInfo=data
           let index=data.address.indexOf('区')
            if(index<0) index=data.address.indexOf('县')

            this.addressInfo.addressDetail=data.address.substring(index+1)

            console.log(this.addressInfo)
        },
        data() {
            return {
                areaList:AreaList,
                addressInfo:null,

            };
        },
        methods: {
            onSave(item) {
                // console.log(item)
                let instance=Toast("添加成功");
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