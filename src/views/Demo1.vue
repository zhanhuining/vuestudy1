<template>
  <div class="box">
   <h2>购物车列表</h2>
   

   <div class="cen">
    <tr>
        <!--  标题-->
        <th>   <!-- 选择按钮 -->
            <button @click="checkAll()">全选</button>
            <button @click="checkNot()">全不选</button>
            <button  @click="inverSelection()">反选</button>
        </th>
        <th>商品</th>
        <th>商品图片展示</th>
        <th>单价</th>
        <th>数量</th>
        <th>购买数量</th>
        <th>小计</th>
        <th>操作</th>
     </tr>
     <!-- 数字后面可以添加小数点 .toFixed(3)-->
       <!-- 数据遍历 -->
     <tr v-for="(v,k) in goodlist" :key="k" v-show="v.booll">
        <td ><input type="checkbox" name="" id="" v-model="v.bool" @click="fn(k)"></td>
        <td>{{v.goodname}}</td>
        <td class="good_img">
            <img :src="v.good_img" alt="">
            <!-- <img src="../img/1.png" alt=""> -->
        </td>
        <td>{{v.price}}</td>
        <td>{{v.inventory}}</td>
        <td>
            <button @click="jia(k)">+</button>
            {{v.good_num}}
            <button @click="jian(k)">-</button>
        </td>
        <td>{{v.good_num*v.price}}</td>
        <td><button @click="del(k)">删除</button></td>
     </tr>
     <!-- 价格总计 -->
      <tr>
        <td>总计:{{aggregate}}</td>
      </tr>
   </div>
     

  </div>
</template>

<script>
export default {
  data(){
     return{
        /*
          <th>商品</th>
          <th>单价</th>
          <th>数量  (库存数量inventory)</th>
          <th>购买数量</th>
          <th>小计 subtotal </th>  用单价*购买数量
          <th>操作</th>
        */ 
        goodlist:[
              {goodname:"裤子",good_img:require("../img/1.png"),price:150, inventory:4,good_num:1,bool:false,booll:true},
              {goodname:"裙子",good_img:require("../img/2.png"),price:250,inventory:100,good_num:1,bool:false,booll:true},
              {goodname:"体恤衫",good_img:require("../img/3.png"),price:100,inventory:500,good_num:1,bool:false,booll:true},
              {goodname:"眼镜",good_img:require("../img/4.png"),price:500,inventory:2,good_num:1,bool:false,booll:true}
            ]
     }
  },
  methods:{
    // 数量加
       jia(k){
        if(this.goodlist[k].good_num<this.goodlist[k].inventory){
          this.goodlist[k].good_num+=1;
          }
       else{
         alert("没有库存")
       }
     },
    //  数量减
     jian(k){
        if(this.goodlist[k].good_num>1){
            this.goodlist[k].good_num-=1;
        }
        else{
            alert("购买的商品不能少于1件")
        }
     },

    //  fn(v){
    //        console.log(this.goodlist[v].bool);
    //  },
    // 全选
     checkAll(){
        for(let i=0;i<this.goodlist.length;i++)
          this.goodlist[i].bool=true
     },
    // 全不选
     checkNot(){
        for(let i=0;i<this.goodlist.length;i++)
            this.goodlist[i].bool=false
     },
    //  反选
     inverSelection(){
        for(let i=0;i<this.goodlist.length;i++)
            this.goodlist[i].bool= !this.goodlist[i].bool;
     },
    //  删除整条信息
     del(v){
           console.log(v); 
           this.goodlist[v].booll=!this.goodlist[v].booll;

     }
  },
  computed:{
    // 计算 只需要调用一次
    // 商品所有价格
    aggregate(){
        let hold=0;
         for(let i=0;i<this.goodlist.length;i++){
                 if( this.goodlist[i].bool===true){
                          hold+=this.goodlist[i].good_num*this.goodlist[i].price
                        //   console.log(hold);
                 }
         }
          return hold;
    }
   
  }
}
</script>

<style>
tr th,tr td{
    border:1px solid #000;
}
.cen{
    background: pink;
    width: 800px;
    height: 500px;
    margin: 40px auto;
}
img{
    width: 30px;
    height: 30px;
}
</style>