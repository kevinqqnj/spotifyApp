<template>
  <div id="list">
    <f7-navbar>
      <f7-nav-left back-link="Back" sliding></f7-nav-left>
      <f7-nav-center sliding>Results</f7-nav-center>
      <f7-nav-right>
        <f7-link icon="icon-bars" open-panel=""></f7-link>
      </f7-nav-right>
    </f7-navbar>
    <f7-page name="list">
      <!-- Search bar -->
      <f7-searchbar cancel-link="Cancel" search-list="#mediaList" placeholder="Search in items" :clear-button="true" >
      </f7-searchbar>
      <!-- Will be visible if there is no any results found, defined by "searchbar-not-found" class -->
      <f7-list class="searchbar-not-found">
        <f7-list-item title="Nothing found"></f7-list-item>
      </f7-list>
      <!-- Search-through list -->
      <f7-list class="searchbar-found" media-list id="mediaList">
        <f7-list-item swipeout v-for="(item, key, index) in searchTracks" :key="item.id" link="#" :media="'<img src=' + item.album.images[2].url +' >'" :title="item.name" :subtitle="item.artists[0].name" :text="item.album.name">
          <f7-swipeout-actions right>
            <f7-swipeout-button>
              <a class="bg-orange favorite" :data-item="index"><i class="icon fa fa-star fa-2x"></i></a>
              <a href="#" class="bg-blue share" :data-item="index"><i class="icon fa fa-share fa-2x"></i></a>
            </f7-swipeout-button>
          </f7-swipeout-actions>
          <f7-swipeout-actions left>
            <f7-swipeout-button>
              <a href="#" class="bg-green preview" :data-item="index"><i class="icon fa fa-play fa-2x"></i></a>
            </f7-swipeout-button>
          </f7-swipeout-actions>
        </f7-list-item>
      </f7-list>
    </f7-page>
  </div>
</template>
<script>
import store from '../../store.js'
export default {
  name: 'list',
  data() {
    return {
      searchTracks: [],
    }
  },
  mounted() {
    window.Dom7(document).on('deviceready', () => {
      console.log("List Page is ready!");
      this.searchTracks = store.searchTracks;
    });
  }
}
</script>
