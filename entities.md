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

| Field                 | Type               | Description                                                        |
| --------------------- | ------------------ | -------------------------------------------------------------------|
| id                    | ID!                | comptroller.address                                                |
| owner                 | Bytes!             | Wallet address of the owner                                        |
| players               |[DripTokenPlayer!]! | Data derived at query time in relation to drip token player entity |
| balanceDrips          |[BalanceDrip!]!     | Data derived at query time in relation to balance drip entity      |
| volumeDrips           |[VolumeDrip!]!      | Data derived at query time in relation to volume drip entity       |


# PrizePool

| Field                        | Type                 | Description                                                        |
| ---------------------------- | -------------------- | -------------------------------------------------------------------|
| id                           | ID!                  | prizePool.address                                                  |
| deactivated                  | Boolean!             | Checks if prize pool is active                                     |
| owner                        | Bytes!               | Wallet address of the owner                                        |
| reserveRegistry              | Bytes!               | Reserve registry contract address                                  |
| prizeStrategy                | PrizeStrategy        | Relation to prize strategy entity                                  |
| prizePoolType                | PrizePoolType        | Relation to prize pool type entity                                 |
| compoundPrizePool            | CompoundPrizePool    | Relation to compound prize pool entity                             |
| stakePrizePool               | StakePrizePool       | Relation to stake prize pool entity                                |
| reserveFeeControlledToken    | Bytes!               | Reserve fee controlled token address                               |
| underlyingCollateralToken    | Bytes                | Underlying collateral token address                                |
| underlyingCollateralDecimals | BigInt               | Underlying collateral decimals                                     |
| underlyingCollateralName     | String               | Underlying collateral token name                                   |
| underlyingCollateralSymbol   | String               | Underlying collateral token symbol                                 |
| maxExitFeeMantissa           | BigInt!              | Max exit fee mantissa for withdrawal from prize pool               |
| maxTimelockDuration          | BigInt!              | Max time lock duration for prize pool                              |
| timelockTotalSupply          | BigInt!              | Time lock total supply                                             |
| liquididtyCap                | BigInt!              | Liquidiy cap for prize pool                                        |
| cumulativePrizeGross         | BigInt!              | Cumulative prize gross                                             |
| cumulativePrizeReserveFee    | BigInt!              | Cumulative prize reserve fee                                       |
| cumulativePrizeNet           | BigInt!              | Cumulative prize net                                               |
| currentPrizeId               | BigInt!              | Current prize Id                                                   |
| currentState                 | PrizePoolState!      | Current state of prize pool in relation to prize pool state entity |
| prizes                       | [Prize!]!            | Data derived at query time in relation to prize entity             |
| tokenCreditRates             | [CreditRate!]!       | Data derived at query time in relation to prize entity             |
| tokenCreditBalances          | [CreditBalance!]!    | Data derived at query time in relation to prize entity             |
| prizePoolAccounts            | [PrizePoolAccount!]! | Data derived at query time in relation to prize entity             |
| controlledToken              | [ControlledToken!]!  | Data derived at query time in relation to controller entity        |


# CompoundPrizePool

| Field       | Type       | Description                |
| ----------- | ---------- | -------------------------- |
| id          | ID!        | compoundPrizePool.address  |
| cToken      | Bytes      | cToken address             |


# StakePrizePool

| Field       | Type       | Description                |
| ----------- | ---------- | -------------------------- |
| id          | ID!        | compoundPrizePool.address  |
| stakeToken  | Bytes      | stake token address        |


# PrizeStrategy

| Field              | Type                            | Description                                     |
| ------------------ | ------------------------------- | ----------------------------------------------- |
| id                 | ID!                             | prizeStrategy.address                           |
| singleRandomWinner | singleRandomWinnerPrizeStrategy | relation to single random winner prize strategy |
| multipleWinners    | multipleWinnersPrizeStrategy    | relation to multiple winners prize strategy     |


# SingleRandomWinnerPrizeStrategy

| Field                | Type                                      | Description                                                        |
| -------------------- | ----------------------------------------- | ------------------------------------------------------------------ |
| id                   | ID!                                       | singleRandomWinner.address (will be same address as PrizeStrategy) |
| owner                | Bytes                                     | Wallet address of owner                                            |
| tokenListener        | Comptroller                               | Relation to comptroller entity                                     |
| prizePool            | PrizePool                                 | Relation to prize pool entity                                      |
| rng                  | Bytes                                     | Random number generator address                                    |
| ticket               | ControlledToken                           | Relation to controlled token entity                                |
| sponsorship          | ControlledToken                           | Relation to controlled token entity                                |
| prizePeriodSeconds   | BigInt!                                   | Prize period interval in seconds                                   |
| prizePeriodStartedAt | BigInt!                                   | Prize period started at timestamp                                  |
| prizePeriodEndAt     | BigInt!                                   | Prize period ended at timestamp                                    |
| externalErc20Awards  | [SingleRandomWinnerExternalErc20Award!]!  | Data derived at query time in relation to prize strategy entity    |
| externalErc721Awards | [SingleRandomWinnerExternalErc721Award!]! | Data derived at query time in relation to prize strategy entity    |


# Prize
 {Dynamically generated entity type, not mapped to a specific contract}
| Field                       | Type                          | Description                                            |
| --------------------------- | ----------------------------- | ------------------------------------------------------ |
| id                          | ID!                           | {prizePool.address}-{prizeCount}                       |
| prizePool                   | PrizePool!                    | Relation to the prize pool entity                      |
| awardStartOperator          | Bytes                         | Address of the award start operator                    |
| awardedOperator             | Bytes                         | Address of the awarded operator                        |
| prizePeriodStartedTimestamp | Bytes                         | Timestamp of when the prize period started             |
| lockBlock                   | BigInt                        | Block where prize was locked                           |
| awardedBlock                | BigInt                        | Block where prize was awarded                          |
| awardedTimestamp            | BigInt                        | Timestamp of when the prize was awarded                |
| rngrequestId                | BigInt                        | Random number generator request Id                     |
| randomNumber                | BigInt                        | Random Number                                          |
| numberOfSubWinners          | BigInt                        | Number of sub-winners                                  |
| totalTicketSupply           | BigInt                        | cache of num tickets sold when this prize was awarded  |
| awardedControlledTokens     | [AwardedControlledToken!]!    | Data derived at query time in relation to prize entity |
| awardedExternalErc20Tokens  | [AwardedExternalErc20Token!]! | Data derived at query time in relation to prize entity |
| awardedExternalErc721Nfts   | [AwardedExternalErc721Nft!]!  | Data derived at query time in relation to prize entity |


# AwardedControlledToken

| Field      | Type                | Description                             |
| ---------- | ------------------- | --------------------------------------- |
| id         | ID!                 | {prizePool.id}-{winner}                 |
| winner     | Bytes!              | Wallet address of winner                |
| amount     | BigInt!             | Amount won by winner                    |
| token      | ControlledToken!    | Relation to the controlled token entity |
| prize      | Prize!              | Relation to the prize entity            |


# AwardedExternalErc20Token

| Field          | Type   | Description                         |
| -------------- | ------ | ----------------------------------- |
| id             | ID!    | {prize.id}-${token.address}         |
| address        | Bytes! | awarded Erc20 token address         |
| name           | String | Name of token                       |
| symbol         | String | Token symbol                        |
| decimals       | BigInt | Token decimals                      |
| balanceAwarded | BigInt | Balance awarded                     |
| prize          | Prize! | Relation to the prize entity        |
| winner         | Bytes  | Wallet address of winner            |


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


