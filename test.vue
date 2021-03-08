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
     testplaces: [
        {
          id: "790",
          title: "Vakcína Nemocnica Agel Bánovce",
          longitude: "18.25625860",
          latitude: "48.72012930",
          city: "Bánovce nad Bebravou",
          street_name: "Hviezdoslavova",
          street_number: "23",
          postal_code: "95701",
          region_id: "8",
          region_name: "Trenčiansky",
          county_id: "33",
          county_name: "Bánovce nad Bebravou",
          age_from: "70",
          age_to: null,
          calendar_data: [
            { c_date: "2021-03-10", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-11", is_closed: 0, free_capacity: 0 },
            { c_date: "2021-03-12", is_closed: 0, free_capacity: 0 },
            { c_date: "2021-03-13", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-14", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-15", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-16", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-17", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-18", is_closed: 1, free_capacity: 5 },
            { c_date: "2021-03-19", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-20", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-21", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-22", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-23", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-24", is_closed: 1, free_capacity: 0 },
          ],
        },
        {
          id: "007",
          title: "Vakcína Horna Dolna",
          longitude: "18.25625860",
          latitude: "48.72012930",
          city: "Bánovce nad Bebravou",
          street_name: "Hviezdoslavova",
          street_number: "23",
          postal_code: "95701",
          region_id: "8",
          region_name: "Trenčiansky",
          county_id: "33",
          county_name: "Bánovce nad Bebravou",
          age_from: "70",
          age_to: null,
          calendar_data: [
            { c_date: "2021-03-10", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-11", is_closed: 0, free_capacity: 0 },
            { c_date: "2021-03-12", is_closed: 0, free_capacity: 4 },
            { c_date: "2021-03-13", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-14", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-15", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-16", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-17", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-18", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-19", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-20", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-21", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-22", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-23", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-24", is_closed: 1, free_capacity: 0 },
          ],
        },
        {
          id: "889",
          title: "Vakcína Zelený sen, Banská Bystrica",
          longitude: "19.16405040",
          latitude: "48.74096306",
          city: "Banská Bystrica",
          street_name: "Cesta k nemocnici",
          street_number: "1/B",
          postal_code: "97401",
          region_id: "5",
          region_name: "Banskobystrický",
          county_id: "23",
          county_name: "Banská Bystrica",
          age_from: "70",
          age_to: null,
          calendar_data: [
            { c_date: "2021-03-10", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-11", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-12", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-13", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-14", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-15", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-16", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-17", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-18", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-19", is_closed: 1, free_capacity: 3 },
            { c_date: "2021-03-20", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-21", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-22", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-23", is_closed: 1, free_capacity: 0 },
            { c_date: "2021-03-24", is_closed: 1, free_capacity: 1 },
          ],
        },
      ],
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
