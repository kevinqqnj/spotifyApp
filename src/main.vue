<template>
  <!-- App -->
  <div id="app">
    <f7-views>
      <!-- Main view-->
      <f7-view main :dynamicNavbar="true">
        <!-- Top Navigation Bar-->
        <f7-navbar>
          <f7-nav-left>
            <f7-link icon="icon-bars" open-panel="left"></f7-link>
          </f7-nav-left>
          <f7-nav-center>Spotify Browser</f7-nav-center>
        </f7-navbar>
        <!-- Pages -->
        <f7-pages navbar-through toolbar-through>
          <!-- Page, data-page contains page name-->
          <f7-page name="index">
            <!-- Scrollable page content-->
            <f7-block-title>Criteria</f7-block-title>
            <f7-list form>
              <f7-list-item media="<i class='icon fa fa-music'></i>">
                <f7-label>Songs</f7-label>
                <f7-input type="text" placeholder="Search for..." v-model="term" />
              </f7-list-item>
              <f7-list-item media="<i class='icon fa fa-list-ol'></i>">
                <f7-label>Max Results</f7-label>
                <f7-input type="range" id="numResults" min="0" max="50" step="1" v-model="sliderVal" />
                <span>&nbsp;&nbsp;</span>
                <f7-input type="text" id="sliderVal" disabled :value="sliderVal" />
              </f7-list-item>
            </f7-list>
            <f7-block>
              <div class="row">
                <div class="col-100">
                  <f7-button id="btnSearch" class="button button-big button-fill color-green" @click="onSubmit">Submit</f7-button>
                </div>
              </div>
            </f7-block>
          </f7-page>
        </f7-pages>
        <!-- Bottom Toolbar on every view unless no-toolbar class specified (see item template)-->
        <f7-toolbar>
          <f7-link href="http://www.spotify.com" class="link external">
            <i class="icon icon-spotify"></i>
            <p class="color-white">&nbsp;Spotify</p>
          </f7-link>
          <f7-link href="http://www.idangero.us/framework7" class="link external">
            <i class="icon icon-f7"></i>
          </f7-link>
        </f7-toolbar>
      </f7-view>
    </f7-views>
  </div>
</template>
<script>
import store from './store.js';
export default {
  name: 'Index',
  data() {
    return {
      sliderVal: 20,
      term: '',
    }
  },
  created() {

  },
  mounted() {
    window.Dom7(document).on('deviceready', () => {
      console.log("Device is ready!");
    });
  },
  computed: {

  },
  methods: {
    onSubmit() {
      if (this.term.length == 0) {
        window.f7.alert("请输入搜索内容");
      } else {
        var mediaType = "track";
        var url = "https://api.spotify.com/v1/search?q=" + this.term + "&type=" + mediaType + "&limit=" + this.sliderVal;;
        window.Dom7.ajax({
          dataType: 'json',
          url: url,
          success: function(resp) {
            // window.f7.alert("Number of results " + resp.tracks.items.length);
            console.log(resp.tracks.items);
            store.searchTracks = resp.tracks.items;
            window.f7.mainView.router.load({
              url: '/list/',
              context: resp.tracks.items
         });
          },
          error: function(xhr) {
            console.log("Error on ajax call " + xhr);
          }
        });
      }
    }
  }
}
</script>
