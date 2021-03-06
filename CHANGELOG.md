# v8.0.0 Hot and Heavy

- Upgraded `hget` to `2.0.0`

# v7.1.9 Wet and Dry

- Added `wet` option that avoids history updates on redirects

# v7.1.8 Acceptance

- Upgraded `accepts` to `1.3.0`

# v7.1.6 Render Carnage

- The client-side implementation now emits a `render.error` event whenever a view fails to render. It includes the following arguments: `err, container, model, route`

# v7.1.5 Toothpick

- Upgraded `gradual` to `1.0.7`

# v7.1.4 Idempotency

- Fixed a bug where the prefetched wouldn't work
- Changed `taunus.xhr` so that it can only make identical requests once every second

# v7.1.2 Lipstick

- Fixed a bug where deferral wouldn't work because the global alias was miscalculated

# v7.1.1 Makeup

- Fixed a bug in the prefetcher logic
- Introduced the ability to filter `DEBUG` message types using `DEBUG.filter('name|name|name')`

# v7.1.0 Garbage Truck

- Added a `taunus.track` method that keeps track of things that should be destroyed when a view or partial view gets removed from the document

# v7.0.0 Gradual

- Now using `crossvent` for event handling
- Incorporated `gradual` into Taunus core
- It can be accessed as `taunus.gradual`
- Option to disable `gradual` by setting `forms: false` in the options
- Option to disable link hijacking by setting `links: false` in the options

_<sub>For form submissions to be handled properly, make sure to honor the `as-text` query string, returning a plain text response even if the request asks for JSON</sub>_

# v6.1.8 Aural Emission

- Replaced `contra.emitter` with `contra@1.9.1/emitter`

# v6.1.6 Ancients

- Fixed `console.log` patch in `taunus/browser/debug` which would fail under IE9

# v6.1.5 Omnibox

- Replaced `fast-url-parser` with `omnibox` to broaden browser support

# v6.1.3 Body Double

- `taunus.partial.replace` changes the `container` to the first topmost element after replacement
- `partial(...).on('render', fn)` changed so that `fn` now receives `container` in addition to `html`

# v6.1.2 Pay Per View

- `taunus.partial.replace` now gets rid of the target DOM element entirely, as originally intended

# v6.1.1 Version Eagle

- Exposed a `versionCheck(version, url?)` method on the client-side that will redirect to `url` (or refresh the page), if there's a version mismatch. Returns `true` if the check passes
- Exposed a `state` object on the server-side containing the `version` that was used to mount Taunus

# v6.0.1 Carbon Emissions

- The `router` event is now properly emitted after a timeout

# v6.0.0 ViewState of the Art

- Partial view templates can now interact with the `route` model property just like master views
- Added `taunus.partial.appendTo`, `taunus.partial.beforeOf`, and `taunus.partial.replace` methods to complement `taunus.partial`
- Added `dry` option to `taunus.go`, which only updates the URL and relevant state components
- Added a `router(route)` event whenever the history route changes through Taunus

# v5.4.7 Literally

- Added an optional `as-text` query parameter for Taunus view responses to return JSON responses as plain-text HTML

# v5.4.6 Trailer Park

- `taunus.resolve` no longer returns routes with trailing slashes if they have a missing optional parameter

# v5.4.4 Lopsided Landslide

- All deferred templates and controllers are stored in memory, sorted by version

# v5.4.3 Two Bedroom Apartment

- Fixed an issue where versioning mismatches wouldn't refresh the page

# v5.4.2 Likable Links

- Taunus now ignores anchor tags with a `download` attribute
- Taunus now ignores anchor tags with `target='_blank'`
- Taunus now ignores anchor tags with a `data-taunus-ignore` attribute

# v5.3.4 Sans Lyrics

- Introduced ability to call `taunus.xhr` with `(options, done)` in addition to `(url, done)` and `(url, options, done)`

# v5.3.2 Gas Leak

- Added ability for redirects to be forced even if redirecting to the same URL

