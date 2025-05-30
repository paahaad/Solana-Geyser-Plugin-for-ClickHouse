> ⚠️ **Project Moved**  
> This project has been moved to a new home: [https://github.com/torrey-xyz/Solana-Geyser-Plugin-for-ClickHouse](https://github.com/torrey-xyz/Solana-Geyser-Plugin-for-ClickHouse).  
> All future development and maintenance will be handled by **Torrey**.

# Solana Geyser Plugin for ClickHouse
### Prerequisites
- Rust toolchain (latest stable version)
- Docker (for running ClickHouse locally)
- Git
- CMake (for building Solana)

## Set Up Local Solana Development Environment
- Install Solana CLI
```
sh -c "$(curl -sSfL https://release.solana.com/v1.17.0/install)"
```

## Configure Local Testnet
```
solana-test-validator --geyser-plugin-config ./config.json
```

## Set Up ClickHouse
Start ClickHouse using Docker
```
docker run -d --name clickhouse-server \
    -p 8123:8123 \
    -p 9000:9000 \
    --ulimit nofile=262144:262144 \
    clickhouse/clickhouse-server
```

## Build and Test
Build the Plugin
```
cargo build --release
```
Start Solana Validator with Plugin
```
solana-test-validator \
    --geyser-plugin-config config.json
```
Test Data Flow

Send test transactions:

```
solana transfer <RECIPIENT_ADDRESS> 1 --url http://localhost:8899
````

Query ClickHouse to verify data:

```
SELECT * FROM solana.transactions ORDER BY slot DESC LIMIT 5;
```
