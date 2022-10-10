# Entities

## Entities for the PoolTogether Subgraph are all listed below
- [Comptroller](#Comptroller)
- [PrizePool](#PrizePool)
- [CompoundPrizePool](#CompoundPrizePool)
- [StakePrizePool](#StakePrizePool)
- [PrizeStrategy](#PrizeStrategy)
- [SingleRandomWinnerPrizeStrategy](#SingleRandomWinnerPrizeStrategy)
- [Prize](#Prize)
- [AwardedControlledToken](#AwardedControlledToken)
- [AwardedExternalErc20Token](#AwardedExternalErc20Token)
- [AwardedExternalErc721Nft](#AwardedExternalErc721Nft)
- [ControlledToken](#ControlledToken)
- [ControlledTokenBalance](#ControlledTokenBalance)
- [SingleRandomWinnerExternalErc721Award](#SingleRandomWinnerExternalErc721Award)
- [PrizePoolAccount](#PrizePoolAccount)
- [Account](#Account)
- [CreditRate](#CreditRate)
- [CreditBalance](#CreditBalance)
- [DripTokenPlayer](#DripTokenPlayer)
- [BalanceDripPlayer](#BalanceDripPlayer)
- [BalanceDrip](#BalanceDrip)
- [VolumeDripPlayer](#VolumeDripPlayer)
- [VolumeDripPeriod](#VolumeDripPeriod)
- [VolumeDrip](VolumeDrip)
- [MultipleWinnersPrizeStrategy](#MultipleWinnersPrizeStrategy)
- [MultipleWinnersExternalErc20Award](#MultipleWinnersExternalErc20Award)
- [MultipleWinnersExternalErc721Award](#MultipleWinnersExternalErc721Award)


# Comptroller

| Field                 | Type     | Description                                 |
| --------------------- | -------- | ------------------------------------------- |
| id                    | ID!      | comptroller.address                         |
| owner                 | Bytes!   |                                             |
| players               |          |                                             |
| balanceDrips          |          |                                             |
| volumeDrips           |          |                                             |


# PrizePool

| Field                 | Type              | Description                                 |
| --------------------- | ----------------- | ------------------------------------------- |
| id                    | ID!               | prizePool.address                           |
| deactivated           | Boolean!          |                                             |
| owner                 | Bytes!            |                                             |
| reserveRegistry       | Bytes!            |                                             |
| prizeStrategy         | PrizeStrategy     |                                             |
| prizePoolType         | PrizePoolType     |                                             |
| compoundPrizePool     | CompoundPrizePool |                                             |
| stakePrizePool        | StakePrizePool    |                                             |
| reserveFeeControlledToken | Bytes! |                                        |
| underlyingCollateralToken | Bytes |                                        |
| underlyingCollateralDecimals | BigInt |                                    |
| underlyingCollateralName | String |                                        |
| underlyingCollateralSymbol | String |                                      |
| maxExitFeeMantissa | BigInt! |                                             |
| maxTimelockDuration | BigInt! |                                            |
| timelockTotalSupply | BigInt! |                                            |
| liquididtyCap | BigInt! |                                                  |
| cumulativePrizeGross | BigInt! |                                           |
| cumulativePrizeReserveFee | BigInt! |                                      |
| cumulativePrizeNet | BigInt! |                                             |
| currentPrizeId | BigInt! |                                    |
| currentState | PrizePoolState! |                               |
| prizes | [Prize!]! | @derivedFrom(field: "prizePool")          |
| tokenCreditRates | [CreditRate!]! | @derivedFrom(field: "prizePool") |
| tokenCreditBalances | [CreditBalance!]! | @derivedFrom(field: "prizePool") |
| prizePoolAccounts | [PrizePoolAccount!]! | @derivedFrom(field: "prizePool") |
| controlledToken | [ControlledToken!]! | @derivedFrom(field: "controller") controlled tokens may not exist until transfer is called |


# CompoundPrizePool

| Field       | Type       | Description                |
| ----------- | ---------- | -------------------------- |
| id          | ID!        | compoundPrizePool.address  |
| cToken      | Bytes      |                            |


# CompoundPrizePool

| Field       | Type       | Description                |
| ----------- | ---------- | -------------------------- |
| id          | ID!        | compoundPrizePool.address  |




