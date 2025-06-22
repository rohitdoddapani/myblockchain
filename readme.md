# Simple Go Blockchain

This project is a minimal blockchain implementation in Go. It demonstrates the core concepts of blockchains, such as block creation, hashing, and chain validation, using a simple HTTP API.

> Want to see the networking version?  
> 👉 [Check out the `networking` branch here.](https://github.com/rohitdoddapani/myblockchain/tree/networking)

## Features

- **Block Structure:** Each block contains an index, timestamp, BPM (beats per minute, as example data), hash, and previous hash.
- **Hashing:** Blocks are linked using SHA-256 hashes.
- **Validation:** New blocks are validated before being added to the chain.
- **REST API:** 
  - `GET /` returns the current blockchain.
  - `POST /` adds a new block with a given BPM value.

## Getting Started

### Prerequisites

- Go 1.16+ installed
- [Gorilla Mux](https://github.com/gorilla/mux)
- [go-spew](https://github.com/davecgh/go-spew)
- [godotenv](https://github.com/joho/godotenv)

Install dependencies:
```sh
go get github.com/gorilla/mux
go get github.com/davecgh/go-spew/spew
go get github.com/joho/godotenv
```

### Setup

1. **Clone the repository:**
   ```sh
   git clone <repo-url>
   cd <repo-directory>
   ```

2. **Create a `.env` file** in the project root with:
   ```
   PORT=8080
   ```

3. **Run the application:**
   ```sh
   go run blockchain.go
   ```

## Usage

### Get the Blockchain

```sh
curl http://localhost:8080/
```

### Add a Block

```sh
curl -X POST -H "Content-Type: application/json" -d '{"BPM": 72}' http://localhost:8080/
```

## How It Works

- The blockchain is a slice of `Block` structs.
- Each block’s hash is calculated from its contents and the previous block’s hash.
- The server starts with a genesis block.
- New blocks are added via POST requests and validated before being appended.

## Notes

- This is a demonstration and **not suitable for production**.
- There is no peer-to-peer networking or consensus algorithm.
- The blockchain is stored in memory and will reset on restart.


> Want to see the networking version?  
> 👉 [Check out the `networking` branch here.](https://github.com/rohitdoddapani/myblockchain/tree/networking)