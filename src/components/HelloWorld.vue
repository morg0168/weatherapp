<template>
  <div class="hello">
    <h1>{{ nowformatted()[0] }}</h1>

    <h3>days left until</h3>

    <h2>{{ nowformatted()[1] }}</h2>

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

      seasonToMatch: '',

      dFormatted: '',
      dFormatted2: '',


      nowformatted: function(seasonToMatch, dFormatted, dFormatted2, theMonth, timeToSeason1, season1, season2, season3, season4, now, startDate, startDateSeason) {

        //add 284 and debug at winter again
        now = new moment().add(0, 'day');

        //account for leap year

        startDate = now.clone().startOf('year');

        //december 21st of Y-1
        startDateSeason = startDate.clone().subtract(1, 'month').add(21, 'days');

        //march 21st Y
        season1 = startDateSeason.clone().add(3, 'months');

        //june 21st Y
        season2 = startDateSeason.clone().add(6, 'months');

        //september 21st Y
        season3 = startDateSeason.clone().add(9, 'months');

        //december 21st Y
        season4 = startDateSeason.clone().add(12, 'months');


        timeToSeason1 = [];

        if (now.isBefore(season1) && now.isAfter(startDateSeason)) {

          seasonToMatch = season1;

          theMonth = 'spring';

        } else if (now.isAfter(season1) && now.isBefore(season2)) {

          seasonToMatch = season2;

          theMonth = 'summer';

        } else if (now.isAfter(season2) && now.isBefore(season3)) {

          seasonToMatch = season3;

          theMonth = 'autumn';

        } else if (now.isAfter(season3) && now.isBefore(season4)) {

          seasonToMatch = season4;

          theMonth = 'winter';

        } else {

          //its the 21st

        }


        dFormatted = seasonToMatch.diff(now, 'days');

        dFormatted2 = theMonth;

        return [dFormatted, dFormatted2];

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
