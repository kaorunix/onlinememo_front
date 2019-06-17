<template>
<div>
  <div class="app" v-bind:key="memo.id" v-for="(memo,index) in memos">
    <div>{{memo.id}}{{index}}</div>
  </div>
  <div class="app2" v-bind:key="memo.id" v-for="(memo,index) in memos">
  <p>{{memo.id}}</p>
   <table >
   <tr class="piece">
<!--   v-bind:style="{ top: memoPositionY + 'px', left: memoPositionX + 'px'  }"> -->
<!--   <tr class="piece" v-bind:style="'{ top:' + {{memo.position.y}} + 'px;left:' + {{memo.position.x}} + 'px; }'"> -->
   <th>
     <div v-if="memo.edit">{{index}}{{memo.title}}</div>
     <div v-else>{{index}}<input type="text" v-model="memo.title" /></div>
   </th>
   <td>
     <div v-if="memo.edit">{{memo.body}}</div>
     <div v-else><input type="text" v-model="memo.body" /></div>
   </td>
   <td>
     <button v-if="memo.edit" @click="edit(index)">変更</button> 
     <button v-else @click="save(index)">保存</button> 
   </td>	     
   </tr>
   </table>

  </div>
</div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

export default {
  el: '#memo',
  name: 'memo',
  data () {
    return {
      msg: 'HelloWorld',
      memos: [
        {id: 1, title: 'タイトル1', body: '中身', edit: true, position: 1, memostyle:1},
	//{color: "#8AF0F0", position: absolute, left:0, top:0}},
        {id: 2, title: 'タイトル2', body: '中身中身', edit: true, position: 1,memostyle:1},
//	{ color: "#8AF0F0",position: absolute, left:10, top:10}},
        {id: 3, title: 'タイトル3', body: '中身中身中身', edit: true, position: 1,memostyle:1}
//	{color: "#8FF0F0", position: absolute, left:20, top:20}}
      ],
      active_title: false
    }
  },
  methods: {
    edit: function (i){
      var obj = {
        id:this.memos[i].id,
	title:this.memos[i].title,
	body:this.memos[i].body,
	edit: (! this.memos[i].edit),
	position: this.memos[i].position
      };
      this.$set(this.memos, i,obj)
    },
    save: function (i){
      var obj = {
        id:this.memos[i].id,
	title:this.memos[i].title,
	body:this.memos[i].body,
	edit: (! this.memos[i].edit)
      };
      this.$set(this.memos, i,obj)
    }

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
tr.piece {
  color: #8AF0F0;
  position:absolute;
  left: 100px;
  top: 100px;
}
</style>
