<template>

    <form @submit.prevent="valider">
		<label for="colone">Nombre de colones</label>
		<input id="colone" type="number" v-model="inputColone" max="38"/>
		
		<label for="ligne">Nombre de lignes</label>
		<input id="ligne" type="number" v-model="inputLigne" max="20"/>

		<label for="times">Nombre d'occurrences</label>
		<div>
            <input id="times" type="number" v-model="inputTime"/>
            <span>{{afficheCurrentTime}}</span>
        </div>

		<button>Valider</button>
        <button @click="reinitialiser">Reinitialiser</button>
	</form>

	<i class="far fa-play-circle play" @click="steps"></i><br/>
	
	<section>
		<div class="ligne" v-for="ligne in nbr_l" :key="ligne">
			<div v-for="colone in nbr_c" :key="colone">
				<div class="case" 
					:id="'case'+((ligne-1)*nbr_c+colone)"
					@click="changeColor((ligne-1)*nbr_c+colone)"></div>
			</div>
		</div>
	</section>

</template>

<script>
export default {
    name: 'Formulaire',
    data(){
		return{
			nbr_c:20,
			nbr_l:10,
			inputColone:20,
			inputLigne:10,

			currentTime:10,
			inputTime:10,
			afficheCurrentTime:0,

			table:[],
			N:0
		}
	},
	methods:{
		valider(){
			this.nbr_l = this.inputLigne
			this.nbr_c = this.inputColone

			this.currentTime = this.inputTime
		},
		reinitialiser(){
			this.nbr_c = 20
			this.nbr_l = 10

			this.inputColone = 20
			this.inputLigne = 10

			this.currentTime = 10
			this.inputTime = 10
			this.afficheCurrentTime = 0

			let select = null
			this.table.map(val =>{
				select = document.getElementById(`case${val}`)
				select.classList.remove('color')
			})
		},
		changeColor(id){
			let element = document.getElementById(`case${id}`)
			element.classList.toggle('color')
		},
		steps(){
			let timer = setInterval(() => {
				this.step()
				this.currentTime--
				this.afficheCurrentTime = this.inputTime - this.currentTime 
				if(this.currentTime === 0){
					this.currentTime = this.inputTime
					clearInterval(timer)
				}
			}, 500);
		},
		step(){
			let table_step=[]
			let selected = null

			this.table.map(val =>{
				selected = document.getElementById(`case${val}`)
				if(selected.classList.contains("color")){
					table_step.push(1)
				}else{
					table_step.push(0)
				}
			})
			
			this.table.map(input =>{
				let voisins = []
				let somme = 0
				let select = null
				voisins = this.voisinage(input)
				select = document.getElementById(`case${input}`)
				
				for(let i=0;i<voisins.length;i++){
					somme = somme+table_step[voisins[i]-1]
				}
				
				if(table_step[input-1]==1){
					if((somme <= 1) || (somme > 3)){
						select.classList.remove('color')
					}
				}else if(table_step[input-1]==0){
					if(somme == 3){
						select.classList.add('color')
					}
				}
			})	
		},
		voisinage(id){
			const first_l = this.table.filter(val => (val>=1)&&(val<=this.nbr_c))
			const last_l = this.table.filter(val => (val>=(1+(this.nbr_l-1)*this.nbr_c))&&(val<=this.N))
			let last_c = this.table.filter(val => (val%this.nbr_c ==0))
			last_c.pop()
			last_c.shift()
			let first_c = this.table.filter(val => (val%this.nbr_c ==1))
			first_c.pop()
			first_c.shift()

			let table_color=[]
			if(first_l.includes(id)){
				if(id==1){
					table_color.push(2,1+this.nbr_c,2+this.nbr_c)
				}else if(id==this.nbr_c){
					table_color.push(this.nbr_c-1,this.nbr_c*2-1,this.nbr_c*2)
				}else{
					table_color.push(id-1,id+1,id+this.nbr_c-1,id+this.nbr_c,id+this.nbr_c+1)
				}
			}else if(last_l.includes(id)){
				if(id==last_l[0]){
					table_color.push(id-this.nbr_c,id-this.nbr_c+1,id+1)
				}else if(id==this.N){
					table_color.push(this.N-this.nbr_c-1,this.N-this.nbr_c,this.N-1)
				}else{
					table_color.push(id-this.nbr_c-1,id-this.nbr_c,id-this.nbr_c+1,id-1,id+1)
				}
			}else if(last_c.includes(id)){
				table_color.push(id-this.nbr_c-1,id-this.nbr_c,id-1,id+this.nbr_c-1,id+this.nbr_c)
			}else if(first_c.includes(id)){
				table_color.push(id-this.nbr_c,id-this.nbr_c+1,id+1,id+this.nbr_c,id+this.nbr_c+1)
			}else{
				table_color.push(id-this.nbr_c-1,id-this.nbr_c,id-this.nbr_c+1,id-1,id+1,id+this.nbr_c-1,id+this.nbr_c,id+this.nbr_c+1)
			}
			return table_color
		}
	},
	created(){
		this.N = this.nbr_c*this.nbr_l
		this.table = Array.from({length: this.N}, (_, index) => index + 1)
	},
	updated(){
		this.N = this.nbr_c*this.nbr_l
		this.table = Array.from({length: this.N}, (_, index) => index + 1)
	},      
}
    
</script>

<style scoped>
    form{
        width: 50%;
        margin: 1rem auto;
        display: grid;
        grid-template-columns: 50% 1fr;
        place-items: center;
        box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
    }
    label{
        color: rgb(55 65 81);
    }
    input{
        height: 2rem;
        width: 5rem;
        margin: 0.8rem 1rem;
        border-radius: 0.375rem;
        box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05);
        border-color: rgb(209 213 219);
    }
    input:focus{
        border-color: rgb(165 180 252);
    }
    button{
        margin: 0.8rem 1rem;
        padding: 0.5rem;
        font-size: 1.1rem;
        cursor: pointer;
        border: none;
    }
    button:hover{
		font-weight:bold;
        background-color: rgb(134 239 172);
    }

	section{
		display: inline-block;
		margin: 1rem auto;
	}
	.ligne{
		display: flex;
	}
	.case{
		height: 25px;
		width: 25px;
		cursor: pointer;
		background-color: white;
		border:1px solid black;
	}
	.color{
		background-color: black;
	}
	.play{
		font-size: 50px;
		cursor: pointer;
		border-radius: 50%;
	}
	.play:hover{
        background-color: rgb(155, 119, 189);
    }
	.play:active{
		font-weight:bold;
		background-color: rgb(133, 60, 201);
	}
</style>

  