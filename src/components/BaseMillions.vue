<template>
  <div class="basemillions">
    <h1>🌈 BaseMillions 🌈</h1>
    <p>
      Converts your data into colors
    </p>
    <br />
    <h2>Input Your Data</h2>
    <input v-model="input" type="text" />
    <h3>Hashed Color</h3>
    <div class="hashed" v-for="(item, index) in hashed">
      <div class="box" v-bind:style="{ backgroundColor: '#'+item }">
      </div>
    </div>
    <h3>Unicode Color</h3>
    <div class="hashed" v-for="(item, index) in color">
      <div class="box" v-bind:style="{ backgroundColor: '#'+item }">
      </div>
    </div>
    <h3>ASCII Color</h3>
    <div class="hashed" v-for="(item, index) in ascii">
      <div class="box" v-bind:style="{ backgroundColor: '#'+item }">
      </div>
    </div>
  </div>
</template>
<script>
var crypto = require('crypto')

export default {
  data: function () {
  return {
    input: ""
  }
  },
  computed: {
    color: function () {
      var colors = Buffer.from(this.input, 'utf8').toString('hex').match(/.{1,6}/g)
      if (colors != null) {
      colors.forEach(function(part, index, colors) {
        colors[index] = colors[index].padStart(6, "0")
      });
      }
      return colors
    },
    ascii: function () {
      if (this.input != "") {
        var colors = this.input.split("")
        colors.forEach(function(part, index, colors) {
          colors[index] = colors[index].charCodeAt(0)
          console.log(colors[index])
          var hex = colors[index].toString(16)
          colors[index] = hex.length == 1 ? "0" + hex : hex;
        });
        colors = colors.join("").match(/.{1,6}/g)
        colors.forEach(function(part, index, colors) {
          colors[index] = colors[index].padStart(6, "0")
        });
        console.log(colors)
      }
      return colors
    },
    hashed: function () {
      var string1 = crypto.createHash('sha512').update(this.input).digest("hex")
      var string2 = string1.substr(0, string1.length - 2)
      var string3 = string1.substr(string1.length - 2, 2).padStart(6, "0")
      var string4 = string2 + string3
      return string4.match(/.{1,6}/g)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
.hashed {
  display: inline-block;
}
li {
  display: inline-block;
  margin: 0;
}
a {
  color: #42b983;
}
.box {
  border: 1px solid black;
  display: inline-block;
  height: 25px;
  width: 25px;
}
</style>
