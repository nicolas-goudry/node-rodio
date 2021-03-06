# node-rodio

[![npm (scoped)](https://img.shields.io/npm/v/@yellowinnovation/node-rodio.svg)](https://www.npmjs.com/package/@yellowinnovation/node-rodio)
[![David](https://img.shields.io/david/YellowInnovation/node-rodio.svg)](https://www.npmjs.com/package/@yellowinnovation/node-rodio)


[Rodio](https://github.com/tomaka/rodio) (Rust audio playback library) bindings for Node.js, built with [Neon](https://www.neon-bindings.com/)

## Installation

`npm install @yellowinnovation/node-rodio`

or

```json
{
    "dependencies": {
        "@yellowinnovation/node-rodio": "0.0.9"
    }
}
```

## Usage

```javascript

const rodio = require('@yellowinnovation/node-rodio');

try {
    console.log(rodio.defaultInputDevice()); // { name: "Your default microphone" ... sample rate, format etc }
    console.log(rodio.defaultOutputDevice()); // { name: "Your default speakers/headphones" ... sample rate, format etc }
    console.log(rodio.devices()); // Lists all devices on the machine
    console.log(rodio.inputDevices()); // Lists all input devices on the machine
    console.log(rodio.outputDevices()); // Lists all output devices on the machine

    const player = new rodio.Player(); // Initializes a new player

    player.append("./samples/music.mp3"); // Loads a file in the queue
    player.append("./samples/beep.wav"); // Another one that will play after the music.mp3
    player.volume(0.5); // Sets volume to 50%; CANNOT BE USED DURING PLAYBACK OR IT WILL THROW, it'll behave fine here though
    // If you'd like to get sounds in parallel, just create another player and make them .play(); at the same time!
    player.play(() => { // Starts playback, expects a callback that is executed when the queue is over
        console.log('done!');
    });
    player.pause(); // Pauses playback
    player.resume(); // Resumes playback
    player.volume(1.0); // Sets the volume to 100%; CANNOT BE USED DURING PLAYBACK OR IT WILL THROW, it will throw here for example
    player.stop(); // Stops playback completely and empties queue.
    // player is not usable at this point since we killed the background thread.
} catch (e) {
    console.error(e); // all functions can throw in case there's a problem with system configuration or you did something wrong
}
```

## License

Licensed under:

* Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)), or
* MIT license ([LICENSE-MIT](LICENSE-MIT) or [http://opensource.org/licenses/MIT](http://opensource.org/licenses/MIT))

## Credits

* Huge props to [@tomaka](https://github.com/tomaka) for his amazing work on [rodio](https://github.com/tomaka/rodio) & [cpal](https://github.com/tomaka/cpal)

## Yellow Innovation

Yellow Innovation is the innovation laboratory of the French postal service: La Poste.

We create innovative user experiences and journeys through services with a focus on IoT lately.

[Yellow Innovation's website and works](http://yellowinnovation.fr/en/)
