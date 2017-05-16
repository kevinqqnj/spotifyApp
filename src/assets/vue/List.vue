<template>
  <f7-page name="list" id="list">
    <f7-navbar>
      <f7-nav-left back-link="Back" sliding></f7-nav-left>
      <f7-nav-center sliding>Results</f7-nav-center>
      <f7-nav-right>
        <f7-link icon="icon-bars" open-panel=""></f7-link>
      </f7-nav-right>
    </f7-navbar>
    <!-- Search bar -->
    <f7-searchbar cancel-link="Cancel" search-list="#mediaList" placeholder="Search in items" :clear-button="true">
    </f7-searchbar>
    <!-- Will be visible if there is no any results found, defined by "searchbar-not-found" class -->
    <f7-list class="searchbar-not-found">
      <f7-list-item title="Nothing found"></f7-list-item>
    </f7-list>
    <!-- Search-through list -->
    <f7-list class="searchbar-found" media-list id="mediaList">
      <f7-list-item swipeout v-for="(item, index) in searchTracks" :key="item.id" :link="'/media/'+index+'/'" :media="'<img data-src=' + item.album.images[2].url +' width=64px class=lazy>'" :title="item.name" :subtitle="'<span class=singerPrex>by </span>'+item.artists[0].name" :text="item.album.name">
        <f7-swipeout-actions right>
          <f7-swipeout-button class="bg-orange">
            <a class="bg-orange favorite" @click="addFavorite(index)"><i class="icon fa fa-star fa-2x"></i></a>
          </f7-swipeout-button>
          <f7-swipeout-button class="bg-blue">
            <a href="#" class="bg-blue share" @click="share(index)"><i class="icon fa fa-share fa-2x"></i></a>
          </f7-swipeout-button>
        </f7-swipeout-actions>
        <f7-swipeout-actions left>
          <f7-swipeout-button class="bg-green">
            <a href="#" class="bg-green preview" @click="preview(index)"><i class="icon fa fa-play fa-2x"></i></a>
          </f7-swipeout-button>
        </f7-swipeout-actions>
      </f7-list-item>
    </f7-list>
  </f7-page>
</template>
<script>
import store from '../../store.js'
export default {
  name: 'list',
  data() {
    return {
      searchTracks: [],
      favoriteList: [],
    }
  },
  mounted() {
    window.Dom7(document).on('deviceready', () => {
      console.log("List Page is ready!");
      this.searchTracks = store.searchTracks;
      this.favoriteList = store.favoriteList;
    });
  },
  methods: {
    addFavorite(index) {
      store.favoriteList.push(this.searchTracks[index]);
      window.f7.alert(this.searchTracks[index].name + ' added to favorites!');
    },
    preview(index) {
      var item = this.searchTracks[index];
      window.f7.alert("Previewing " + item.name);
      var media = new Media(item.preview_url, function() {
        console.log("Media Success");
      }, function(error) {
        console.log("Media fail " + error)
      }, null);
      media.play();
      setTimeout(function() {
          media.stop()
        }, 7000) //preview for 7 seconds
    },
    share(index) {
      var item = this.searchTracks[index];
      console.log(item);
      if (window.plugins && window.plugins.socialsharing) {
        window.plugins.socialsharing.share("Hey! My new favorite song is " + item.name + " check it out!",
          'Check this out', item.album.images[2].url, item.preview_url,
          function() {
            console.log("Share Success")
          },
          function(error) {
            console.log("Share fail " + error)
          });
      } else window.f7.alert("Share plugin not found");
    }
  }
}
</script>
