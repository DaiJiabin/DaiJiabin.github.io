# NodeJS


# Week 1

## What is NodeJS?

- Node.js is a __JavaScript runtime__ built on Chrome's V8

- Node.js uses an __event-driven, non-blocking I/O__ model

  - __Blocking:__ When I/O processing, process waits until I/O finishes.
  
  - __Non-blocking:__ When I/o processing, process doesn't wait.

  - __Event-driven:__ i.g., Click event.

## Advantages of NodeJS

- Deals well with High Concurrency and I/O intensiv

### CPU Intensiv vs. I/O Intensiv

- CPU Intensiv: compress, decompress, encrpt, descrypt

- I/O Intensiv: Operations on File, Network and Database, which are offen used by Web ( Reading Static Resources, Operate Database, Render).

### How to deal with High Concurrency

- Increase Servers

- Increase the numbers of CPU-Cores
