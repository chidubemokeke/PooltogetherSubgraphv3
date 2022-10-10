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


## Comptroller

| Field                 | Type     | Description                                 |
| --------------------- | -------- | ------------------------------------------- |
| id                    | ID!      | comptroller.address                         |
| owner                 | Bytes!   |                                             |
| players               |          |                                             |
| balanceDrips          |          |                                             |
| volumeDrips           |          |                                             |


## PrizePool

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


# StakePrizePool

| Field       | Type       | Description                |
| ----------- | ---------- | -------------------------- |
| id          | ID!        | compoundPrizePool.address  |
| stakeToken  | Bytes      |                            |


# PrizeStrategy

| Field              | Type                            | Description                         |
| ------------------ | ------------------------------- | ----------------------------------- |
| id                 | ID!                             | prizeStrategy.address               |
| singleRandomWinner | singleRandomWinnerPrizeStrategy |                                     |
| multipleWinners    | multipleWinnersPrizeStrategy    |                                     |


# SingleRandomWinnerPrizeStrategy

| Field                | Type                                      | Description                                                        |
| -------------------- | ----------------------------------------- | ------------------------------------------------------------------ |
| id                   | ID!                                       | singleRandomWinner.address (will be same address as PrizeStrategy) |
| owner                | Bytes                                     |                                                                    |
| tokenListener        | Comptroller                               |                                                                    |
| prizePool            | PrizePool                                 |                                                                    |
| rng                  | Bytes                                     |                                                                    |
| ticket               | ControlledToken                           |                                                                    |
| sponsorship          | ControlledToken                           |                                                                    |
| prizePeriodSeconds   | BigInt!                                   |                                                                    |
| prizePeriodStartedAt | BigInt!                                   |                                                                    |
| prizePeriodEndAt    | BigInt!                                   |                                                                    |
| externalErc20Awards  | [SingleRandomWinnerExternalErc20Award!]!  | @derivedFrom(field: "prizeStrategy")                               |
| externalErc721Awards | [SingleRandomWinnerExternalErc721Award!]! | @derivedFrom(field: "prizeStrategy")                               |


# Prize

| Field                | Type                                      | Description                                                        |
| -------------------- | ----------------------------------------- | ------------------------------------------------------------------ |
| id                   | ID!                                       | {prizePool.address}-{prizeCount}       |
| prizePool            | PrizePool!             |                                                         |
| awardStartOperator   | Bytes                      |                                |
| awardedOperator      | Bytes                      |                                |
| prizePeriodStartedTimestamp | Bytes               |                                |
| lockBlock             | BigInt            |                                        |
| awardedBlock          | BigInt                       |                            |
| awardedTimestamp      | BigInt                      |                             |
| rngrequestId          | BigInt                       |                           |
| randomNumber          | BigInt                    |                              |
| numberOfSubWinners    | BigInt                    |                              |
| totalTicketSupply     | BigInt                    | cache of num tickets sold when this prize was awarded |
| awardedControlledTokens | [AwardedControlledToken!]! | @derivedFrom(field: "prize") |
| awardedExternalErc20Tokens | [AwardedExternalErc20Token!]! | @derivedFrom(field: "prize") |
| awardedExternalErc721Nfts | [AwardedExternalErc721Nft!]! | @derivedFrom(field: "prize") |


# AwardedControlledToken

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prizePool.id}-{winner}             |
| winner     | Bytes!              |                                     |
| amount     | BigInt!             |                                     |
| token      | ControlledToken!    |                                     |
| prize      | Prize!              |                                     |


# AwardedExternalErc20Token

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prize.id}-${token.address}         |
| address    | Bytes!              |                                     |
| name       | String              |                                     |
| symbol     | String              |                                     |
| decimals   | BigInt              |                                     |
| balanceAwarded | BigInt          |                                     |
| prize      | Prize!              |                                    |
| winner     | Bytes               |                                    |


# AwardedExternalErc721Nft

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prize.id}-${token.address}         |
| address    | Bytes!              |                                     |
| tokenIds   | [BigInt!]           |                                     |
| prize      | Prize               |                                     |
| winner     | Bytes               |                                     |


# ControlledToken

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {controlledToken.address           |
| name       | String!              |                                     |
| symbol     | String!              |                                     |
| decimals   | BigInt              |                                     |
| controller | PrizePool           |                                    |
| totalSupply | BigInt!            |                                    |
| numberOfHolders | BigInt!        |                                    |
| balances        | [ControlledTokenBalance!]! | @derivedFrom(field:"controlledToken") |


# ControlledTokenBalance

| Field      | Type                | Description                         |
| ---------- | ------------------- | ---------------------------------------------- |
| id         | ID!                 | composite key of (address, controlledToken)          |
| account    | Account!            |                                                |
| controlledToken | ControlledToken! |                                              |
| balance     | BigInt   |                                                |


# SingleRandomWinnerExternalErc20Award

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prizeStrategy.address}-${token.address}         |
| address    | Bytes!              |                                     |
| name       | String              |                                     |
| symbol     | String              |                                     |
| decimals   | BigInt              |                                     |
| prizeStrategy | SingleRandomWinnerPrizeStrategy |                                     |


# SingleRandomWinnerExternalErc721Award

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prizeStrategy.address}-${token.address}  |
| address    | Bytes!              |                                     |
| tokenIds   | [BigInt!]           |                                     |
| prizeStrategy | SingleRandomWinnerPrizeStrategy |                            |


