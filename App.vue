<template>
  <div class="container-fluid">
	<nav class="navbar navbar-dark bg-dark">
		<span class="navbar-brand mb-0 h1">Cats and food list</span>
	</nav>
	<div class="list">
	<h1>koty i ich karma</h1>
		<div v-if="alert==true" class="alert alert-danger" role="alert"><h2>Wypełnij wszystkie pola!</h2></div>
	</div>
	<cat-table v-bind:cats="cats" v-on:cdelete="deletec($event)" v-on:cedit="edit($event)"></cat-table>
	
	<form v-on:submit.prevent="addoredit()">
	<div class="formularz">
		<div class="form-group">
			<label for="cat">kot</label>
			<input v-model="cat" type="text" class="form-control" id="formGroupExampleInput" placeholder="kot">
		</div>
		<div class="form-group">
			<label for="nazw">karma</label>
			<input v-model="food"  type="text" class="form-control" id="formGroupExampleInput2" placeholder="karma">
		</div>
		<button type="submit" class="btn btn-info">Zapisz</button> <button type="reset" class="btn btn-danger">Wyczyść pola</button>
	</div>
	</form>
	<kolor></kolor>
  </div>
</template>

<script>
import CatTable from "./CatTable.vue";
import kolor from "./kolor.vue"
export default {
	components:{CatTable,kolor},

  data:function(){
	return{
		cats:[],
		cat:null,
		food:null,
		id:null,
		alert:false,
		}
		
	},
	methods:{
	addoredit:function(){
		var nowy={
			cat:this.cat,
			food:this.food,
			id:Math.random()*1000,
			};
			if(this.id==null){
				if(this.cat==null || this.food==null){
					this.alert=true;
				}
				else{
					this.alert=false;
					this.cats.push(nowy);
				}
			}
			else{
				var newcat=this.cats.find((p) => {return p.id===this.id});
				newcat.cat = this.cat;
				newcat.food = this.food;
				this.id=null;
			}
			this.cat=null;
			this.food=null;
			},
	deletec:function(id){
	this.cats=this.cats.filter((p) => {return p.id != id})
	},
	edit:function(id){
	this.cat=this.cats.find((p) => {return p.id === id}).cat;
	this.food=this.cats.find((p) => {return p.id === id}).food;
	this.id=id;
		},
	
	
	
	
	
	}
			}
		

</script>

<style>
	.formularz{
	margin:1rem;
	}
	.container-fluid{
	padding:0;
	margin:0;
	}
	
</style>

