<template>
  <div id="app">
    <p>Rubiks scrambler</p>
    <div class="container">
            <ul v-if="loading">
                <li v-for="(color, index) in scrambledColors" :key=index>
                    <div class="square">{{color}}</div>
                </li>    
            </ul>  
        </div>  
  </div>
</template>

<script>


import Scrambler from './components/Scrambler.vue'



export default {
  name: 'app',
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
            for(let i = 0; i < 9; i++){
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
    created(){
        this.generateColors(this.scrambledColors);
        this.loading = true;
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
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

p{
  transform: translateY(5vh);
}

div.square{
  height: 250px;
  width: 250px;
}

div.container {
  height: 900px;
  width: 900px;
  margin:0 auto;
  transform: translateY(15vh);
  display: flex;
  flex-flow: row wrap
}
</style>