# PrizePoolAccount 

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | Composite prizerpool id - accountid  |
| prizePool  | PrizePool!          |                                     |
| account    | Account!            |                                     |
| timelockedBalance | BigInt! |                        |
| unlockTimestamp | BigInt!       |                           |


# Account 

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | User Address                   |
| prizePoolAccounts | [PrizePoolAccount!]! | @derivedFrom(field: "account") |
| controlledTokenBalances | [ControlledTokenBalance!] | @derivedFrom(field: "account") |


# CreditRate

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prizePool.address}-{controlledToken.address}  |
| prizePool  | PrizePool!          |                                     |
|creditLimitMantissa | BigInt!   |                                      |
| creditRateMantissa | BigInt!   |                                      |
| 


# CreditBalance

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prizePool.address}-{controlledToken.address}  |
| prizePool  | PrizePool!          |                                     |
| balance    | BigInt        |                                     |
| timestamp  | BigInt               |                              |
| initialized | Boolean            |                                |


# DripTokenPlayer

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {comptroller.address}-{dripToken.address}-{player.address} |
| comptroller | Comptroller!       |                                                            |
| dripToken  | Bytes!              |                                                            |
| address    | Bytes!              |                                     |
| balance    | BigInt!        |  Claimable balance                                   |


# BalanceDripPlayer 

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {balanceDripId}-${player.address}   |
| balanceDrip | BalanceDrip! |                                    |
| address     | Bytes!       |                             |


# BalanceDrip 

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {comptroller.address}-${sourceToken.address}-${measureToken.address}-${dripToken.address} |
| comptroller | Comptroller!       |                                                            |
| sourceAddress | Bytes! |                                        |
| measureToken |  Bytes!    |                                 |
| dripToken    | Bytes!    |                                |
| dripRatePerSecond | BigInt |                             |
| exchangeRateMantissa | BigInt |                        |
| timestamp            | BigInt |                        |
| players              | [BalanceDripPlayer!]! | @derivedFrom(field: "balanceDrip") |
| deactivated          | Boolean! |                                     |


# VolumeDripPlayer

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {volumeDripId}-${player.address}    |
| volumeDrip | VolumeDrip!         |                                     |
| address    | Bytes!              |                                     |
| periodIndex | BigInt!            |                                     |
| balance    | BigInt!        |  Claimable balance                                   |


# VolumeDripPeriod 

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | ${volumeDripId}-${periodIndex}      |
| volumeDrip | VolumeDrip!         |                                     |
| periodIndex | BigInt!            |                                     |
| totalSupply | BigInt            |                                    |
| dripAmount  | BigInt             |                                     |
| endTime     | BigInt             |                                     |
| isDripping  | Boolean!           |                                     |


# VolumeDrip  

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!            | ${comptroller.address}-${sourceToken.address}-${measureToken.address}-${dripToken.address}-${isReferral} |
| comptroller | Comptroller!       |                                                            |
| sourceAddress | Bytes! |                                        |
| measureToken |  Bytes!    |                                 |
| dripToken    | Bytes!    |                                |
| referral     | Boolean! |                       |
| periodSeconds | BigInt  |                       |
| dripAmount    | BigInt  |                     |
| periodCount   | BigInt  |                     |
| deposits      | [VolumeDripPlayer!]! | @derivedFrom(field: "volumeDrip")    |
| periods       | [VolumeDripPeriod!]! | @derivedFrom(field: "volumeDrip")    |
| deactivated   | Boolean!     |                                    |


# MultipleWinnersPrizeStrategy

| Field                | Type                                      | Description                                           |
| -------------------- | ---------------------------- | ------------------------------------------------------------------ |
| id                   | ID!                          | multipleWinners.address (will be same address as PrizeStrategy) |**
| owner                | Bytes                        |                                                                    | 
| numberOfWinners     | BigInt                       |                                       |
| tokenListener        | Bytes                               |                                                           |
| prizePool            | PrizePool                 |                                                                    |
| rng                  | Bytes                      |                                                                    | 
| ticket             | ControlledToken       |                                      |
| sponsorship        | ControlledToken       |                                      |
| prizePeriodSeconds   | BigInt!                                   |                                                |
| prizePeriodStartedAt | BigInt!                                   |                                                |
| prizePeriodEndAt    | BigInt!                                    |                                               | 
| externalErc20Awards  | [MultipleWinnersExternalErc20Award!]!  | @derivedFrom(field: "prizeStrategy")              |
| externalErc721Awards | [MultipleWinnersExternalErc721Award!]! | @derivedFrom(field: "prizeStrategy")              |


# MultipleWinnersExternalErc20Award

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prizeStrategy.address}-${token.address}         |
| address    | Bytes!              |                                     |
| name       | String              |                                     |
| symbol     | String              |                                     |
| decimals   | BigInt              |                                     |
| balanceAwarded  | BigInt         |                                     |
| prizeStrategy | SingleRandomWinnerPrizeStrategy |                      |


# MultipleWinnersExternalErc721Award

| Field      | Type                | Description                         |
| ---------- | ------------------- | ----------------------------------- |
| id         | ID!                 | {prizeStrategy.address}-${token.address}  |
| address    | Bytes!              |                                     |
| tokenIds   | [BigInt!]           |                                     |
| prizeStrategy | MultipleWinnersPrizeStrategy |                         |


