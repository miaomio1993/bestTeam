<template>
  <div class="headercenter">
		<a href="#/" class="s-logo">
			<img src="./img/logo.png"/>
		</a>

    <div class="s-search">
      <div class="s-search-input">
        <input type="text" id="search" placeholder="请输入关键字进行搜索">
        <a href="javascript:void(0)" @click="search" class="iconfont icon-fangdajing"></a>
      </div>
      <div class="s-search-hot">
        <span>热门：</span>
        <a href="javascript:void(0)">奇异果</a>
        <a href="javascript:void(0)">牛排</a>
        <a href="javascript:void(0)">山竹</a>
        <a href="javascript:void(0)">牛油果</a>
      </div>
    </div>

    <div class="s-right">
      <a class="s-personal" href="javascript:void(0)" @click="gotouser">
        <span class="iconfont icon-geren-80-copy"></span>
        <b>个人中心</b>
      </a>
      <a class="s-shopping-car" href="javascript:void(0)" @click="gotocar">
        <span class="iconfont icon-gouwuche"></span>
        <b>购物车</b>
        <em v-if="showShoppingcar">{{shoppingNum}}</em>
      </a>
    </div>
    <login v-if="isLog"></login>
  </div>
</template>

<script>
    import Login from "@/components/Search/Login";
    export default {
        name: 'headercenter',
        data () {
            return {
              shoppingNum:0,
              isLog:false,
              showShoppingcar:false,
            }
        },
        components:{
            Login,
        },
        methods:{
          getLogin:function (data) {
            this.isLog=true;
          },
          shoppingcar:function (data) {
            this.shoppingNum=data;
            this.showShoppingcar=true;
//            console.log(this.shoppingNum)
          },
          gotocar:function () {
            if(localStorage.userPhone){
              this.$router.push({path:'/shoppingcar'})
            }else {
              this.$root.$emit("login",true);
            }
          },
          gotouser:function () {
            if(localStorage.userPhone){
              this.$router.push({path:'/users'})
            }else {
              this.$root.$emit("login",true);
            }
          },
          search:function () {
            var that=this;
            $.ajax({
              url:'api/search',
              type:'get',
              data:{
                search:$("#search").val(),
              },
              success:function (data) {
                if(data.err==1){
                  if(data.list.length>0){
                    sessionStorage.search=$("#search").val();
                    that.$router.push({path:'/search'});
                    location.reload();
                  }else {
                    that.$router.push({path:'/searchunfind'});
                  }
                }
              }
            })

          }
        },
        created:function () {
          this.$root.$on("login",this.getLogin);
          this.$root.$on("addshoppingcar",this.shoppingcar);
          if(localStorage.userPhone){
              var that=this;
              $.ajax({
                url:'/api/shoppingcar',
                type:'get',
                data:{
                  act:'num',
                  userPhone:localStorage.userPhone,
                },
                success:function (data) {
                  that.shoppingNum=data.goods.split("$").length;
                  if(that.shoppingNum>0){
                      that.showShoppingcar=true;
                  }
                }
              })
          }
        }
    }
</script>


<style scoped>
  .headercenter{
    width: 1280px;
    /*margin: 0 auto;*/
    overflow: hidden;
    height: 130px;
  }
  .s-logo{
    display: block;
    float: left;
    margin-top: 25px;
    margin-bottom: 38px;
  }
  .s-logo>img{
    width: 370px;
    height: 67px;
  }
  .s-search{
    float: left;
    margin-left: 100px;
    margin-top: 50px;
    width: 500px;
  }
  .s-search-input{
    height: 40px;
    background: #4b943d;
    margin-bottom: 3px;
  }
  .s-search-input>input{
    height: 16px;
    width: 440px;
    margin-top: 2px;
    margin-left: 2px;
    background: #fff;
    padding: 10px;
    font-size: 14px;
    vertical-align: top;
  }
  .s-search-input>a{
    line-height: 40px;
    font-size: 24px;
    color: #fff;
    margin-left: 2px;
    font-weight: bolder;
  }
  .s-search-hot{
    font-size: 14px;
    color: #666;
  }
  .s-search-hot>a{
    margin-left: 5px;
    margin-right: 5px;
  }
  .s-right{
    margin-top: 50px;
    float: right;
    width: 290px;
  }
  .s-right>a{
    float: left;
    margin-left: 20px;
    display: block;
    width: 123px;
    height: 38px;
    background: #f8f8f8;
    border:1px solid #e5e5e5;
    text-align: center;
    font-size: 14px;
    color: #666;
    line-height: 38px;
    position: relative;
  }
  .s-right>a>b{
    font-weight: normal;
    vertical-align: top;
  }
  .s-right>a>span{
    font-size: 20px;
    vertical-align: top;
    margin-right: 5px;
  }
  .s-shopping-car>em{
    position: absolute;
    top: -15px;
    left: 40px;
    display: block;
    width: 24px;
    height: 24px;
    line-height: 24px;
    color: #fff;
    background: url("img/header-shopping-num.png") no-repeat center center;
    background-size:23px 23px;
  }

</style>
