# Skycoin Explorer

[![Build Status](https://travis-ci.org/skycoin/skycoin-explorer.svg)](https://travis-ci.org/skycoin/skycoin-explorer)

https://explorer.skycoin.net

## Requirements

```
go>=1.8
node>=v6.9.0
npm>=3.10.10
```

### Go

The server is written in golang.

The golang server returns the static content from `dist/` and proxies a subset of the skycoin node API.

### Angular

As an Angular CLI projects,  Node 6.9.0 or higher, together with NPM 3 are required.

After cloning the project, you will need to run `npm install` to pull in all javascript dependencies.

The angular code is compiled to the `dist/` folder.

## Usage

### Run a skycoin node

```sh
git clone github.com/skycoin/skycoin
cd skycoin
./run.sh
```

### Run the explorer

```sh
make run
```

This must be run from the same directory that contains `dist/`.

The explorer assumes that the skycoin node is running on `localhost:6420` by default.

To point it at a different address:

```sh
SKYCOIN_ADDR=http://127.0.0.1:3333 ./explorer
```

`explorer` can be run in api-only mode, which will expose the JSON API but not serve the static content from `dist/`:

```sh
make run-api
```

## API documentation

HTML documentation:

http://explorer.skycoin.net/api.html

JSON formatted API docs:

http://explorer.skycoin.net/api/docs

## Development

After changing the angular frontend, it should be compiled and committed to the repo.
This is to simplify deployment of the application, and allow users to run it themselves without
installing node and npm then running `npm install` and `npm run build`.

### Compiling the angular frontend

```sh
make build-ng
```

## Deployment

Compile `explorer.go` to a binary:

```sh
make build-go
```

Allow it to bind to port 80 using `setcap`:

```sh
sudo setcap 'cap_net_bind_service=+ep' ./explorer
```

Run it on port 80:

```sh
EXPLORER_HOST=:80 ./explorer
```
