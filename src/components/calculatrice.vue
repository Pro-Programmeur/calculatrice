<script>

export default{
  name: 'calculatrice',
  props: {
    msg: String
  },

  data(){
    return{
      calculatriceValue: '',
      calculatriceElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',3,2,1,'=',0,'.'],
      operator: null,
      previouscalculatriceValue: '',
    }
  },
    methods:{
// Virgule
      action(n){
        if (!isNaN(n) || n === '.') {
          this.calculatriceValue += n + '';
        }

   // Effacer les données

    if (n === 'C') {
      this.calculatriceValue = '';
    }

    // Pourcentage

    if(n === '%'){
      this.calculatriceValue = this.calculatriceValue/100 + '';
    }

   // Calcul avec tous les signes

    if(['+','-','*','/'].includes(n)){

        this.operator= n;
        this.previouscalculatriceValue = this.calculatriceValue;
        this.calculatriceValue = '';
    }

    if(n === '='){
      
        this.calculatriceValue = eval(
        this.previouscalculatriceValue + this.operator + this.calculatriceValue
      );
        
        this.previouscalculatriceValue = '';
        this.operator = null;
        } 
      }

    }

  }





</script>

<template>
  
<div id="cal" class="p-3">

<!-- Calculatrice result -->
      <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white">
  
         {{calculatriceValue || 0  }}

   </div>

 <!-- Calculatrice buton -->

 <div class="row no-gutters">
 
      <div class="col-3" v-for="n in calculatriceElements" :key="n">

          <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
                :class="{ 'bg-vue-green': ['C','*','/','-','+','%','='].includes(n)}" @click="action(n)">

                {{ n  }}

                </div>
      </div>
 </div>

</div>

</template>
