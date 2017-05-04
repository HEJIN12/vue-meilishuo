<template>
	<div class="home">
		<div id="home_main">
			<div id="home_search">
				<form action="" method="post">
					<img src="../img/logo.png" alt="" id="logo" />
					<a href="javascript:vido(0)">
						<input type="text" placeholder="卫衣" />
					</a>
					<img src="../img/xx.png" alt="" />
				</form>
			</div>
			<swiper :options="swiperOption" ref="mySwiper" class="swiper">
				<!-- slides -->
				<swiper-slide v-for="item in arrAllData">
					<img :src='item.image' alt="">
				</swiper-slide>
				<!-- Optional controls -->
				<div class="swiper-pagination" slot="pagination"></div>
				<!-- <div class="swiper-button-prev" slot="button-prev"></div>
            <div class="swiper-button-next" slot="button-next"></div>
            <div class="swiper-scrollbar"   slot="scrollbar"></div> -->
			</swiper>
			<div id="home_menu">
				<div id="home_menu1">
					<ul>
						<li v-for="(item,i) in home_menu">
							<a href=""><img :src="item.image" />
								<p>{{item.title}}</p>
							</a>
						</li>
					</ul>
				</div>
			</div>
			<div class="home_menu_next" v-for="item in home_menu_next">
				<a :href="item.originUrl">
					<img :src="item.image" />
					<h3>{{item.title}}</h3>
					<p>{{item.butDesc}}</p>
				</a>
				<div class="home_menu_next_2">
					<a :href="items.h5GoodUrl" v-for="items in item.goodsList">
						<img :src="items.image" />
						<h3>{{items.title}}</h3>
						<p>￥{{items.price}}</p>
					</a>
				</div>
			</div>
			<div id="home_more">查看更多</div>
			<div id="home_tab">
				<div @click="isClick(moren,0)"><span :class="{'changs':ischang==0}">流行</span></div>
				<div @click="isClick(zuixin,1)"><span :class="{'changs':ischang==1}">新款</span></div>
				<div @click="isClick(jingxuan,2)"><span :class="{'changs':ischang==2}">精选</span></div>
			</div>
			<div id="home_tab_main">
				<ul>
					<li v-for="item in home_tab_main">
						<a href="">
							<div class="tab_main_img">
								<div class="leftTop" v-if="item.lefttop_taglist[0]"><img :src="item.lefttop_taglist[0].img" /></div>
								<div class="leftBottom" v-if="item.leftbottom_taglist[0]"><img :src="item.leftbottom_taglist[0]" /></div>
								<img :src="item.show.img" />
							</div>
							<h3>{{item.title}}</h3>
							<p><span class="home_price">{{item.price}}</span><span class="home_cfav"><img src="../img/wjx.jpg"/>{{item.cfav}}</span></p>
						</a>
					</li>
				</ul>
			</div>
		</div>
		<a href="" id="mbj" onclick="document.getElementById('innerBox').scrollIntoView()"></a>
	</div>
</template>

<script>export default {
	name: 'home',
	data() {
		return {
			arrAllData: [],
			home_menu: [],
			home_menu_next:[],
			moren:[],
			jingxuan:[],
			zuixin:[],
			home_tab_main:[],
			ischang:0,
			swiperOption: {
				// NotNextTick is a component's own property, and if notNextTick is set to true, the component will not instantiate the swiper through NextTick, which means you can get the swiper object the first time (if you need to use the get swiper object to do what Things, then this property must be true)
				// notNextTick是一个组件自有属性，如果notNextTick设置为true，组件则不会通过NextTick来实例化swiper，也就意味着你可以在第一时间获取到swiper对象，假如你需要刚加载遍使用获取swiper对象来做什么事，那么这个属性一定要是true
				notNextTick: true,
				// swiper configs 所有的配置同swiper官方api配置
				autoplay: 300,
				//   direction : 'vertical',
				grabCursor: true,
				setWrapperSize: true,
				autoHeight: true,
				loop: true,
				pagination: '.swiper-pagination',
				paginationClickable: true,
				//   prevButton:'.swiper-button-prev',
				//   nextButton:'.swiper-button-next',
				//   scrollbar:'.swiper-scrollbar',
				mousewheelControl: true,
				observeParents: true,
				// if you need use plugins in the swiper, you can config in here like this
				// 如果自行设计了插件，那么插件的一些配置相关参数，也应该出现在这个对象中，如下debugger
				debugger: true,
				// swiper callbacks
				// swiper的各种回调函数也可以出现在这个对象中，和swiper官方一样
				onTransitionStart(swiper) {
					// console.log(swiper)
				},
				// more Swiper configs and callbacks...
				// ...
			}
		}
	},
	// you can find current swiper instance object like this, while the notNextTick property value must be true
	// 如果你需要得到当前的swiper对象来做一些事情，你可以像下面这样定义一个方法属性来获取当前的swiper对象，同时notNextTick必须为true
	computed: {
		swiper() {
			return this.$refs.mySwiper.swiper
		}
	},
	mounted: function() {
		this.$http.get('static/json/topContent.json').then(function(res) {
			this.arrAllData = res.body.data[20114].list;
			this.home_menu = res.body.data[13730].list;

		})
		this.$http.get('static/json/niuzaiku.json').then(function(res) {
			this.home_menu_next = res.body.data;

		})
		this.$http.get('static/json/moren.json').then(function(res) {
			this.moren = res.body.data.list;
			this.home_tab_main=this.moren;
			console.log(this.moren)

		})
		this.$http.get('static/json/jingxuan.json').then(function(res) {
			this.jingxuan= res.body.data.list;
			console.log(this.jingxuan)

		})
		this.$http.get('static/json/zuixin.json').then(function(res) {
			this.zuixin = res.body.data.list;
			console.log(this.zuixin)

		})
		
	},
	methods: {
    	isClick: function (datas, i) {
      		this.ischang = i;
			this.home_tab_main = datas;
    	}
  	}

}
</script>
<style>
.home{width: 100%;height:90%;position: absolute;top: 0;font-size: .6rem;}
#home_main{width: 100%;position: absolute;top:0;overflow:auto;height: 100%;}
#home_search{width: 100%;height: 1.9rem;}
#home_search>form{width: 100%;height: 100%;}
#home_search>form>img{margin-left:.6rem;width: .7rem;vertical-align: middle;}
#home_search #logo{width: 1.3rem;}
#home_search>form>a{width: 11.3rem;height: 1.2rem;margin:.35rem 0 0 .6rem;display:inline-block;}
#home_search>form>a>input{width: 100%;height: 100%; border: none;border-radius: 5px;outline: none;
	background:#f4f4f4 url("../img/search.png")no-repeat .4rem center ;padding-left: 1.2rem;color: #a9a9a9;background-size: .5rem .5rem;}
