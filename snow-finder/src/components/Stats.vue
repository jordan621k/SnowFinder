<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="results"
      class="elevation-1"
    >
      <template slot="items" slot-scope="props">
        <td>{{ props.item.name }}</td>
        <td class="text-xs-right">{{ props.item.weather }}</td>
        <td class="text-xs-right">{{ props.item.trails }}</td>
        <td class="text-xs-right">{{ props.item.lifts }}</td>
      </template>
    </v-data-table>
  </div>
</template>

<script>
import request from 'request';
import cheerio from 'cheerio';

export default {
  name: "Stats",
  data() {
    return {
      results: [],
      headers: [
        { text: 'Name', value: 'name' },
        { text: 'Weather', value: 'weather' },
        { text: 'Trails', value: 'trails' },
        { text: 'Lifts', value: 'lifts' },
      ]
    };
  },
  created() {
    this.results = [];
    this.hunter();
    this.creek();
  },
  methods: {
    async hunter() {
      let res = {};
      res['name'] = 'Hunter';
      let self = this;
      await request("https://www.huntermtn.com", function(error, response, body) {
        if (error) {
          console.log("Error: " + error);
        }
        const $ = cheerio.load(body);

        $("div.hm-conditionsWidget_preview").each(function() {
          $(this).find("div.hm-conditionsWidget_condition").each(function() {
            let label = $(this)
            .find("div.hm-conditionsWidget_label")
            .text()
            .trim();

            let val = $(this)
            .find("div.hm-conditionsWidget_value")
            .text()
            .trim();

            if (label === 'Trails') {
              res['trails'] = val;
            } else if (label === 'Lifts') {
              res['lifts'] = val;
            } else {
              res['weather'] = val;
            }
          });
        });
        self.results.push(res);
      });
    },
    async creek() {
      let res = {};
      let self = this;
      res['name'] = 'MountainCreek';
      await request("https://cors-anywhere.herokuapp.com/https://mountaincreek.com/mountainreport", function(error, response, body) {
        if (error) {
          console.log("Error: " + error);
        }
        const $ = cheerio.load(body);

        let temp = $("div.condition.conditions-temp").text().trim()
        res['weather'] = temp

        $("li.open_trail").each(function() {
          let val = $(this)
          .find("span.trail_lift_open")
          .text()
          .trim();
          res['trails'] = val
        });
        $("li.open_lift").each(function() {
          let val = $(this)
          .find("span.trail_lift_open")
          .text()
          .trim();
          res['lifts'] = val
        });
        self.results.push(res);
      });
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