# v5.3.1 Gas Leak

- Fixed a bug where views wouldn't emit an event asynchronously if the view could be rendered immediately

# v5.3.0 Shale Gas

- Introduced a view-level event emitter. You can now do `taunus.partial(div, 'tags', ['a', 'b']).on('render', fn)` and `fn` will be eventually invoked when the partial is rendered. Useful for situations where a partial view may be rendered asynchronously because it was deferred.

# v5.2.0 Medal of Honor

- Exposed `taunus.redirect` method on the client-side

# v5.1.1 Casual Tuesday

- `taunus.xhr` now allows you to issue requests with content other than JSON _(e.g `multipart/form-data`)_ and still get a JSON response back

# v5.1.0 Twisted Transistor

- `taunus.redirect` now takes an `options` object, where you can set a `hard` option. If it's set to `true`, AJAX redirects will be followed using `location.href = url` rather than `taunus.navigate(url)`

# v5.0.0 Package Router

##### Views

- Exposed `route` information directly on view models, for convenience.
  - Most useful for accessing `route.query` parameters
  - Has `toJSON` no-op so that it doesn't bloat the model itself after use on templates

##### `.route(url?)`

- Removed `parts` from the result
- Introduced `hash` as a string containing the `#hash` part of a URL (equivalent of `parts.hash`, except it's `''` if empty)
- Introduced `path` (equivalent of `parts.path`)
- Introduced `pathname` (equivalent of `parts.pathname`)
- Introduced `search` (equivalent of `parts.search`)
- Introduced `query` as an equivalent of `parts.query`. Parsed according to input values:
  - `''` and `'true'` are converted to `true`
  - `'false'` is converted to `false`
  - `'123'`, `'-123'`, and `'+123'` are all converted to base-10 integers
  - Anything else stays a string

##### `.route.equals(a?, b?)`

- Faster and simpler, now compares on `route.path` _(ignoring hashes as usual)_

# v4.1.8 Deferred Globalization

- `require('taunus')` is automatically transformed into `require('taunus/global')` in deferred modules

# v4.1.7 Intense Database Bickering

- Fixed an issue in the underlying IndexedDB caching layer where it would throw on WebKit-based devices _(Safari, Chrome for iOS, etc)_

# v4.1.6 Hashcow

- Hash navigation no longer triggers a Taunus activation. Navigating from `/foo` to `/foo#bar` has no effect, while navigating from /foo#bar to `/baz#bar` still triggers an activation

# v4.1.5 Clown Clone

- The `taunus` API that's available in view templates will no longer leave a trace in the view model
- Partial templates can no longer modify the view model, and they have access to a cloned copy instead

# v4.1.3 Set Sail

- If loading a server-side controller results in an error other than `'MODULE_NOT_FOUND'`, the error is now thrown

# v4.1.1 Imperverance

- Exposed `version` property on client-side API
- Fixed an issue where routes with the same path but different query part would be considered identical

# v4.1.0 Transaction Reversal

- Removed `startIndex` parameter to Router API introduced in `4.0.0`

# v4.0.0 Roomba Loompa

- Navigating to the same route over and over no longer pushes new history states, uses `replaceState` instead
- Added `startIndex` parameter to Router API
- Taunus notices redirects and renders the appropriate view
- Introduced `taunus.redirect` API on the server-side

# v3.3.1 ER

- Fixes a bug caused by `v3.3.0`

# v3.3.0 Hack Journalism

- Internal `taunus.render` method _(consumed by `taunus-express` and `taunus-hapi`)_ changed signature. Upgrade to `taunus-express@1.2.0` or `taunus-hapi@1.4.0`.

# v3.2.5 Ruta 3

- Fix a bug on the client-side where you couldn't have multiple routes with the same route pattern
- Internal: Replaced `routes` with `ruta3` for flexibility and convenience

# v3.2.4 Test Run

- Fix failing test in `taunus.resolve` where optional parameters would be enforced

# v3.2.3 Major Resolve

- Fixed an issue where `taunus.resolve` would replace named regular expression parameters such as `:hash(d+)` and keep the regular expression part, resulting in `/hashes/5499cf5f(d+)` instead of  `/hashes/5499cf5f`

# v3.2.1 Optional Options

- Fixed an issue where `taunus.resolve` would replace falsy values with empty strings

# v3.2.0 Routing Solution

- Introduced `taunus.resolve(action, data)` method to resolve routes without manually constructing them, on both client-side and server-side

# v3.1.4 Action Figure

- Layout gets access to rendered `action` _(partials can always use JavaScript!)_

# v3.1.3 Spring Cleaning

- Removed `uglifyify` dependency
- Removed duplicate `uglify-js` dependency

# v3.1.2 Bumper Sticker

- Bumped `hget` to `1.1.0`

# v3.1.0 Prefetch Party

- Public `taunus.prefetch(url, element)` API exposed

# v3.0.2 Mirror Entity

- ETag is now computed out of the HTML (or text) and not just the model in non-JSON responses

# v3.0.1 Contractual Terms

- Added dependency on `contra`

# v3.0.0 Deferred Execution

- Taunus exposes itself as a global to simplify script deferral
- Introduced `taunus/browser/debug` and `taunus/global` alternative entry points
- Introduced deferred loading for view templates and view controllers
- Added `--defer` flag to the CLI
- Added `deferMinified` option to `taunus.mount` to minify deferred bundles
- Changed `taunus.route()`, now exposes query string as an object in `route.parts`
- Created `'change'` event, emitted whenever a view navigation occurs
- Created `taunus.state.clear()` method to clear the cache
- Renamed `--standalone` to `--bundle` in the CLI
- Created `getPartial` option for `taunus.mount` on the server-side

# v2.10.4 Version Tracker

- Fixed an issue where Taunus version-tracking was updating the wrong file

# v2.10.3 Cache Buster

- Reduced maximum interceptor latency to `50ms`, from previous `200ms` maximum
- Force directory creation when using the `taunus` CLI

# v2.10.2 Event Planner

- Improved consistency across event handler arguments

# v2.10.1 Consistent Baker

- Routes baked by the CLI are an array similar to the server-side routes created by the consumer, avoiding confusion

# v2.9.3 Exposed Request

- Exposed an `.xhr(url, options?, done)` method on the client-side Taunus API

# v2.9.2 Hash Awareness

- When navigating to a hashed route on a different view, the scroll position will be properly updated

# v2.9.1 Version Awareness

- Introduced versioning API, Taunus now has the ability to work through application version changes

# v2.8.6 Window Breaker

- Fixed an issue where the Taunus CLI would generate invalid CommonJS wiring modules

# v2.8.4 Scroll Acrobat

- Introduced `scroll` option for `taunus.navigate`, allowing the consumer to control whether scroll position should be modified
- Use `document.documentElement` as the default scroll target

# v2.8.0 Posted Bail

- Created `router.equals(route, route)` method
- Router now works even when passed partial routes such as `'#foo'` or `''`, using `location.href` as reference
- `taunus.navigate` won't fetch the model for a route that has the same parameters as the last route
- A `force` option on `taunus.navigate` can be used to request a model anyways
- A `strict` option on `taunus.navigate` can be used to ignore unmatched URLs
- `taunus.state` now exposes the current `route` alongside its model
- Fixed a bug where the caching layer would never pull cached results for hashed routes

# v2.7.2 Caching Miracles

- The `ETag` is now calculated using the full `viewModel`, and not just the `partial` view model

# v2.7.0 Treasure Cache

- Routes now properly override caching on an individual basis
- CLI flag `--replacements` renamed `--resolvers` for consistency
- Shortened resolver names for simplicity and to mitigate confusion
  - `getViewTemplatePath` is now `getView`
  - `getViewControllerPath` is now `getClientController`
  - `getControllerActionPath` is now `getServerController`
- On the client-side, throw if `bootstrap` is unsupported when `taunus.mount` is called
- If `taunus.navigate` is called with an URL that doesn't match any route, then the user will be redirected via `location.href`
- Added `canPreventDefault` property to interceptor `event` parameters

# v2.6.0 Event Bar

- Client-side controller signature changed to `controller(model, container, route)`

# v2.5.0 Public Speaking

- Renamed public `hget` option into `plaintext`
- Fixed link behavior where hash navigation _(as in `/foo#comments`)_ would trigger unnecessary AJAX requests
- Introduced simpler `manual` bootstrap option

# v2.4.1 Nitpick

- Added additional safe-guards against failed IndexedDB bootstrapping
- Fixed a bug when resolving relative paths in the Taunus CLI
- Fixed a bug when omitting the `options` object when invoking `taunus.mount` in the client-side
- `document.title` only changes if it's defined in the model
- The `container` object passed to `taunus.mount` on the client-side must be a DOM element

# v2.4.0 Bootstrap Overload

- Removed `manual` bootstrap option
- Introduced automatic bootstrap that fetches the model for you
- Reinstated inline bootstrap that expects model to be inline in a `<script type='text/taunus'>` tag
- Reduced maximum caching latency to `200ms` from `500ms`

# v2.3.0 Clickety Click

- Got rid of `localStorage` cache, relying solely on memory and IndexedDB cache stores
- Introduced link prefetching on `mouseover` and `touchstart` for anchor links with valid Taunus routes
- Default cache half-life set to `30` seconds
- Simplified interface to `'fetcher.*'` events

# v2.2.1 Back-End Portability

- Introduced ability to use different backends through `taunus-express` or `taunus-hapi`
- CLI arguments now have proper shorthand one-character aliases
- CLI supports transforming routes, e.g using `hapiify` to transform Hapi routes into something the client-side Taunus router understands
- Reasonable defaults using a dedicated `.bin` directory

# v2.0.0 Carrier Interceptor

- Interceptors are now event-drived
- Introduced blind-caching engine based on interceptors, disabled by default

# v1.8.3 Evented XHR

- Introduced more XHR-tracking events

# v1.8.2 Defer All The Things

- Model is now expected to load asynchronously via `taunusReady` global
- Introduced `jsonp` support
- Reduced amount of data transferred over JSON

# v1.7.6 Refund

- Requesting a new page provokes Taunus to `.abort` the request currently being made

# v1.7.5 Dependency Hoarder

- Removed dependency on `lodash.unescape`

# v1.7.3 Cache Driver

- A `max-age=0` header prevents stale content from never being refreshed

# v1.7.2 Cache Driver

- Changed `max-age` to only 1 hour

# v1.7.1 Slave Driver

- Add ability to rebuild default view model at a later point in time

# v1.6.21 Early Bird

Wait for `defaults` to become available before serving any responses

# v1.6.20 Negotiator

- Use `accepts` for content negotiation

# v1.6.19 Hollow Point

- Fixed an issue when navigating to hashes

# v1.6.8 Cat Food

- Fixed an issue with links being reloaded
- Fixed an issue when navigating backwards

# v1.6.4 Crash Course

- Changed caching model to `private, must-revalidate`, and set `max-age` to a day

# v1.6.3 Golf Cart

- Default view model no longer request-based, more memory efficient

# v1.5.1 Cache Negotiation

- Use a different URL when hijacking AJAX requests so that browsers properly cache JSON vs HTML

# v1.5.0 Cache Machine

- Introduced server-side view caching, setting `ETag`, `Vary`, and `cache-control` HTTP headers

# v1.4.10 Ancient Browsing

- Fix a bug where old browsers would change the `location.href` and execute AJAX code afterwards
- Fix a bug where `ignore` wouldn't be propagated by the CLI to client-side routes

# v1.4.8 Hollow Point

- Anchor links containing `<span>` or any other child elements that may be event targets now get hijacked as well

# v1.4.7 Sleepy Hollow

- Print the stack trace of captured template rendering errors

# v1.4.6 Skeptic Magician

- Fix a bug in browsers without history API
- Prevent `.mount` to be called more than once in the client-side
- Friendly error message if view rendering fails

# v1.4.5 Shy Shoulder

- Fix a bug where links wouldn't be ajax-enhanced

# v1.4.4 Sankara Stones

- Introduced `skip` to skip over view routes in certain situations

# v1.4.3 Dividing Line

- Added `ignore` option to allow routes that go straight to the server

# v1.4.2 Fancy Treat

- Introduced ability to set response status code in model

# v1.4.0 Responsive Design

- Implemented public API method that allows generating a response using the Taunus API

# v1.3.0 Ion Drive

- Browser support when `history` API is missing

# v1.2.2 Switcheroo

- Moved around arguments for `'error'` event

# v1.1.1 Silent Killer

- Event emitter no longer throws on errors

# v1.1.0 Renderist

- Renders views using `function(model)` on the server-side as well

# v1.0.6 Anchor Fighters

- Play nice on links with `href='#...'`

# v1.0.3 Rafael

- Fixed a missing reference to `raf`

# v1.0.2 Broken Promises

- Taunus now expects `data-taunus` attributes to match a `<script>` tag containing the view model

# v0.5.5 Backwards Compatibility

- Navigating through history properly triggers the corresponding scroll towards the route hash, or the top of the document

# v0.5.4 Logic Route

- Improved routing logic so that it remembers `search` and `hash` parts of a URL, while these won't factor into routing itself

# v0.5.3 Model of the State

- `taunus.state.model` now exposes the current view's model

# v0.5.2 Wary Goblin

- Introduced middleware option to modify base view model on a request basis

# v0.5.1 State of the Art

- Publish `state` on public API

# v0.4.5 Honorary Title

- Fix a bug when navigating backwards where the `document.title` wouldn't be updated

# v0.4.4 Brokeback Mountain

- Fix a bug when navigating backwards to a view that re-routed the action through `model.action`

# v0.4.3 User Matters

- `req.user` is automatically copied into `model.user`

# v0.4.2 Foo Fighters

- Relative paths for convenience

# v0.4.1 Action Figure

- Ability to change the default action through a property in the model

# v0.4.0 High Seas

- Introduced public API method `.navigate(url)`

# v0.3.6 Route 66

- Added an optional `route` parameter for internal use

# v0.3.5 Contextual Tasting

- Fixed a bug where the initial `start` and `render` events would broadcast the wrong context

# v0.3.3 Logical Perplexion

- Fixed navigation when clicking links that don't match a route

# v0.3.2 Steady Navigation

- Fixed navigation when clicking links

# v0.3.1 Boob Flash

- `res.viewModel.action` allows you to change the view to be rendered
- If the request has a `.flash` method, then it'll get consumed when generating a response

# v0.3.0 Exposed Parts

- Expose partials on the core API in the client-side

# v0.1.10 Lock Picking

- Use `'` intead of `"` in auto-generated wiring

# v0.1.9 Word Smith

- Reworded standalone CLI usage

# v0.1.8 Bug Crusher

Fixes

- Fixed an issue with controllers not running on the client-side

# v0.1.7 Enviroment Activism

- Separated concerns in routing, templating, and controllers in the client-side

# v0.1.6 XML Vulnerability

- Added ability to intercept model requests and return a cached response before they server is queried

# v0.1.5 Packaging

- `.taunusrc` options can also be configured in `package.json`, as the `taunus` property

# v0.1.4 Emancipation

- `taunus --standalone taunus.js` eliminates dependency on Common.JS and Browserify

# v0.1.3 Spare Change

Fixes

- Fixed an issue when clicking on links

# v0.1.2 Town Car

- Turned into an event emitter
- Link click route-checking is delegated from `document.body`
- Implemented replaceable module path resolvers for customization

# v0.1.1 Saucy Studio

- Fixed a CLI issue forming paths on Windows

# v0.1.0 Fiery Pony

- Initial Public Release