.swiper{width: 100%;}
.swiper img{width: 100%;}
#home_menu{background: #eeeeee;padding-bottom: .4rem;}
#home_menu1{padding: .4rem;background: white;overflow: auto;}
#home_menu1>ul{overflow: hidden; overflow-x:scroll;white-space: nowrap;}
#home_menu1>ul>li{margin-right: .4rem;display: inline-block;}
#home_menu1>ul>li>a{display: block;}
#home_menu1>ul>li>a>img{height:3.2rem;}
#home_menu1>ul>li>a>p{font-size: .6rem;width: 100%;text-align: center;}
#home_menu1>ul::-webkit-scrollbar{display: none;}
.home_menu_next{width: 100%;background: #eeeeee;}
.home_menu_next>a{display: block;width: 100%;position: relative;}
.home_menu_next>a>img{width: 100%;}
.home_menu_next>a>h3{color: white;font-size: .9rem; position: absolute;top: 6.7rem;width: 100%;text-align: center;}
.home_menu_next>a>p{color: white;font-size: .6rem; position: absolute;top: 7.9rem;width: 100%;text-align: center;background: url('../img/right.png')no-repeat 9.2rem center;}
.home_menu_next_2{padding: .45rem 0 0 .45rem;border-bottom: .45rem solid #eeeeee; background: white;overflow: hidden; overflow-x:scroll;white-space: nowrap;font-size: 0;}
.home_menu_next_2>a{width: 4.3rem;margin-right: .4rem;display: inline-block;}
.home_menu_next_2>a>img{width: 100%;}
.home_menu_next_2>a>h3{font-size: .6rem;color: #3f2a20;overflow: hidden;white-space: nowrap;text-overflow: ellipsis}
.home_menu_next_2>a>p{color: #f14a6b;font-size: .6rem;margin-bottom: .2rem;}
.home_menu_next_2::-webkit-scrollbar{display: none;}
#home_main>div:nth-child(6) .home_menu_next_2{border-bottom: 1px solid #eeeeee;}
#home_more{height: 2rem;line-height: 1.9rem;color: #ff3366;text-align: center;font-size: .7rem;
background: url("../img/right2.png")no-repeat 9.4rem center;border-bottom: .1rem solid #eeeeee;}
#home_tab{height: 1.7rem;z-index: 100;background: white;width: 100%;}
.dw{position: fixed;top: 2.4rem;}
#home_tab>div{height: 100%;width: 33.33%;line-height: 1.7rem;text-align: center;float: left;}
#home_tab>div>span{padding: .1rem .1rem .2rem .1rem;color: #666666;font-size: .7rem;}
#home_tab>div .changs{border-bottom: 2px solid #ff3366;color: #ff3366;}
#home_tab_main>ul>li{width: 50%;float: left;background: white;}
#home_tab_main>ul>li>a{width: 96%;margin:0 auto .7rem;display: block;}
.tab_main_img{width: 100%;position:relative;height: 10rem;}
.tab_main_img>img{width: 100%;height: 10rem;}
.leftTop{position: absolute;top: 0;}
.leftTop>img{width:1.9rem ;margin-left: .2rem;}
.leftBottom{position: absolute;bottom: -0.1rem;}
.leftBottom>img{width:1.5rem ;margin-left: .2rem;}
#home_tab_main>ul>li>a>h3{width: 100%;margin-top: .2rem;font-size: .6rem;overflow: hidden;white-space: nowrap;
	text-overflow: ellipsis;color: #666666;font-weight: normal;}
#home_tab_main>ul>li>a>p{width: 100%;text-align: center;}
.home_price{color:#ff3395 ;margin-right: .5rem;}
.home_cfav{color: #9999a5;}
.home_cfav>img{margin-right: .2rem;}
#mbj{position: fixed;right: 10px;bottom: 70px; width: 1.8rem;height: 1.8rem;background:url("../img/mbj.png")no-repeat; z-index: 2;background-size: 100% 100%;display: none;}
</style>