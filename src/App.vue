<template>
  <div>
    <div class="row scoreBoard" >
      <div class="col">(O) has {{ wins.O }} wins</div>
      <div class="col" >
          <label for="sel1">Select Level:</label>
          <select class="form-control" id="sel1" v-model="level">
              <option value="0">Easy</option>
              <option value="1">Medium</option>
              <option value="2">Hard</option>
              <option value="3">UnBeatable</option>
          </select>
        </div> 
      <div class="col">(X) has {{ wins.X }} wins</div>
    </div>
    <div class="container-fluid">
      <div class="row ">
        <div class="col text-center">
          <h1>Tic Tac Toe</h1>
          <h2>Match #{{ matches + 1 }}</h2>
        </div>
      </div>
      <div class="row text-center">
        <div class="col-md-8 col-sm-12 mb-2 text-center" id="app">
          <grid :alg="alg" :maxLevel="level" class="mx-auto"></grid>
          <button class="restart wm-270" @click="restart">Restart</button>
        </div>
        <div class="col-md-4 col-sm-12 text-center" id="app">
          <h1>Information</h1>
          <h3>number of space nodes</h3> 
          <h5>{{numberOfNodes}}</h5>
          <h3>number of iterations</h3> 
          <h5>{{numberOfComputedNodes}}</h5>
           <div class="form-group">
              <h3 for="sel1">Selected algorithm:</h3>
              <select class="form-control" id="sel1" v-model="alg">
                <option value="MinMax">MinMax</option>
                <option value="AlphaBeta">AlphaBeta</option>
              </select>
            </div> 
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Grid from './components/Grid.vue'

export default {
  components: { Grid },
  name: 'app',
  data () {
    return {
      matches: 0,
      wins: {
        O: 0,
        X: 0
      },
      level:1,
      alg:"MinMax",
      numberOfNodes:0,
      numberOfComputedNodes :0
    }
  },

  methods: {
    restart () {
      Event.$emit('clearCell')

      Event.$emit('gridReset')

      this.matches++
    }
  },

  created () {
    Event.$on('win', winner => this.wins[winner]++)
  }
}
</script>

<style>
body {
  background-color: #141311;
  color: #fff;
  font-family: 'Dosis', Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 0px;
}

#app {
  color: #fff;
}

h1 {
  text-transform: uppercase;
  font-weight: bold;
  font-size: 3em;
}

.restart {
  background-color: #e74c3c;
  color: #fff;
  border: 0px;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  font-family: 'Dosis', Helvetica, sans-serif;
  font-size: 1.4em;
  font-weight: bold;
  margin: 0px;
  padding: 15px;
  width: 100%;
}

.restart:hover {
  background-color: #c0392b;
  cursor: pointer;
}

.scoreBoard {
  align-items: center;
  background-color: #a2482e;
  box-shadow: 10px solid #fff;
  padding: 20px;
  overflow-x: none;
}

.scoreBoard h2 {
  margin: 0px;
}

.scoreBoard div {
  font-size: 1.5em;
  font-weight: bold;
  margin-left: 20px;
}
.wm-270{
  max-width: 270px;
}
  
</style>
