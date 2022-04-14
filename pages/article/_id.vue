<template>
  <div>
    <h1>{{ item.title }}</h1>
    <div v-html="$md.render(item.content)"></div>
    <nuxt-link :to="'/'">
      <h2>戻る</h2>
    </nuxt-link>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      items: [],
    };
  },
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://septum.microcms.io/api/v1/articles/${params.id}`,
      {
        headers: { "X-MICROCMS-API-KEY": process.env.API_KEY },
      }
    );
    return {
      item: data,
    };
  },
};
</script>
<style>
h1 {
  display: block;
  font-size: 3em;
  text-align: center;
  font-weight: bold;
  border-top: solid 3px #364e96;
  border-bottom: solid 3px #364e96;
}
</style>
