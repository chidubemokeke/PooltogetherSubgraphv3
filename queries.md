

## Sample Queries
Below are some sample queries you can use to gather information from the PoolTogether V3 subgraph

You can build your own queries using a [GraphQL Explorer](https://graphiql-online.com/graphiql) and enter your endpoint to limit the data to exactly what you need.

### PrizePools

Description: This query fetches the last 20 prize pools, the state of the pools and the balance from the protocol.

```graphql
{
  prizePools(first: 20, orderDirection: desc) {
    id
    reserveRegistry
    underlyingCollateralName
    compoundPrizePool {
      cToken
    }
    currentState
    prizePoolAccounts {
      account {
        id
        controlledTokenBalances {
          balance
        }
      }
    }
  }
}
```

### Prizes 

Description: This query fetches the last 20 prizes awarded in the protocol

```graphql
   prizes(first: 20, orderBy: id, orderDirection: desc) {
    id
    awardedBlock
    awardedExternalErc20Tokens {
      id
      symbol
      name
      winner
      balanceAwarded
    }
    awardedExternalErc721Nfts {
      id
      tokenIds
      winner
    }
    awardedControlledTokens {
      id
      amount
      winner
      token {
        name
        symbol
      }
    }
  }
}
```

### Reward time

Description: This query fetches the pools' reward time and amount.

```graphql
{
    prizePools {
    id
    prizes {
      awardedTimestamp
      awardedControlledTokens {
        winner
        amount
      }
    }
  }
}
```

