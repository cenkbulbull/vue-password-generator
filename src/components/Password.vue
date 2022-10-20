<template>
	<div class="container d-flex flex-column align-items-center mt-5">
		<div class="password mt-3 d-flex justify-content-between">
			<textarea class="result-area form-control " rows="1" readonly>{{result}}</textarea>
			<a style="cursor:pointer;" @click="copyPassword()"><font-awesome-icon style="color: #87ab93;font-size: 20px;" class="mt-2" icon="fa-regular fa-copy" /></a>
		</div>
		<div class="options">
			<div style="font-size:11px;" class="d-flex justify-content-between">
				<span>Character Length</span>
				<span style="color:#87ab93" >{{length}}</span>
			</div>
			<div>
				<input v-model="length" type="range" class="form-range " min="8" max="20" step="1">
			</div>
			<div class="form-check">
				<input v-model="characters" class="form-check-input" type="checkbox" value="ABCDEFGHIJKLMNOPQRSTUVWXYZ">
				<label class="form-check-label">
					Include Uppercase Letters
				</label>
			</div>
			<div class="form-check">
				<input v-model="characters" class="form-check-input" type="checkbox" value="abcdefghijklmnopqrstuvwxyz">
				<label class="form-check-label">
					Include Lowercase Letters
				</label>
			</div>
			<div class="form-check">
				<input v-model="characters" class="form-check-input" type="checkbox" value="0123456789">
				<label class="form-check-label">
					Include Numbers
				</label>
			</div>
			<div class="form-check">
				<input v-model="characters" class="form-check-input" type="checkbox" value="?*-_!.&/@,\$&<>()">
				<label class="form-check-label">
					Include Symbols
				</label>
			</div>

			<div v-if="result!=''" class="strenght p-3 mt-3 d-flex justify-content-between">
				<span>STRENGTH</span>
				<div>
					<span style="background-color: #face6e !important;" v-for="strenght in characters" class="p-2 mx-1"></span>
				</div>
			</div>

			<button :disabled="!characters.length>0" @click="randomPassword()" class="generate_btn btn w-100 mt-3">GENERATE</button>
		</div>
	</div>
</template>
<script>
	export default{
		data () {
			return {
				length:10,
				characters:[],
				result:"",
			}
		},
		methods:{
			randomPassword(){
				this.result=""
				var newcharacters = this.characters.join("");
        		//console.log(newcharacters)
        		for ( var i = 0; i < this.length; i++ ) {
        			this.result += newcharacters.charAt(Math.floor(Math.random() * newcharacters.length));
        		}
        	},
        	copyPassword(){
        		var result = document.querySelector(".result-area")
        		result.select();
        		document.execCommand('copy');
        	}
        }
    }
</script>
<style scoped>
	.password{
		background-color: #24232a;
		width: 350px;
		padding: 15px 20px;
	}
	.options{
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		background-color: #24232a;
		width: 350px;
		height: 350px;
		padding: 15px 20px;
		margin-top: 20px;
	}
	.result-area {
		background-color: transparent !important;
		color: #fff !important;
		border: 0 !important;
		resize: none;
		width: 250px;
	}
	.generate_btn{
		background-image: linear-gradient(120deg, #d4fc79 0%, #96e6a1 100%);
		color: #24232a;
		font-size: 11px;
		font-weight: bolder;
		letter-spacing: 1px;
		padding: 13px 0 !important;
	}
	textarea:focus, 
	textarea.form-control:focus, 
	select.form-control:focus{
		box-shadow: inset 0 0 0;
	}
	.strenght{
		background-color: #18171F;
		color: #47464F;
		font-size: 11px;
		font-weight: bold;
		letter-spacing: .5px;
	}
</style>