<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12 col-md-12 controls shadow p-3 mb-5 bg-white rounded">
        <div class="row">
          <div class="col-md-1"></div>
          <div class="col-md-5 ">
            <h1>You</h1>
            <div class="progress">
              <div class="progress-bar"></div>
            </div>  
          </div>
          <div  class="col-md-5 ">
            <h1>Opponent</h1>
            <div class="progress">
              <div class="progress-bar"></div>
            </div>
          </div>
          <div class="col-md-1"></div>
        </div>
      </div>
      <div class="col-md-12 controls shadow p-3 mb-5 bg-white rounded">
          <button class="btn btn-lg btn-success float-center">Start New Game</button>
      </div>
      <div class="col-md-12 controls shadow p-3 mb-5 bg-white rounded">
        <button class="btn btn-lg btn-danger float-center btn-space">Attack</button>
        <button class="btn btn-lg btn-warning float-center btn-space">Special Attack</button>
        <button class="btn btn-lg btn-primary float-center btn-space">Heal</button>
        <button class="btn btn-lg float-center btn-space">Give Up</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>
.controls{
  text-align: center;
}
.btn-space {
    margin-right: 25px;
}
/*
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.row{
  margin: 2%;
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
*/

.progress{
  height: 40px;
}
.progress-bar{
  width: 60%;
}
</style>
