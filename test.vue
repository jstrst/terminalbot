<template>
  <section class="container">
    <button class="button" @click="getURL()">Get data - manual trigger</button>

    <br />
    <br>--------------------- 
    <br>
    No. of requests: {{ counter }} <br>

    <strong>FREE PLACES:</strong>
    <div v-if="!freeOnly">NOTHING AVAILABLE...try again later...</div>
    <div v-else>
    <strong>{{ freeOnly }}</strong>
    </div>


    <ul>
      <li v-for="(data, index) in availablePlaces" :key="index">{{data.count}} - {{ data.title }}  </li>
    </ul>

  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "MojeData",
  data() {
    return {
     url:"https://mojeezdravie.nczisk.sk/api/v1/web/get_all_drivein_times_vacc",
     counter: 0,
     places: [],
    };
  },
  props: {
    bot: String
  },
  computed: {
    // get All places
    availablePlaces() {
      let output = []

      this.places.forEach(element => {

         let x  = {}
         x.title = element.title
         x.count = 0

         element.calendar_data.forEach(item => {
              x.count +=  item.free_capacity
         });
         output.push(x)
      });

      return output;
    },

    // filter free places...  and send notifiacion if not empty... 
    freeOnly() {
     let res = this.availablePlaces.filter( item => item.count > 0 )
     if (res.length == 0) {
       return false
    }
     else {
       this.sendMsg(res)  // check for change later
       return res 
     }
    }    

  },

  methods: {

    getURL() {
      axios
        .get(this.url)
        .then((response) => {
          // handle success
          this.places = response.data.payload;
          this.counter++
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        })
    },

    createMsg(val) {
      let m = ''
      val.forEach(element => {
        m = m + element.title + ": " + element.count + "%0A"
      });
      return m 
    },

    sendMsg(m) {
      let url = this.bot + this.createMsg(m);
      axios.post(url)
    }
  },
};
</script>

<style>
</style>
