<template>
  <div class="countlist-wrap">
    <div class="s-title">
      <h2 :style="{backgroundImage:'url('+list.titleImg+')'}">{{list.title}}<span>{{list.subhead}}</span></h2>
      <a href="#/list">更多 ></a>
    </div>
    <div class="s-cont">
      <div class="s-cont-detail" v-for="item in list.itemlist" :style="{backgroundImage:'url('+item.img+')'}">
        <a href="#/detail" @click="goto(item.id)">
          <div class="s-text">
            <p>{{item.title}}</p>
            <p>{{item.subhead}}</p>
          </div>
        </a>
        <div class="s-detail-bottom">
          <p><span>￥{{item.priceNow}}</span><i>￥{{item.priceOld}}</i></p>
          <span class="iconfont icon-gouwuche" @click="addShoppingcar(item.id)"></span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'countlist',
        props:{
          list:Object
        },
        data () {
            return {}
        },
        methods:{
          goto:function (id) {
            sessionStorage.goodsId=id;
          },
          addShoppingcar:function (id) {
            var that=this;
            if(localStorage.userPhone){
              $.ajax({
                url:'api/addshoppingcar',
                type:'get',
                data:{
                  userPhone:localStorage.userPhone,
                  goodsId:id,
                },
                success:function (data) {
                  if(data.err==1){
                    that.$root.$emit("addshoppingcar",1);
                  }else if(data.err==2){
                      var num=data.goods.split("$").length;
                    that.$root.$emit("addshoppingcar",num);
                  }
                },
              });
            }else {
              this.$root.$emit("login",true);
            }
          }

        }

    }
</script>


<style scoped>
  .s-title{
    width: 100%;
    height: 100px;
    background: #ebffe8;
    border-bottom: 1px solid #498e3d;
  }
  .s-title>h2{
    font-weight: 500;
    margin-top: 30px;
    float: left;
    margin-left: 30px;
    height: 42px;
    line-height: 42px;
    font-size: 30px;
    color: #498e3d;
    padding-left: 65px;
    background: url("./img/index-friday.png") no-repeat left center;
  }
  .s-title>h2>span{
    margin-left: 10px;
    font-size: 18px;
    color: #afb4ae;
    font-weight: normal;
  }
  .s-title>a{
    float: right;
    margin-right: 30px;
    font-size: 18px;
    line-height: 18px;
    margin-top: 40px;
  }
  .s-cont{
    margin: 20px 0;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .s-cont-detail{
    width: 305px;
    height: 433px;
    overflow: hidden;
    position: relative;
    background: url("./img/index-friday1.png") no-repeat center top;
    /*background-color: #f2f2f2;*/
    background-size: 100% auto;
    box-sizing: border-box;
    border:1px solid rgb(237,237,237);
  }
  .s-cont-detail>a{
    display: block;
    width: 100%;
    height: 365px;
    position: relative;
  }
  .s-text{
    position: absolute;
    left:20px;
    bottom: 0;
  }
  .s-text>p:nth-child(1){
    font-size: 16px;
    line-height: 16px;
    color: #333;
  }
  .s-text>p:nth-child(2){
    font-size: 14px;
    line-height: 14px;
    color: #666;
    margin-top: 18px;
  }
  .s-detail-bottom{
    margin-top: 18px;
    overflow: hidden;
    line-height: 30px;
  }
  .s-detail-bottom>p{
    float: left;
    margin-left: 20px;
  }
  .s-detail-bottom>p>span{
    font-size: 20px;
    line-height: 20px;
    color: #ff5757;
    font-weight: bold;
    margin-right: 15px;
  }
  .s-detail-bottom>p>i{
    font-size: 16px;
    line-height: 16px;
    font-weight: 400;
    color: #666;
    text-decoration: line-through;
  }
  .s-detail-bottom>span{
    float: right;
    margin-right: 30px;
    color: #f08200;
    font-weight: bold;
    font-size: 27px;
    cursor: pointer;
  }
</style>
