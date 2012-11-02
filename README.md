# LessWatcher 

Command-line / shell script to watch a project's LESS and CSS directories for changes to .less files, and to trigger lessc compilation to .css in the CSS directory. 

## Rationale (Opinionated)

At Care.com we manage less files in two places:
  /less = for .less files designed for @import only, e.g. libs like twitter-bootstrap
  /css = for "primary" .less files that compile directly to .css

This script watches the filesystem for changes to .less files in both places, then compiles just the css directory's .less files. (This way there aren't tons of unused .css files generated = avoids litter and confusion.) The generated .css files are checked in to source control, and they can be referenced directly in markup or app config just like any other .css file. The generated .css files should never be edited by hand of course.

This script has been tested on OSX Lion and Windows 7.

## Installation

1. Install latest node (e.g. 0.8.11) and npm (e.g. 1.1.62)
  (If on Windows, use the official nodejs.org/download/ MSI installer)

2. Edit your $PATH env var:
  Add the npm/bin directory to your $PATH
  (Its location depends on your system, might be e.g. /usr/local/share/npm/bin)

3. Add a new $NODE_PATH env var:
  Add the npm/lib/node_modules directory to it
  (npm/lib is a peer of npm/bin, it's where node's global modules are installed)

4. Install lesswatcher globally, e.g.:
$ npm install -g lesswatcher

5. See if it worked! Just type:
$ lesswatcher
LessWatcher module v 0.0.9 activated... (etc)

6. If you need to specify alternate values for the less and css dirs to watch, you can pass them to lesswatcher when you invoke it, e.g.:
$ lesswatcher -l /my/project/custom/less -c /my/project/css

7. Optional compression and minification are supported via -o=yui (calls lessc with "-yui-compress" flag)

8. That's it! Now, editing .less files will trigger lessc on all less files under your CSS_DIR's directory (with console logging in the terminal window).


## TODO - Possible future features

1. support watching for newly created files without restart

2. support config.json file (w/ configurable location via arg) for project-specific settings

3. show lessc errors instead of exiting
