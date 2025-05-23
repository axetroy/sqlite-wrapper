# sqlite-wrapper.js

[![Badge](https://img.shields.io/badge/link-996.icu-%23FF4D5B.svg?style=flat-square)](https://996.icu/#/en_US)
[![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg?style=flat-square)](https://github.com/996icu/996.ICU/blob/master/LICENSE)
![Node](https://img.shields.io/badge/node-%3E=14-blue.svg?style=flat-square)
[![npm version](https://badge.fury.io/js/sqlite-wrapper.js.svg)](https://badge.fury.io/js/sqlite-wrapper.js)

A wrapper for SQLite3 with a focus on simplicity and ease of use.

It uses the SQLite3 executable file for database operations and it's zero-dependencies.

## Installation

```bash
npm install sqlite-wrapper.js --save
```

## Usage

```js
import { SQLiteWrapper } from "sqlite-wrapper.js";

// Initialize the sqlite process
const sqlite = new SQLiteWrapper("/path/to/sqlite3", { dbPath: "/path/to/database.db" });

// Create a table
await sqlite.exec("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)");
// Insert data
await sqlite.exec("INSERT INTO users (name) VALUES (?)", ["Alice"]);
await sqlite.exec("INSERT INTO users (name) VALUES (?)", ["Bob"]);

// Query data
const result = await sqlite.query("SELECT * FROM users");
console.log(result); // Output: [ { id: 1, name: 'Alice' }, { id: 2, name: 'Bob' } ]

// Update data
await sqlite.exec("UPDATE users SET name = ? WHERE id = ?", ["Charlie", 1]);
const results = await sqlite.query("SELECT * FROM users WHERE id = ?", [1]);
console.log(results); // Output: [ { id: 1, name: 'Charlie' } ]

await sqlite.close(); // Close the SQLite3 process
```

## License

The [Anti 996 License](LICENSE)
