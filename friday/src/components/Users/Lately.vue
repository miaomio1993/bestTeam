<template>
	<div>
		<div class="z-lately">
			<h2>最近浏览</h2>
			<ul>
				<li v-for="(item,index) in items" class="z-all">
					<img v-bind:src="item.imgs" alt="" />
					<p>{{item.p1}}</p>
					<p>{{item.p2}}</p>
					<p><span>{{item.newcost}}</span><i>{{item.oldcost}}</i><em class="iconfont icon-gouwuche"></em></p>
					<div class="remove" @click="move(index)">x</div>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
  export default{
      data(){
        return{
            items:[
              {
                  imgs:require("./img/lately1.png"),
                  p1:"新西兰佳沛黄金奇异果",
                  p2:"果肉绵密，花蜜般的甘甜百吃不厌",
                  newcost:"¥28.8",
                  oldcost:"¥41.00"

              },
              {
                imgs:require("./img/lately1.png"),
                p1:"新西兰佳沛黄金奇异果",
                p2:"果肉绵密，花蜜般的甘甜百吃不厌",
                newcost:"¥28.8",
                oldcost:"¥42.00"

              },
              {
                imgs:require("./img/lately1.png"),
                p1:"新西兰佳沛黄金奇异果",
                p2:"果肉绵密，花蜜般的甘甜百吃不厌",
                newcost:"¥28.8",
                oldcost:"¥43.00"

              },
              {
                imgs:require("./img/lately1.png"),
                p1:"新西兰佳沛黄金奇异果",
                p2:"果肉绵密，花蜜般的甘甜百吃不厌",
                newcost:"¥28.8",
                oldcost:"¥44.00"

              },
              {
                imgs:require("./img/lately1.png"),
                p1:"新西兰佳沛黄金奇异果",
                p2:"果肉绵密，花蜜般的甘甜百吃不厌",
                newcost:"¥28.8",
                oldcost:"¥45.00"

              },
              {
                imgs:require("./img/lately1.png"),
                p1:"新西兰佳沛黄金奇异果",
                p2:"果肉绵密，花蜜般的甘甜百吃不厌",
                newcost:"¥28.8",
                oldcost:"¥46.00"

              },
            ]
        }
      },
      methods:{
         move:function (index) {
          this.items.splice(index,1)
         }
      }
  }
</script>

<style scoped>
.z-lately{
width: 1077px;
border: 1px solid #e3e3e3;
}
.z-lately>h2{
  line-height: 60px;
  font-size: 20px;
  border-bottom: 1px solid #e3e3e3;
  text-align: left;
  padding-left: 20px;
  font-weight: 400;
}
.z-lately>ul{
	width: 1034px;
	padding: 15px 20px 20px 20px;
	display: flex;
	justify-content: space-around;
	flex-wrap: wrap;
}
.z-lately>ul>li{
	width: 303px;
	height: 433px;
	border: 1px solid #F2F7F7;
	border-radius: 3px;
	margin-bottom: 20px;
	text-align: center;
	position: relative;
}
.z-lately>ul>li>p{
	text-align: left;
	padding-left: 20px;
	line-height: 50px;
}
.z-lately>ul>li>p:nth-child(3){
	color: gray;
	font-size: 14px;
}
.z-lately>ul>li>p>span{
	color: red;
	padding-right: 15px;
}
.z-lately>ul>li>p>i{
	color: gray;
	font-size: 14px;
	text-decoration: line-through;
}
.z-lately>ul>li>p>em{
	color: #F78327;
	margin-left: 130px;
	font-size: 20px;
}
.z-lately>ul>li>div{
	color: white;
	height: 15px;
	width: 15px;
	border-radius: 50%;
	background: #498E3D;
	position: absolute;
	top: 5px;
	right: 5px;
	line-height: 15px;

}

</style>
