<template>
  <div>
      <div class="container">
        <p>Rubiks scrambler</p>
            <ul v-if="loaded">
                <li v-for="(color, index) in scrambledColors" :key=index>
                    <div class="square">{{color}}</div>
                </li>    
            </ul>  
        </div>  
  </div>
</template>

<script>
export default {
    name: 'Scrambler',
    data () {
        return {
            colorOptions: {
                    'white':'white',
                    'red':'red',
                    'blue':'blue',
                    'yellow':'yellow',
                    'orange':'orange',
                    'green':'green',
                },
            scrambledColors: [],
            loading: false
        }
    },
    methods: {
        generateColors(arr) {
            for(i = 0; i < 9; i++){
                this.checkScrambledColors(arr);
                arr.push(this.randomProperty(this.colorOptions));
                console.log(arr)
            }

        },
        randomProperty (obj) {
            let keys = Object.keys(obj);
            return obj[keys[ keys.length * Math.random() << 0]];
        },
        checkScrambledColors(arr){
                let sortedArr = arr.slice().sort();
                // JS by default uses a crappy string compare.
                // (we use slice to clone the array so the
                // original array won't be modified)
                let results = [];
                let counter = 1
                for (let i = 0; i < sortedArr.length - 1; i++) {
                    if (sortedArr[i + 1] == sortedArr[i]) {
                        counter++;
                        if(counter === 5) {
                           continue; 
                        }
                        results.push(sortedArr[i]);
                    }
                }
                return results;
        }
    },
    mounted(){
        this.generateColors(this.scrambledColors);
        this.loading = true;
    }    
}
</script>

<style>
</style>
