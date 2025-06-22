# Simple Go Blockchain with Networking

This project is a minimal blockchain implementation in Go, now enhanced with basic networking. It demonstrates the core concepts of blockchains—block creation, hashing, and chain validation—while allowing multiple clients to connect and interact with the blockchain over TCP.

> Looking for the basic blockchain without networking?  
> 👉 [Check out the `basic` branch here.](https://github.com/rohitdoddapani/myblockchain/tree/main)


## Features

- **Block Structure:** Each block contains an index, timestamp, BPM (beats per minute, as example data), hash, and previous hash.
- **Hashing:** Blocks are linked using SHA-256 hashes.
- **Validation:** New blocks are validated before being added to the chain.
- **Networking:**  
  - Runs a TCP server (port configurable via `.env`).
  - Multiple clients can connect and submit new BPM values.
  - Blockchain state is periodically broadcast to all connected clients.
- **Chain Replacement:** The blockchain is replaced if a longer valid chain is received.

## Getting Started

### Prerequisites

- Go 1.16+ installed
- [go-spew](https://github.com/davecgh/go-spew)
- [godotenv](https://github.com/joho/godotenv)

Install dependencies:
```sh
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
   go run networking.go
   ```

## Usage

### Connect as a Client

You can use `nc` (netcat) or `telnet` to connect to the blockchain server:

```sh
nc localhost 8080
```
or
```sh
telnet localhost 8080
```

- After connecting, you will be prompted to enter a BPM value.
- Enter an integer and press Enter to submit a new block.
- The blockchain will be periodically broadcast to your terminal in JSON format.

### Example Session

```
Enter a new BPM:72

Enter a new BPM:80

[...blockchain JSON output every 30 seconds...]
```

## How It Works

- The blockchain is a slice of `Block` structs.
- Each block’s hash is calculated from its contents and the previous block’s hash.
- The server starts with a genesis block.
- New blocks are added by clients submitting BPM values over TCP.
- The blockchain is periodically sent to all connected clients.

## Notes

- This is a demonstration and **not suitable for production**.
- There is no peer-to-peer networking or consensus algorithm.
- The blockchain is stored in memory and will reset on restart.
- All clients share the same blockchain state managed by the server.
