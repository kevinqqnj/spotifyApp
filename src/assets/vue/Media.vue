<template>
  <f7-page name="media" no-toolbar id="media">
    <f7-navbar>
      <f7-nav-left back-link="Back" sliding></f7-nav-left>
      <f7-nav-center sliding>Media Detail</f7-nav-center>
      <f7-nav-right>
        <f7-link icon="icon-bars" open-panel=""></f7-link>
      </f7-nav-right>
    </f7-navbar>
    <f7-block-title>Track Info</f7-block-title>
    <f7-list>
      <f7-list-item :media="'<img src=' + searchTracks[mediaId].album.images[0].url +' width=90% >'" :title="searchTracks[mediaId].name">
      </f7-list-item>
      <f7-list-item>
        <f7-label>Type</f7-label>
        <f7-label>{{searchTracks[mediaId].type}}</f7-label>
      </f7-list-item>
      <f7-list-item>
        <f7-label>Artist</f7-label>
        <f7-label>{{searchTracks[mediaId].artists[0].name}}</f7-label>
      </f7-list-item>
    </f7-list>
    <f7-block-title>Album Info</f7-block-title>
    <f7-list form>
      <f7-list-item title="">
        <f7-label>Album</f7-label>
        <f7-label>{{searchTracks[mediaId].album.name}}</f7-label>
      </f7-list-item>
      <f7-list-item>
        <f7-label>Popularity Rank</f7-label>
        <f7-input type="range" min="0" max="100" step="1" v-model="sliderVal" disabled/>
        <f7-input type="text" disabled value="90" class="rangeVal" />
      </f7-list-item>
    </f7-list>
    <f7-block-title>Preview</f7-block-title>
    <f7-block inset>
      <f7-block inner>
        <div id="previewAudio" align="center">
          <audio controls preload :src="searchTracks[mediaId].preview_url"></audio>
        </div>
      </f7-block>
    </f7-block>
    <f7-list>
      <f7-list-item class="bottom">
        <a href="#" class="item-media link favorite"><i class="icon fa fa-star fa-2x"></i> </a>
        <div class="item-title">
          <a :href="searchTracks[mediaId].external_urls.spotify" class="link external">Open in Spotify</a>
        </div>
        <a class="share item-media link" @click="share"><i class="icon fa fa-external-link fa-2x"></i></a>
      </f7-list-item>
    </f7-list>

  </f7-page>
</template>
<script>
import store from '../../store.js'
export default {
  name: 'list',
  props: ['mediaId'], //  <!-- $route.params are also passed as component props: -->
  data() {
    return {
      searchTracks: [],
    }
  },
  mounted() {
    this.searchTracks = store.searchTracks;
  },
  methods: {
    share() {
      var item = this.searchTracks[this.mediaId];
      console.log(item);
      if (window.plugins && window.plugins.socialsharing) {
        window.plugins.socialsharing.share("Hey! My new favorite song is " + item.name + ", check it out!",
          'Check this out', item.album.images[2].url, item.preview_url,
          function() {
            console.log("Share Success")
          },
          function(error) {
            console.log("Share fail: " + error)
          });
      } else window.f7.alert("Share plugin not found");
    }
  }
}
</script>
