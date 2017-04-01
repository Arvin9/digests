<template>
  <div>
    <x-header :left-options="{showBack: false}">
      This is the page title.
    </x-header>
    <cell title="公告">
      <marquee>
        <marquee-item v-for="i in 5" :key="i" @click.native="onClick(i)">{{ 'JavaScript is the best language '}}{{i}}</marquee-item>
      </marquee>
    </cell>

    <card v-for="digest in digests">
      <h3 slot="header" class="card-padding"> {{digest.title}} </h3>
      <p slot="content" class="card-padding"> {{digest.content}} </p>
      <span slot="footer"> {{digest.provenance}}--{{digest.add_time}} </span>
    </card>

  </div>
</template>

<script>
import { XHeader, Marquee, MarqueeItem, Group, Cell, Card} from 'vux'

export default {
  data () {
    return {
      digests:[]
    }
  },
  components: {
    XHeader,
    Marquee,
    MarqueeItem,
    Group,
    Cell,
    Card
  },
  computed: {

  },
  beforeMount: function() {
    let that = this;
    var req = new Request('http://localhost:3000/digests', {method: 'GET', mode: "cors"});
    fetch(req).then(function(response) {
      return response.json();
    }).then(function(json) {
      that.digests = json;
    });
  },
  methods: {
    onClick (i) {
      console.log(i);

    }
  }
}
</script>

<style scoped>

</style>
