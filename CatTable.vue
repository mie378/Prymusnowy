<template>
	<div v-if="cats.length > 0">
			<div class="row">
				<div class="col-sm-6 col-md-3"><h3>kot</h3></div>
				<div class="col-sm-6 col-md-3"><h3>karma</h3></div>
			</div>
			<div v-for="cat2 in cats" v-bind:key="cat2.id">
				<div class="row">
					<div class="col-sm-6 col-md-3">{{cat2.cat}}</div> 
					<div class="col-sm-6 col-md-3">{{cat2.food}}</div>
					<div class="col-sm-6 col-md-3">
						<button v-on:click="deletec(cat2.id)" type="button" class="btn btn-danger">Usuń</button>
					</div>
					<div class="col-sm-6 col-md-3">
						<button v-on:click="edit(cat2.id)" type="button" class="btn btn-success">Edytuj</button>
					</div>
					
			</div>
			
			</div>
	</div>
	<div v-else class="alert alert-info" role="alert">
		Brak :c 
	</div>
</template>
<script>
export default{
	props:['cats'],
	data:function(){
	return{
	hej:null,
	}
	},
	methods:{
		deletec:function(id){
			this.$emit("cdelete",id);
		},
		edit:function(id){
			this.$emit("cedit",id);
		},
	}

}
</script>
<style>
</style>