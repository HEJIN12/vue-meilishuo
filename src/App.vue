<template>
  <div id="app">
    <router-view></router-view>
    <ul id="tab">
    	<li>
    		<router-link to="home">首页</router-link>
    	</li>
    	<li>
    		<router-link to="category">分类</router-link>
    	</li>
    	<li>
    		<router-link to="shopcar">购物车</router-link>
    	</li>
    	<li>
    		<router-link to="mine">我的</router-link>
    	</li>
    </ul>
  </div>
</template>

<script>
import Hello from './components/Hello'

export default {
  name: 'app',
  components: {
    Hello
  }
}
</script>

<style>
html,body{width: 100%;height: 100%;}
*{margin: 0;padding: 0;}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul{list-style: none}
#tab{position: fixed;bottom: 0;width: 100%;height: 10%;background: lightpink}
#tab>li{float: left;width: 25%;}
</style>
