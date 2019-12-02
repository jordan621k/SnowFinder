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
      res: {
        'name': '',
        'weather': '',
        'trails': '',
        'lifts': ''
      },
      headers:[
        { text: 'Name', value: 'name' },
        { text: 'Weather', value: 'weather' },
        { text: 'Trails', value: 'trails' },
        { text: 'Lifts', value: 'lifts' },
      ]
    };
  },
  created() {
    this.crawl();
    this.crawl2();
  },
  methods: {
    async crawl() {
      this.results = [];
      this.res['name'] = 'Hunter';
      let self = this;
      await request("https://www.huntermtn.com", function(error, response, body) {
        if (error) {
          console.log("Error: " + error);
        }
        console.log("Status code: " + response.statusCode);
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
              self.res['trails'] = val;
            } else if (label === 'Lifts') {
              self.res['lifts'] = val;
            } else {
              self.res['weather'] = val;
            }
          });
        });
      });

      this.results.push(this.res);
    },
    async crawl2() {
      this.results = [];
      this.res['name'] = 'MountainCreek';
      let self = this;
      await request("https://cors-anywhere.herokuapp.com/https://mountaincreek.com/mountainreport", function(error, response, body) {
        if (error) {
          console.log("Error: " + error);
        }
        console.log("Status code: " + response.statusCode);
        const $ = cheerio.load(body);

        let temp = $("div.condition.conditions-temp").text().trim()
        //console.log(temp)
        self.res['weather'] = temp

        $("li.open_trail").each(function() {
          let val = $(this)
          .find("span.trail_lift_open")
          .text()
          .trim();
          self.res['trails'] = val
        });
        $("li.open_lift").each(function() {
          let val = $(this)
          .find("span.trail_lift_open")
          .text()
          .trim();
          self.res['lifts'] = val
        });
      });

      this.results.push(this.res);
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
