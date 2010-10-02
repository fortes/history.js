# history.js

history.js provides an implementation of the [HTML5 history API](http://www.whatwg.org/specs/web-apps/current-work/multipage/history.html#the-history-interface): `history.pushState` and `history.replaceState` functions, as well as the `window.onpopstate` event.

Browsers that already support his event (Chrome & Safari, Firefox 4+) use native implementations, which are able to change the page URL without refreshing the page. Older browsers use `location.hash` in order to mimic the official behavior.

1214 bytes minified / 588 bytes gzipped

## Installation

Include the script file in your HTML file:

    <!-- Include JSON if you want to support older browsers -->
    <script type="text/javascript" src="json2.js"></script>
    <script type="text/javascript" src="history-min.js"></script>

## Usage

Same as the official HTML5 API:

    // Switch to the item
    window.history.pushState({ id: 35 }, 'Viewing item #35', '/item/35'});

    // Single handler
    window.onpopstate = function (e) {
      var id = e.state.id;
      load_item(id);
    };
    
    // Multiple listeners using addEventListener
    window.addEventListener("popstate", function callback1(event) {
      var id = e.state.id;
      load_item(id);
    }, true);
    
    window.addEventListener("popstate", function callback2(event) {
      do_something_else(e.state);
      // remove one single listener
      window.removeEventListener("popstate", callback2, true);
    }, true);

Any use allowed in the standard but not supported by this API is considered a bug.

## Supported & Tested Browsers

* Chrome 5+ & Safari 5+ (Native)
* Firefox 4+ (Native)
* Firefox 3.5+
* Chrome 4+
* Safari 4+
* IE8+

## Unsupported / Need to test

* Opera ?
* IE6-7
* Safari 3+ (No persitence)
* Chrome 3+ (No persitence)
* Firefox 2+ (No persitence)

## TODO

* Support IE6&7
  * Use `iframe` for history
  * Use `userData` behavior for persistence
* Support FF2+
  * Use `globalStorage` for persistence
* Chrome < 4
  * Use Gears?
* Fallback for browsers that are unsupported
