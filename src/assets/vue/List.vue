 <div class="navbar">
            <div class="navbar-inner">
                <div class="left"><a href="#" class="back link"> <i class="icon icon-back"></i><span>Back</span></a></div>
                <div class="center sliding">Results</div>
                <div class="right">
                    <a href="#" class="link icon-only open-panel"> <i class="icon icon-bars"></i></a>
                </div>
            </div>
        </div>

        <div class="page" data-page="list">
            <form class="searchbar searchbar-init" data-search-list=".list-block-search" data-search-in=".item-title"
                  data-searchbar-found=".searchbar-found" data-searchbar-not-found=".searchbar-not-found">
                <div class="searchbar-input">
                    <input type="search" placeholder="Search">
                    <a href="#" class="searchbar-clear"></a>
                </div>
                <a href="#" class="searchbar-cancel">Cancel</a>
            </form>
            <div class="searchbar-overlay"></div>
            <div class="page-content">
                <!-- no result -->
                <div class="content-block searchbar-not-found">
                    Nothing found
                </div>

                <div id="mediaList" class="list-block media-list list-block-search searchbar-found">
                    <ul>
                        {{#each this}}
                        <li class="swipeout">
                            <div class="swipeout-content">
                                <a href='#' class="item-content item-link">
                                    <div class="item-media">
                                        <img data-src="{{album.images[2].url}}" class="lazy">
                                    </div>
                                    <div class="item-inner">
                                        <div class="item-title-row">
                                            <div class="item-title">{{name}}</div>
                                        </div>
                                        <div class="item-subtitle">{{artists[0].name}}</div>
                                        <div class="item-text">{{album.name}}</div>
                                    </div>
                                </a>
                            </div>
                            <div class="swipeout-actions-right">
                                <a href="#" class="bg-orange favorite" data-item="{{@index}}"><i class="icon fa fa-star fa-2x"></i></a>
                                <a href="#" class="bg-blue share" data-item="{{@index}}"><i class="icon fa fa-share fa-2x"></i></a>
                            </div>
                            <div class="swipeout-actions-left">
                                <a href="#" class="bg-green preview" data-item="{{@index}}"><i class="icon fa fa-play fa-2x"></i></a>
                            </div>
                        </li>
                        {{/each}}
                    </ul>
                </div>
            </div>
        </div>
