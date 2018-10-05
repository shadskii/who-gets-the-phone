<template>
  <v-container grid-list-lg>
    <v-slide-y-transition mode="out-in">
      <v-layout row wrap justify-center>
        <v-flex xs10>
          <v-card>
            <v-card-title>
              <h2>Start</h2>
            </v-card-title>
            <v-card-text>
              Add all of the contenders to the list and then hit the GO button to find out who gets the phone!
            </v-card-text>
            <v-progress-linear :value="(count/repeat)*100"></v-progress-linear>
            <v-card-actions>
              <v-btn @click="findWinner" :disabled="contenders.length === 0">GO</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
        <v-flex xs10>
          <v-card>
            <v-card-title>
              <h2>Add a contender</h2>
            </v-card-title>
            <v-card-actions>
              <v-text-field v-model="textField" />
              <v-btn @click="addContender" small>ADD</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
        <v-flex xs10>
          <transition-group name="flip-list">
            <v-flex v-for="con in contenders" :key="con" xs12>
              <v-card :color="(count===repeat && contenders.indexOf(con) === 0) ? 'success' : ''">
                <v-card-title>
                  <h1> {{con}} </h1>
                </v-card-title>
              </v-card>
            </v-flex>
          </transition-group>
        </v-flex>
      </v-layout>
    </v-slide-y-transition>
  </v-container>
</template>

<script>
import _ from 'lodash';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      contenders: [],
      textField: '',
      repeat: 25,
      count: 0
    }
  },
  methods:{
    addContender(){
      let c = this.textField;
      this.contenders.push(c);
      this.textField = '';
    },
    shuffleContenders(){
      this.count++;
      this.contenders = _.shuffle(this.contenders);
    },
    findWinner(){
      let time = 500;
      this.count =0;
      let interval = setInterval(this.shuffleContenders, time);
      setTimeout(()=> clearInterval(interval),time *this.repeat);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flip-list-move {
  transition: transform 1s;
}
h3 {
  margin: 40px 0 0;
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
</style>
