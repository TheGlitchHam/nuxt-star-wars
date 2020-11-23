<template>
  <div class="container">
    <div>
      <h1 class="title">
        Star Wars Films
      </h1>
      <h2 class="subtitle text-primary mb-5">
        - A Nuxt.js project
      </h2>
    </div>
    <b-card-group deck>
      <b-card
        v-for="item in filmsOrderedByID"
        :key="item.episode_id"
        class="mb-5"
      >
        <b-list-group>
          <b-list-group-item>
            <b-card-title class="text-primary">
              {{ item.title }}
            </b-card-title>
          </b-list-group-item>
          <b-list-group-item>
            <div class="opening-crawl text-primary">
              {{ item.opening_crawl }}
            </div> </b-list-group-item
          ><b-list-group-item>
            <strong>Episode:</strong> {{ item.episode_id }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Director:</strong> {{ item.director }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Producer:</strong> {{ item.producer }}
          </b-list-group-item>
          <b-list-group-item>
            <strong>Release Date:</strong> {{ item.release_date }}
          </b-list-group-item>
        </b-list-group>
      </b-card>
    </b-card-group>
  </div>
</template>

<script>
import axios from "~/plugins/axios";
import _ from "lodash";

export default {
  components: {},
  computed: {
    filmsOrderedByID: function() {
      const filmsOrdered = _.orderBy(this.films, "episode_id");
      return filmsOrdered;
    }
  },
  async asyncData({ error }) {
    const films = await axios
      .get("films/")
      .then(response => ({
        films: response.data.results
      }))
      .catch(e => {
        error({ statusCode: 404, message: "Endpoint could not be resolved" });
      });
    return films;
  }
};
</script>

<style></style>
