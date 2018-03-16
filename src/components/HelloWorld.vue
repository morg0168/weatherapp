<template>
  <div class="hello">
    <h1>{{ nowformatted()[0] }}</h1>

    <h2>days till</h2>

    <h3>{{ nowformatted()[1] }}</h3>

    <button class="btn btn-primary" v-on:click="counter++">You've clicked this button {{ counter }} times.</button>

    <h6><blockquote>{{ todaysSunrise }}</blockquote></h6> 
    <h6><blockquote>{{ todaysSunset }}</blockquote></h6> 

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

      response: '',
      ipresult: '',

      sunrise: '',
      sunset: '',

      str: '',

      todaysSunrise: '',
      todaysSunset: '',

      sunSchedule: ''
    }
  }, 

   mounted(ipresult) {

      //get ip

      axios({ method: "GET", "url": "https://httpbin.org/ip" }).then(result => {

          ipresult = result.data.origin;

          console.log(ipresult);

          getCoordinates(ipresult);

      }, error => {

          console.error(error);

      });

      //consume http://ipinfo.io/ api for latitude and longitude

      function getCoordinates(ipresult){

        axios({method: "GET", "url": "https://www.iplocate.io/api/lookup/" + ipresult}).then(result => {

          console.log(response);

        }, error => {

            console.error(error);

        });

      }

      //consume https://sunrise-sunset.org/api for sunset and sunrise times

      axios({ method: "GET", "url": "https://api.sunrise-sunset.org/json?lat=36.7201600&lng=-4.4203400" }).then(result => {


          this.sunrise = result.data.results.sunrise;

          this.sunset = result.data.results.sunset;

          this.str = [this.sunrise, this.sunset];



          //turn sunrise and sunset strings into moment objects

          this.todaysSunrise = moment(this.str[0], 'HH:mm:ss A');

          this.todaysSunset = moment(this.str[1], 'HH:mm:ss A');

          console.log(this.todaysSunset); 



          //countdown minutes till



         
      }, error => {

          console.error(error);

      });
    


      //change background dynamically

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
