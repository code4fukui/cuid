# cuid2

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

Secure, collision-resistant ids optimized for horizontal scaling and performance. Next generation UUIDs.

## Features

-   **Secure:** It's not feasible to guess the next id. Cuid2 uses multiple, independent entropy sources and hashes them with a security-audited, NIST-standard cryptographically secure hashing algorithm (SHA3-512).
-   **Collision-Resistant:** It's extremely unlikely to generate the same ID twice. You would need to generate roughly 4 quadrillion (4 x 10¹⁸) IDs to have a 50% chance of a single collision.
-   **Horizontally Scalable:** Generate IDs on multiple machines without coordination.
-   **Offline-Compatible:** Generate IDs without a network connection.
-   **URL and Name-Friendly:** No special characters.
-   **Fast and Convenient:** No async operations, and the library is less than 5k gzipped.

## Installation

```bash
npm install @paralleldrive/cuid2
```

## Usage

```javascript
import { createId } from "@paralleldrive/cuid2";

const id = createId();
// 'tz4a98xxat96iws9zmbrgj3a'
```

## API

### `init(options)`

Customize the ID generation by providing your own random number generator, length, or host fingerprint.

```javascript
import { init } from "@paralleldrive/cuid2";

// Create a custom ID generator
const createId = init({
  // A custom random function returning a value between 0 and 1
  random: Math.random,
  // The length of the id
  length: 10,
  // A custom fingerprint for the host environment
  fingerprint: "a-custom-host-fingerprint",
});

const customId = createId(); // e.g., 'wjfazn7qnd'
```

### `isCuid(id)`

Check if a string is a valid Cuid.

```javascript
import { createId, isCuid } from "@paralleldrive/cuid2";

console.log(
  isCuid(createId()), // true
  isCuid("not a cuid") // false
);
```

## Randomness and Distribution

Cuid2 is designed to produce IDs with a uniform, random distribution. This is critical for security and collision resistance. The included demo application visualizes this property by mapping segments of generated IDs to pixel coordinates on a canvas, resulting in an image that resembles white noise, with no discernible patterns.

## License

MIT License — see [LICENSE](LICENSE).