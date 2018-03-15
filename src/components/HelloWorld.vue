<template>
  <div class="hello">
    <h1>{{ nowformatted()[0] }}</h1>

    <h3>days left until</h3>

    <h2>{{ nowformatted()[1] }}</h2>

    <button class="btn btn-primary" v-on:click="counter++">You've clicked this button {{ counter }} times.</button>

    <h2><blockquote>{{ schedule }}</blockquote></h2> 
     <h2>{{ response }}</h2>

  </div>
</template>

<script>

import moment from 'moment'

import axios from "axios";

export default {
  name: 'HelloWorld',

  data: function () {
    return {
      counter: 0,
      moment: 'moment',

      startDate: '',
      startDateSeason: '',

      theMonth: '',

      season1: '',
      season2: '',
      season3: '',
      season4: '',

      seasonToMatch: '',

      dFormatted: '',
      dFormatted2: '',

      schedule: '',
      response: ''
    }
  }, 

   mounted() {
      axios({ method: "GET", "url": "https://httpbin.org/ip" }).then(result => {
          this.schedule = result.data.origin;
      }, error => {
          console.error(error);
      });
  },

  methods: {
      nowformatted: function(seasonToMatch, dFormatted, dFormatted2, theMonth, season1, season2, season3, season4, now, startDate, startDateSeason) {

        now = new moment().add(0, 'days');

        //jan 1st of Y
        startDate = now.clone().startOf('year');

        //december 21st of Y-1
        startDateSeason = startDate.clone().subtract(1, 'month').add(21, 'days');

        //march 21st Y
        season1 = startDateSeason.clone().add(3, 'months');

        //june 21st Y
        season2 = startDateSeason.clone().add(6, 'months');

        //september 21st 2018
        season3 = startDateSeason.clone().add(9, 'months');

        //december 21st Y  2018
        season4 = startDateSeason.clone().add(12, 'months');


        if (now.isBefore(season1) && now.isAfter(startDateSeason)) {

          seasonToMatch = season1;

          theMonth = 'spring';

        } 

        //its march 21st

        else if (now.isSame(season1)) {

          seasonToMatch = season1;

          theMonth = 'spring';

        }

        else if (now.isAfter(season1) && now.isBefore(season2)) {

          seasonToMatch = season2;

          theMonth = 'summer';

        }  

        //its june 21st

        else if (now.isSame(season2)) {

          seasonToMatch = season2;

          theMonth = 'summer';

        }

        else if (now.isAfter(season2) && now.isBefore(season3)) {

          seasonToMatch = season3;

          theMonth = 'autumn';

        }  

        //its september 21st

        else if (now.isSame(season3)) {

          seasonToMatch = season3;

          theMonth = 'autumn';

        }

         else if (now.isAfter(season3) && now.isBefore(season4)) {

          seasonToMatch = season4;

          theMonth = 'winter';

        }  

        //its december 21st

        else if (now.isSame(season4)) {

          seasonToMatch = season4;

          theMonth = 'winter';

        } 
 
        else if (now.isAfter(season4)) {

          startDateSeason.add(1, 'year');

          season1 = startDateSeason.clone().add(3, 'months');

          seasonToMatch = season1;

          theMonth = 'spring';

        } 

        else {

          //its the 21st

        }

        dFormatted = seasonToMatch.diff(now, 'days');

        dFormatted2 = theMonth;

        return [dFormatted, dFormatted2];

      }

    },

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
