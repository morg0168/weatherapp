<template>
  <div class="hello">
    <h1>{{ nowformatted(now, startDate, startDateSeason) }}</h1>
    <ul>
    <li v-for="index in 4">{{  }}</li>
    </ul>
    <h2>{{ displayTimeLeft() }}</h2>

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
      now: '',
      nextMoment: '',
      previousMoment: '',
      daysLeft: '',

      season1: '',
      season2: '',
      season3: '',
      season4: '',

      timeToSeason1: '',

      dynamicTimestamps: [
        {daysUntil: 22, season: 'spring'}, 
        {daysUntil: 52, season: 'summer'},
        {daysUntil: 83, season: 'fall'},
        {daysUntil: 102, season: 'winter'},
      ],

      nowformatted: function(season1, season2, season3, season4, now, startDate, startDateSeason) {

        startDate = moment().startOf('year');

        startDateSeason = startDate.subtract(1, 'month').add(20, 'days');

        season1 = startDateSeason.clone().add(3, 'months');
        season2 = startDateSeason.clone().add(6, 'months');
        season3 = startDateSeason.clone().add(9, 'months');
        season4 = startDateSeason.clone().add(12, 'months');

        console.log(season1, season2, season3, season4);

        now = new moment();
        //return now;

        if (now.isBefore(season1)) {
          console.log('now is before season1 ' + season1);
          

        }
        //if now.isSame(nextMoment);
        //if now.isBefore(nextMoment);

      },

      //do the calculation
      displayTimeLeft() {
        return 'TEST DAYS LEFT';
        //daysLeft = nextMoment.subtract('days', now);
        //daysLeft.fromNow();
      },
      //do the next calculation
      findNextDifference() {

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
