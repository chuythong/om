# Om

A [ClojureScript](http://github.com/clojure/clojurescript) interface
to [Facebook's React](http://facebook.github.io/react/).

Om allows users to represent their UIs simply as
[EDN](http://github.com/edn-format/edn). Because ClojureScript data is
immutable data, Om can always rapidly re-render the UI from the
root. Thus Om UIs are out of the box snapshotable and undoable and
these operations have no implementation complexity and little
overhead.

## Example

```clj
(ns example
  (:require [om.core :as om :include-macros true]
            [om.dom :as dom :include-macros true]))

(defn widget [data]
  (om/component
    (dom/div nil "Hello world!")))

(om/root {} widget js/document.body)
```

An implementation of [TodoMVC](http://todomvc.com) implemented in Om
[exists here](http://github.com/swannodette/todomvc/blob/gh-pages/labs/architecture-examples/om/src/todomvc/app.cljs).

## Documention

There's no commitment yet to an API. Still, the code has fairly
verbose docstrings for the existing functionality.

## HTML Syntax

Om is not opinionated about HTML syntax, third parties can provide the
preferred flavors over the `React.DOM` api. Alternative syntaxes will
be listed here:

* [sablono](http://github.com/r0man/sablono), Hiccup-style

## Using it

Om is pre-alpha software.

Make sure you have [Leiningen](http://leiningen.org/)
installed, then clone the Om repo and install it locally with `lein
install`.

Your `project.clj` should include something like the following:

```clj
(defproject foo "0.1.0-SPAPSHOT"
  ...
  :dependencies [[org.clojure/clojure "1.5.1"]
                 [org.clojure/clojurescript "0.0-2127"]
                 [om "0.1.0-SNAPSHOT"]]
  ...)
```

For local development your
[lein-cljsbuild](http://github.com/emezeske/lein-cljsbuild) settings
should look something like this:

```clj
:cljsbuild { 
  :builds [{:id "dev"
            :source-paths ["src"]
            :compiler {
              :output-to "main.js"
              :output-dir "out"
              :optimizations :none
              :source-map true
              :externs ["react/externs/react.js"]}}]}
```

Your local development markup should include something like the following:

```html
<script src="http://fb.me/react-0.8.0.js"></script>
<script src="out/goog/base.js" type="text/javascript"></script>
<script src="main.js" type="text/javascript"></script>
<script type="text/javascript">goog.require("main.core");</script>
```

For production your [lein-cljsbuild](http://github.com/emezeske/lein-cljsbuild) settings should look something
like this:

```clj
:cljsbuild { 
  :builds [{:id "release"
            :source-paths ["src"]
            :compiler {
              :output-to "main.js"
              :optimizations :advanced
              :pretty-print false
              :preamble ["react/react.min.js"]
              :externs ["react/externs/react.js"]
              :closure-warnings
              {:non-standard-jsdoc :off}}}]}
```

This will generate a single file `main.js`.

## Contributing

No pull requests at this time please.

Om is still in the design phase so enhancements are low
priority. However, bug reports are welcome for the existing
functionality.

For a sense of where Om is going the existing issues give a rough
idea.
