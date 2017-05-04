<template>
	<div class="home">
		<div id="home_main">
			<!--<div id="home_search">
				<form action="" method="post">
					<img src="components/home/img/logo.png" alt="" id="logo" />
					<a href="javascript:vido(0)" ui-sref='.search'>
						<input type="text" placeholder="卫衣" />
					</a>
					<img src="components/home/img/xx.png" alt="" />
				</form>
			</div>-->
		</div>
	</div>
</template>

<script>
	export default{
		name:'home',
		data(){
			return{
				arrAllData:[]
			}
		},
		mounted:function(){
			this.$http.get('static/json/topContent.json').then(function(res){
				this.arrAllData=res.body.data;
				console.log(this.arrAllData)
				
			})
		}
	}
</script>

<style>
.home{width: 100%;height: 100%;}
#home_main{width: 100%;position: absolute;top: 2.5rem;overflow:auto;}
#home_search{width: 100%;height: 1.9rem;}
#home_search>form{width: 100%;height: 100%;}
#home_search>form>img{margin-left:.6rem;width: .7rem;vertical-align: middle;}
#home_search #logo{width: 1.3rem;}
#home_search>form>a{width: 11.3rem;height: 1.2rem;margin:.35rem 0 0 .6rem;display:inline-block;}
#home_search>form>a>input{width: 100%;height: 100%; border: none;border-radius: 5px;outline: none;
	background:#f4f4f4 url("img/search.png")no-repeat .4rem center ;padding-left: 1.2rem;color: #a9a9a9;background-size: .5rem .5rem;}
</style>