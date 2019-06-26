<template>
<div>
  <div class="app" v-bind:key="memo.id" v-for="(memo,index) in memos">
  <p>{{memo.id}}</p>
   <div class="piece2" v-bind:style="{ color: memo.memostyle.color, position: memo.memostyle.position, top: memo.memostyle.top + 'px', left: memo.memostyle.left + 'px'}">
<!--   v-bind:style="{ top: memoPositionY + 'px', left: memoPositionX + 'px'  }"> -->
<!--   <tr class="piece" v-bind:style="'{ top:' + {{memo.position.y}} + 'px;left:' + {{memo.position.x}} + 'px; }'"> -->
   <div class="th">
     <div v-if="memo.edit">{{index}}{{memo.title}}</div>
     <div v-else>{{index}}<input type="text" v-model="memo.title" /></div>
   </div>
   <div class ="td">
     <div v-if="memo.edit">{{memo.body}}</div>
     <div v-else><input type="text" v-model="memo.body" /></div>
   </div>
   <div>
     <button v-if="memo.edit" @click="edit(index)">変更</button> 
     <button v-else @click="save(index)">保存</button> 
   </div>
   <div>
   <input type="text" v-mode="memo.memostyle.color" name="hideAfterPaletteSelect" v-bind:id="'hideAfterPaletteSelect' + index" value="" style="display: none;">
   <button @click="changeColor(index,memo)">色の変更</button>
   </div>
   </div>


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
        {id: 1, title: 'タイトル1', body: '中身', edit: true, position: 1, memostyle: {color: '#8AF0F0', position: 'absolute', left:0, top:0}},
        {id: 2, title: 'タイトル2', body: '中身中身', edit: true, position: 1,memostyle: { color: '#8AF0F0',position: 'absolute', left:200, top:250}},
        {id: 3, title: 'タイトル3', body: '中身中身中身', edit: true, position: 1,memostyle: {color: '#8FF0F0', position: 'absolute', left:400, top:30}}
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
	position: this.memos[i].position,
	memostyle: this.memos[i].memostyle
      };
      this.$set(this.memos, i,obj)
    },
    save: function (i){
      var obj = {
        id:this.memos[i].id,
	title:this.memos[i].title,
	body:this.memos[i].body,
	edit: (! this.memos[i].edit),
	position: this.memos[i].position,
	memostyle: this.memos[i].memostyle
      };
      this.$set(this.memos, i,obj)
    },
    changeColor: function(i,obj) {
        var c = obj.memostyle.color;
	var parent = this.memos
	var base = this
        console.log(c);
	console.log("#hideAfterPaletteSelect"+i)
        $("#hideAfterPaletteSelect"+i).spectrum({
	    color: c,//'blanchedalmond',
	    showPaletteOnly: true,
	    showPalette:true,
	    hideAfterPaletteSelect:true,
	    chooseText: "OK", // 選択ボタンのテキスト
	    showButtons: true, // ボタンを表示する
	    showSelectionPalette: false, // ユーザーが前に選択した色をパレットに表示する
	    clickoutFiresChange: true, // ピッカーの外側をクリックしてピッカーを閉じた際にchangeイベントを発生させる
	    palette: [
	            ['black', 'white', 'blanchedalmond',
		     'rgb(255, 128, 0);', 'hsv 100 70 50'],
		     ['red', 'yellow', 'green', 'blue', 'violet']
    	    ],
	    change: function(c){
	    console.log("change");
	      var mstyle = {
	        color: c,
		position: obj.position,
		left: obj.left,
		top: obj.top
	      };
              var retobj = {
                id:obj.id,
                title:obj.title,
                body:obj.body,
                edit: (obj.edit),
                position: obj.position,
                memostyle: mstyle
              };
	    console.log(obj);
            base.$set(parent, i,obj)
	      hide();
	    return
	    },
	    move: function(c){
	    console.log("move" + obj);
	      var mstyle = {
	        color: c,
		position: obj.position,
		left: obj.left,
		top: obj.top
	      };
	    console.log("mstyle");
              var retobj = {
                id:obj.id,
                title:obj.title,
                body:obj.body,
                edit: (obj.edit),
                position: obj.position,
                memostyle: mstyle
              };
	    console.log("obj");
	    console.log(retobj);
            base.$set(parent, i,retobj);
	    console.log("move end")
	    return;
	    },
	    hide: function(c){
	    console.log("hide")
	      var mstyle = {
	        color: c,
		position: this.memos[i].position,
		left: this.memos[i].left,
		top: this.memos[i].top
	      }
              var obj = {
                id:this.memos[i].id,
                title:this.memos[i].title,
                body:this.memos[i].body,
                edit: (this.memos[i].edit),
                position: this.memos[i].position,
                memostyle: mstyle
              }
	    console.log(obj)
            this.$set(this.memos, i,retobj)
	    return
	    }
          }
    	)
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
