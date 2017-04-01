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


    <x-input title="标题" v-model="title"></x-input>
    <x-textarea title="内容" v-model="content" placeholder="请填写详细内容" :show-counter="true" :rows="3"></x-textarea>
    <x-input title="来源" v-model="provenance"></x-input>
    <x-button @click.native="postDigest">提交</x-button>

    <card v-for="digest in digests">
      <h3 slot="header" class="card-padding"> {{digest.title}} </h3>
      <p slot="content" class="card-padding"> {{digest.content}} </p>
      <span slot="footer"> {{digest.provenance}}--{{digest.add_time}} </span>
    </card>
  </div>
</template>

<script>
import { XHeader, Marquee, MarqueeItem, Group, XInput, XTextarea, Cell, Card, XButton } from 'vux'

export default {
  data () {
    return {
      digests: [],
      title: "",
      content: "",
      provenance: "",
    }
  },
  components: {
    XHeader,
    Marquee,
    MarqueeItem,
    Group,
    XInput,
    XTextarea,
    Cell,
    Card,
    XButton
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
    },
    postDigest: function() {
      let title = this.title;
      let content = this.content;
      let provenance = this.provenance;

      var req = new Request('http://localhost:3000/digests', {
        method: 'POST',
        headers: { 'Accept': 'application/json', 'Content-Type': 'application/json'},
        body: JSON.stringify({title:title,content:content,provenance:provenance})
      });
      fetch(req).then(function(response) {
        return response.json();
      }).then(function(json) {
         console.log(json);
      });
    }

  }
}
</script>

<style scoped>

</style>
