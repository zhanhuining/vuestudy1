<template>
  <div class="box">
   <h2>购物车列表</h2>
   

   <div class="cen">
    <tr>
        <!--  -->
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
     <tr v-for="(v,k) in goodlist" :key="k" >
        <td><input type="checkbox" name="" id="" v-model="v.bool" @click="fn(k)"></td>
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
        <td><button>删除</button></td>
     </tr>
      <!-- <tr>
        <td>总计:</td>
      </tr> -->
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
              {goodname:"裤子",good_img:require("../img/1.png"),price:150, inventory:4,good_num:1,bool:false},
              {goodname:"裙子",good_img:require("../img/2.png"),price:250,inventory:100,good_num:1,bool:false},
              {goodname:"体恤衫",good_img:require("../img/3.png"),price:100,inventory:500,good_num:1,bool:false},
              {goodname:"眼镜",good_img:require("../img/4.png"),price:500,inventory:2,good_num:1,bool:false}
            ]
     }
  },
  methods:{
       jia(k){
        console.log(this.goodlist[k].good_num);
        if(this.goodlist[k].good_num<this.goodlist[k].inventory){
          this.goodlist[k].good_num+=1;
          }
       else{
         alert("没有库存")
       }
     },
     jian(k){
        if(this.goodlist[k].good_num>1){
            this.goodlist[k].good_num-=1;
        }
        else{
            alert("购买的商品不能少于1件")
        }
     },
     fn(v){
           console.log(this.goodlist[v].bool);
     },
     checkAll(){
        for(let i=0;i<this.goodlist.length;i++)
          this.goodlist[i].bool=true
     },
     checkNot(){
        for(let i=0;i<this.goodlist.length;i++)
            this.goodlist[i].bool=false
     },
     inverSelection(){
        for(let i=0;i<this.goodlist.length;i++)
            this.goodlist[i].bool= !this.goodlist[i].bool;
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