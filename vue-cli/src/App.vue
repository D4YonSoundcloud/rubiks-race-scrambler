<template>
  <div id="app">
    <div class="button-container">
    <p>Rubiks Race Scrambler</p>
    <button @click='generateColors'>Scramble!</button>
    <button @click='showColorsText'>Show Colors Text</button>
    
    </div>
    <div v-if="loading" class="container">
            <ul>
                <li  v-for="(color, index) in scrambledColors" :key=index>
                    <div v-bind:style="{backgroundColor: color}" class="square"><p v-bind:style="{color: color}" v-if="showColors" class="color">{{color}}</p></div>
                </li>    
            </ul>  
        </div>  
  </div>
</template>

<script>

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
            loading: false,
            showColors: false,
        }
    },
    methods: {
        generateColors() {
          if(this.loading) this.loading = false;
          console.log(this.loading);
          if(this.scrambledColors.length === 9){
            this.scrambledColors = []
          }
          console.log(this.scrambledColors);
          for(let i = 0; i < 9; i++){
                this.checkScrambledColors(this.scrambledColors);
                this.scrambledColors.push(this.randomProperty(this.colorOptions));
                console.log(this.scrambledColors)
          }
          
          console.log(this.loading);
          this.loading = true;
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
                      if(counter >= 4) {
                         continue; 
                      }
                        counter++;
                        console.log(counter);
                    }
                  results.push(sortedArr[i]);
                  console.log(results);
                }
                return results;
        },
        showColorsText(){
          this.showColors = !this.showColors
        }
    },
    created(){
        this.generateColors(this.scrambledColors);
    }    
}
</script>

<style>
    * {
        margin: 0;
    }

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333333;
  background-color: rgb(240, 240, 240);
  height: 100vh
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
  margin: 0;
}

a {
  color: #42b983;
}



div.square{
  height: 180px;
  width: 180px;
  border-radius: 8px;
  margin-left: 10px;
  transition: .4s ease;
  margin-top: 10px;
  transform: translateY(5px) translateX(-5px);
  display: flex;
  align-items: center;
}

p.color {
  transform: translateX(60px);
  font-size: 1.5rem;
  transition: .2s ease;
  text-shadow: 1px 1px 3px black;
  cursor: default;

}

div.square:hover{
  border-radius: 15px;
  transform: scale(1.05) translateY(5px) translateX(-5px);
}

div.container {
  height: 600px;
  width: 600px;
  margin:0 auto;
  transform: translateX(15vw) translateY(10vh);
  display: flex;
  justify-content: center;
  flex-flow: row wrap;
  background-color: rgb(22, 22, 22);
  border-radius: 25px;
  transition: .6s ease;
  box-shadow: 0px 0px 5px 5px rgb(202, 202, 202);
}

div.container:hover{
  border-radius: 35px;
  background-color: black;
  box-shadow: 0px 0px 10px 10px rgb(104, 104, 104);
}

div.button-container {
  position: absolute;
  top: 30vh;
  left: 45vh;
  background-color: white;
  width: 400px;
  height: 150px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-flow: column wrap;
  border-radius: 10px;
  transition: .6s ease;
  box-shadow: 5px 5px 2px blue, -5px 5px 2px red, 5px -5px 2px green, -5px 7px 2px yellow,  -7px 5px 2px orange, -5px -5px 2px white;
}

div.button-container:hover {
    transform: scale(1.05);
    box-shadow: 5px 5px 5px blue, -5px 5px 5px red, 5px -5px 5px green, -5px 7px 5px yellow,  -7px 5px 5px orange, -5px -5px 5px white;
}

button {
  margin-top: 20px;
  transition: .6s ease;
}

button:hover{
  transform: scale(1.1);
  box-shadow: 1px 1px 1px blue, -1px 1px 1px red, 1px -1px 1px green, -1px 1px 1px yellow,  -1px 1px 1px orange, -1px -1px 1px white;
}
</style>
