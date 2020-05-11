<template>
  <div class="home">
    <van-row>
    <van-col span="24">


    <van-tabs @click="onClick">
       <van-tab  v-for="index in categories.length" :title="categories[index-1].name" class="tab">
         <van-card v-for="(item,index) in phone"
                 :price="item.price"
                 :desc="item.desc"
                 :title="item.title"
                 :thumb="item.thumb"
         >
           <template #tags>
             <van-tag v-for="tag in item.tag" color="#f2826a" style="margin-left: 5px">{{tag.name}}</van-tag>
           </template>
           <template #footer>
             <van-button round type="info" size="mini" @click="buy(index)">购买</van-button>
           </template>
         </van-card>

      </van-tab>
    </van-tabs>
    </van-col>
    </van-row>
    <van-sku
            v-model="show"
            :sku="sku"
            :goods="goods"
            :hide-stock="sku.hide_stock"
            @buy-clicked="onBuyClicked">
      <template #sku-actions="props">
        <div class="van-sku-actions">
          <!-- 直接触发 sku 内部事件，通过内部事件执行 onBuyClicked 回调 -->
          <van-button
                  square
                  size="large"
                  type="danger"
                  @click="props.skuEventBus.$emit('sku:buy')"
          >
            买买买
          </van-button>
        </div>
      </template>

    </van-sku>


  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data: function () {
    return {
      categories: [
        {
          name: '魅焰红',
          type: 1
        },
        {
          name: '极光蓝',
          type: 2
        },
        {
          name: '铂光金',
          type: 3
        },
        {
          name: '幻夜黑',
          type: 1
        },
      ],
      phone: [
        {
          id: 1,
          title: "HUA40",
          price: "1881",
          desc: "魅焰红",
          thumb: "https://img.yzcdn.cn/vant/ipad.jpeg",
          tag: [
            {
              name: "720p珍珠屏",

            },
            {
              name: "Micro USE接口",
            },

          ]
        },

      ],
      show: false,
      sku: '',
      goods: '',

  }

  },
  methods:{

    onClick(index){

      switch(index){
        case 0:
          this.phone=[
            {
              id:1,
              title:"HUA40",
              price:"1881",
              desc:"魅焰红",
              thumb:"https://img.yzcdn.cn/vant/ipad.jpeg",
              tag:[
                {
                  name:"720p珍珠屏",

                },
                {
                  name:"Micro USE接口",
                },

              ]
            },
          ];break;
        case 1:
          this.phone=[
            {
              id:2,
              title:"Huawei p40",
              price:"1882",
              desc:"极光蓝",
              thumb:"https://img.yzcdn.cn/vant/ipad.jpeg",
              tag:[
                {
                  name:"720p珍珠屏",

                },
                {
                  name:"Micro USE接口",
                },

              ]
            },
          ];break;
        case 2:
          this.phone=[
            {
              id:3,
              title:"Huawei p40",
              price:"1883",
              desc:"铂光金",
              thumb:"https://img.yzcdn.cn/vant/ipad.jpeg",
              tag:[
                {
                  name:"720p珍珠屏",

                },
                {
                  name:"Micro USE接口",
                },

              ]
            },
          ];break;
        case 3:
          this.phone=[
            {
              id:4,
              title:"Huawei p40",
              price:"1884",
              desc:"幻夜黑",
              thumb:"https://img.yzcdn.cn/vant/ipad.jpeg",
              tag:[
                {
                  name:"720p珍珠屏",

                },
                {
                  name:"Micro USE接口",
                },

              ]
            },
          ];break;

      }
    },
    buy(index){
      this.show=true,
      this.goods={
        picture: 'https://img.yzcdn.cn/1.jpg'
      }
      this.sku={
          tree: [
            {
              k: '颜色', // skuKeyName：规格类目名称
              v: [
                {
                  id: 1, // skuValueId：规格值 id
                  name: '32GB', // skuValueName：规格值名称
                  imgUrl: 'https://img.yzcdn.cn/1.jpg', // 规格类目图片，只有第一个规格类目可以定义图片
                  previewImgUrl: 'https://img.yzcdn.cn/1p.jpg', // 用于预览显示的规格类目图片
                },
                {
                  id: 2,
                  name: '64GB',
                  imgUrl: 'https://img.yzcdn.cn/2.jpg',
                  previewImgUrl: 'https://img.yzcdn.cn/2p.jpg',
                }
              ],
              k_s: 's1' // skuKeyStr：sku 组合列表（下方 list）中当前类目对应的 key 值，value 值会是从属于当前类目的一个规格值 id
            }
          ],
          list: [
            {
              s1:1,
              price:28000,
              stock_num: 110 // 当前 sku 组合对应的库存
            },
            {
              s1:2,
              price:32000,
              stock_num: 110 // 当前 sku 组合对应的库存
            }
          ],
          price: '1.00', // 默认价格（单位元）
          stock_num: 227, // 商品总库存
          none_sku: false, // 是否无规格商品
          hide_stock: false // 是否隐藏剩余库存
        }


    },
    onBuyClicked(item){
      console.log(item)
      this.$store.state.specsId=item.selectedSkuComb.s1
      this.$store.state.quantity=item.selectedNum
      this.$router.push('/addressList')
    }


  }
}
</script>
