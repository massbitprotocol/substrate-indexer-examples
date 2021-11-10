# Getting Started

### 1. Install dependencies

```shell
yarn
```

### 2. Generate types

```shell
yarn codegen
```

### 3. Build the project

```shell
yarn build
```

### 4. Start Indexer Manager
```shell
yarn start:manager

```

### 5. Deploy the project

```shell
yarn deploy
```

### 6. After indexer starting, run GraphQL query service
```shell
yarn start:query
```

### 7. Open `http://127.0.0.1:3001`, run following query

```shell
query {
  accounts(first:10 orderBy:BALANCE_DESC) {
    nodes {
      account
      balance
    }
  }
}
```

# Understanding this project

This project has a function called `handleEvent`. It uses an `EventHandler` which is defined in the manifest file (project.yaml) as "kind: substrate/EventHandler"

The `schema.graphql` file defines the variables blockHeight which is mandatory and of type Int.

If we examine the function `handleEvent` in more detail, you can see that this function takes one argument of type SubstrateEvent. It then creates a new instance of Account passing in the `event.extrinsic.block.block.header.hash` argument as a string and assigning this to the variable record.

Next, the account is converted to a string via `toString()` and assigned to `record.account`. The balance is type cast as Balance and converted to a big integer.
