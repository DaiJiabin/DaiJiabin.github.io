# NodeJS


# Lecture 1

## What is NodeJS?

- Node.js is a __JavaScript runtime__ built on Chrome's V8

- Node.js uses an __event-driven, non-blocking I/O__ model

  - __Blocking:__ When I/O processing, process waits until I/O finishes.
  
  - __Non-blocking:__ When I/o processing, process doesn't wait.

  - __Event-driven:__ i.g., Click event.

## Advantages of NodeJS

- Deals well with High Concurrency and I/O intensiv

## CPU Intensiv vs. I/O Intensiv

- CPU Intensiv: compress, decompress, encrpt, descrypt

- I/O Intensiv: Operations on File, Network and Database, which are offen used by Web ( Reading Static Resources, Operate Database, Render).

## How to deal with High Concurrency

- Increase Servers

- Increase the numbers of CPU-Cores

- __And... NodeJS deals well with high Concurrency and I/O intensiv.__

## NodeJS working Model

![Model](/NodeJS%20Model.jpg)

# Lecture 2

## CommonJS, global and process

- CommonJS:
  
  - Each file is a module, and has its own field.
  
  - Inner the module, the parameter "module" represents module itself.
  
  - Module.exports represents the API of module.
  
    ```modules.exports.<Variable/Function> = <Rename>```

- Rules of _require()_

  - support extensions of js, json and node.

  - Without path build-in Module or other third modules in __node_modules__ will be used.

- Characters of _require()_

  - In the 1st load module will be executed, and then stores in cache.
  
  - When a module loaded repeatly, output the executed part only, instead of the unexecuted part.

  ```
  module.exports.test = 'A';

  const modB = require('./05_modB');
  console.log('modA: ', modB.test);

  module.exports.test = 'AA';
  ```

  ```
  module.exports.test = 'B';

  const modA = require('./05_modA');
  console.log('modB: ', modA.test);

  module.exports.test = 'BB';
  ```
