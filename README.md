# FlowStorm Debugger with Babashka Script

Just following the info
[here](https://flow-storm.github.io/flow-storm-debugger/user_guide.html#_babashka).

## Prerequisites

* Appropriate JVM bits (JDK >= 17 better, but 11 might be made to work too?)
* Clojure tools
* Babashka

## Steps

* Get Babashka script

    ```
    wget https://raw.githubusercontent.com/babashka/babashka/master/examples/htmx_todoapp.clj
    ```

* Generate `deps.edn`

    ```
    bb print-deps > deps.edn
    ```

* Edit `deps.edn`
  1. Add the `:aliases {,,,}` entry (see url above) to the top-level map
  2. Replace first "RELEASE" with "1.12.0-2"
  3. Replace second "RELEASE" with "4.0.2"
    Version strings obtained via: https://github.com/flow-storm/flow-storm-debugger#artifacts - may need to tweak in the future
  4. May need to add following to `:deps`:

    ```clojure
    ;; depending on jvm version may be needed
    org.openjfx/javafx-controls {:mvn/version "19.0.2"}
    org.openjfx/javafx-base     {:mvn/version "19.0.2"}
    org.openjfx/javafx-graphics {:mvn/version "19.0.2"}
    org.openjfx/javafx-web      {:mvn/version "19.0.2"}
    ```

* Edit `htmx_todoapp.clj`
  * Disable the wrapping `(when ...)` at the end, i.e. make sure the
    "inside" code is active.

* Start Clojure cli

    ```
    clj -A:dev
    ```

* Start debugger via repl prompt by typing `:dbg` followed by enter key

    ```
    user=> :dbg
    ```

* In FlowStorm debugger gui, View -> Toggle theme to get dark mode (or ctrl-t)

* Start the Babashka script via the repl prompt

    ```
    user=> (load-file "./htmx_todoapp.clj")
    ```

* Visit http://localhost:3000/ in web browser for interacting with app

* See tutorial in FlowStorm debugger gui's help menu

