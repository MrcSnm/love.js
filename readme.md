Love.js
============

This is [LÖVE](https://love2d.org/) ported to the web using [Emscripten](https://kripken.github.io/emscripten-site/).

It differs from [Motor](https://github.com/rnlf/motor) or [Punchdrunk](https://github.com/TannerRogalsky/punchdrunk) in that it is not a reimplementation but a direct port of the existing LÖVE v0.10.0 code with very few code modifications. As such, it should be at feature parity, as long as the browser it's running in supports a given feature.

## Examples
Here are some live games:

- [Mari0](http://tannerrogalsky.com/mari0/)
- [Friendshape](http://tannerrogalsky.com/friendshape)
- [Mr. Rescue](http://tannerrogalsky.com/mrrescue/)

## Dependencies
- Python 2.7

Python 2.7 will allow you to package your game into a format that Emscripten can read. It will also let you run a simple web server for testing. Python 3.5 is not supported at this time.

## Usage
### Get the code.
1. Clone the repository. `git clone https://github.com/TannerRogalsky/love.js.git`
2. Clone the submodules: `git submodule update --init --recursive`

### Package your game
1. Navigate into the `debug` folder.
2. Package your game.
  - `python ../emscripten/tools/file_packager.py game.data --preload [path-to-game]@/ --js-output=game.js`
  - This should output two files: `game.data` and `game.js` into the `debug` folder.
  - Make sure you include the '@/' after the path to your game source. This will tell the file packager to place your game at the root of Emscripten's file system.
  - Make sure your [path-to-game] does not contain any non ascii characters

### Test it
1. Run a web server.
  - `python -m SimpleHTTPServer 8000` will work.
2. Open `localhost:8000` in the browser of your choice.

### Release it
1. If everything looks good, nagivate to the `release` folder. Package and test your game for release.
2. The `release-compatibility` folder can now be copied to a webserver. A simple static webserver should suffice.

#### Linux Shell Compile
1. Change [path-to-game]@/ to where it is located, it is defaulted on the debug folder
2. The release files is defaulted on release-compatibility, it generates a zip file from the game.data, game.js, love.js, consolewrapper.js and theme for fast server uploading
3. It will automatically starts a simple server in `localhost:8000`

#### Calling JS Functions from .lua files
1. Full documentation and original project about calling JS Functions inside lua on **[Love.js-Api-Player](https://github.com/MrcSnm/Love.js-Api-Player)**
2. It is able to **send** requests and **retrieve** data from the requests

#### Release Types
`release-compatibility` is recommended if the performance it yields is adequate. The difference between `compatibility` and `performance` is that `performance` is compiled with exception catching disabled and memory growth disabled. This means that you will not be able to rely on catching exceptions from C++ in your code and you may need to set `TOTAL_MEMORY` on the `Module` object to indicate how much memory your game will require.

## Issues
Some things, like threads, don't have browser support yet. Please check the project issues for known problems.

## Contributing
Please consider submitting a test. Any functionality that isn't covered in `spec/tests` would be very useful.

The build process for this project is still a very manual process and is not ready to be shared. Feel free to keep an eye on the `emscripten` branch of [my LÖVE fork](https://bitbucket.org/TannerRogalsky/love) if you're really curious.
