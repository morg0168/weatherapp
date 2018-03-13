<template>
  <div class="hello">
    <h1>{{ nowformatted() }}</h1>

    <h3>days left until</h3>

    <h2>{{  }}</h2>

    <button class="btn btn-primary" v-on:click="counter++">You've clicked this button {{ counter }} times.</button>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'HelloWorld',
  data () {
    return {
      counter: 0,
      moment: 'moment',

      startDate: '',
      startDateSeason: '',

      theMonth: '',
      timeToSeason1: '',

      season1: '',
      season2: '',
      season3: '',
      season4: '',


      nowformatted: function(theMonth, timeToSeason1, season1, season2, season3, season4, now, startDate, startDateSeason) {

        startDate = moment().startOf('year');

        startDateSeason = startDate.subtract(1, 'month').add(21, 'days');

        season1 = startDateSeason.clone().add(3, 'months');
        season2 = startDateSeason.clone().add(6, 'months');
        season3 = startDateSeason.clone().add(9, 'months');
        season4 = startDateSeason.clone().add(12, 'months');

        now = new moment();

        timeToSeason1 = [];

        if (now.isBefore(season1)) {

          theMonth = 'spring';

          return season1.diff(now, 'days');

        }

        //if now.isSame(nextMoment);

      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>
