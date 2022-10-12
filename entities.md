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

| Field                 | Type               | Description                                          |
| --------------------- | ------------------ | -----------------------------------------------------|
| id                    | ID!                | comptroller.address                                  |
| owner                 | Bytes!             | Wallet address of the owner                          |
| players               |[DripTokenPlayer!]! | Data derived at query time from field:"comptroller"  |
| balanceDrips          |[BalanceDrip!]!     | Data derived at query time from field:"comptroller"  |
| volumeDrips           |[VolumeDrip!]!      | Data derived at query time from field:"comptroller"  |


# PrizePool

| Field                        | Type                 | Description                                           |
| ---------------------------- | -------------------- | ------------------------------------------------------|
| id                           | ID!                  | prizePool.address                                     |
| deactivated                  | Boolean!             | Checks if prize pool is active                        |
| owner                        | Bytes!               | Wallet address of the owner                           |
| reserveRegistry              | Bytes!               | Reserve registry contract address                     |
| prizeStrategy                | PrizeStrategy        | Relation to prize strategy entity                     |
| prizePoolType                | PrizePoolType        | Relation to prize pool type entity                    |
| compoundPrizePool            | CompoundPrizePool    | Relation to compound prize pool entity                |
| stakePrizePool               | StakePrizePool       | Relation to stake prize pool entity                   |
| reserveFeeControlledToken    | Bytes!               | Reserve fee controlled token address                  |
| underlyingCollateralToken    | Bytes                | Underlying collateral token address                   |
| underlyingCollateralDecimals | BigInt               | Underlying collateral decimals                        |
| underlyingCollateralName     | String               | Underlying collateral token name                      |
| underlyingCollateralSymbol   | String               | Underlying collateral token symbol                    |
| maxExitFeeMantissa           | BigInt!              | Max exit fee mantissa for withdrawal from prize pool  |
| maxTimelockDuration          | BigInt!              | Max time lock duration for prize pool                 |
| timelockTotalSupply          | BigInt!              | Time lock total supply                                |
| liquididtyCap                | BigInt!              | Liquidiy cap for prize pool                           |
| cumulativePrizeGross         | BigInt!              | Cumulative prize gross                                |
| cumulativePrizeReserveFee    | BigInt!              | Cumulative prize reserve fee                          |
| cumulativePrizeNet           | BigInt!              | Cumulative prize net                                  |
| currentPrizeId               | BigInt!              | Current prize Id                                      |
| currentState                 | PrizePoolState!      | Relation to prize pool state entity                   |
| prizes                       | [Prize!]!            | Data derived at query time from field:"prizePool"     |
| tokenCreditRates             | [CreditRate!]!       | Data derived at query time from field:"prizePool"     |
| tokenCreditBalances          | [CreditBalance!]!    | Data derived at query time from field:"prizePool"     |
| prizePoolAccounts            | [PrizePoolAccount!]! | Data derived at query time from field:"prizePool"     |
| controlledToken              | [ControlledToken!]!  | Data derived at query time from field:"controller"    |


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

| Field              | Type                            | Description                                            |
| ------------------ | ------------------------------- | ------------------------------------------------------ |
| id                 | ID!                             | prizeStrategy.address                                  |
| singleRandomWinner | singleRandomWinnerPrizeStrategy | relation to single random winner prize strategy entity |
| multipleWinners    | multipleWinnersPrizeStrategy    | relation to multiple winners prize strategy entity     |


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
| externalErc20Awards  | [SingleRandomWinnerExternalErc20Award!]!  | Data derived at query time from field:"prizeStrategy"              |
| externalErc721Awards | [SingleRandomWinnerExternalErc721Award!]! | Data derived at query time from field:"prizeStrategy"              |


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
| awardedControlledTokens     | [AwardedControlledToken!]!    | Data derived at query time from field:"prize"          |
| awardedExternalErc20Tokens  | [AwardedExternalErc20Token!]! | Data derived at query time from field:"prize"          |
| awardedExternalErc721Nfts   | [AwardedExternalErc721Nft!]!  | Data derived at query time from field:"prize"          |


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

| Field      | Type       | Description                      |
| ---------- | ---------- | -------------------------------- |
| id         | ID!        | {prize.id}-${token.address}      |
| address    | Bytes!     | awarded Erc721 nft token address |
| tokenIds   | [BigInt!]  | Array of token Ids               |
| prize      | Prize      | Relation to the prize entity     |
| winner     | Bytes      | Wallet address of winner         |


# ControlledToken

| Field           | Type                       | Description                                             |
| --------------- | -------------------------- | ------------------------------------------------------- |
| id              | ID!                        | {controlledToken.address                                |
| name            | String!                    | Controlled token name                                   |
| symbol          | String!                    | Controlled token symbol                                 |
| decimals        | BigInt                     | Controlled token decimals                               |
| controller      | PrizePool                  | Relation to prize pool entity                           |
| totalSupply     | BigInt!                    | Total supply of controlled token                        |
| numberOfHolders | BigInt!                    | Number of controlled token holders                      |
| balances        | [ControlledTokenBalance!]! | Data derived at query time from field:"controlledToken" |


# ControlledTokenBalance

| Field           | Type             | Description                                 |
| --------------- | ---------------- | --------------------------------------------|
| id              | ID!              | composite key of (address, controlledToken) |
| account         | Account!         | User account                                |
| controlledToken | ControlledToken! | Relation to controlled token entity         |
| balance         | BigInt           | Controlled token balance                    |


# SingleRandomWinnerExternalErc20Award

| Field         | Type                            | Description                                            |
| ------------- | ------------------------------- | ------------------------------------------------------ |
| id            | ID!                             | {prizeStrategy.address}-${token.address}               |
| address       | Bytes!                          | Wallet address of the winner                           |
| name          | String                          | Token name                                             |
| symbol        | String                          | Token symbol                                           |
| decimals      | BigInt                          | Token decimals                                         |
| prizeStrategy | SingleRandomWinnerPrizeStrategy | Relation to single random winner prize strategy entity |


# SingleRandomWinnerExternalErc721Award

| Field         | Type                            | Description                                            |
| ------------- | ------------------------------- | ------------------------------------------------------ |
| id            | ID!                             | {prizeStrategy.address}-${token.address}               |
| address       | Bytes!                          | Wallet address of the winner                           |
| tokenIds      | [BigInt!]                       | Token Ids of the winner                                |
| prizeStrategy | SingleRandomWinnerPrizeStrategy | Relation to single random winner prize strategy entity |


# PrizePoolAccount 

| Field             | Type       | Description                                |
| ----------------- | --------   | ------------------------------------------ |
| id                | ID!        | {Composite prizerpool id} - {accountid}    |
| prizePool         | PrizePool! | Relation to prize pool entity              |
| account           | Account!   | Relation to account entity                 |
| timelockedBalance | BigInt!    | Time locked balance for prize pool account |
| unlockTimestamp   | BigInt!    | Unlocked timestamp for prize pool account  |


# Account 

| Field                   | Type                      | Description                                     |
| ----------------------- | ------------------------- | ----------------------------------------------- |
| id                      | ID!                       | User Address                                    |
| prizePoolAccounts       | [PrizePoolAccount!]!      | Data derived at query time from field:"account" |
| controlledTokenBalances | [ControlledTokenBalance!] | Data derived at query time from field:"account" |


# CreditRate

| Field               | Type       | Description                                   |
| ------------------- | ---------- | --------------------------------------------- |
| id                  | ID!        | {prizePool.address}-{controlledToken.address} |
| prizePool           | PrizePool! | Relation to prize pool entity                 |
| creditLimitMantissa | BigInt!    | Credit limit mantissa                         |
| creditRateMantissa  | BigInt!    | Credit rate mantissa                          |


# CreditBalance

| Field       | Type       | Description                                   |
| ----------- | ---------- | --------------------------------------------- |
| id          | ID!        | {prizePool.address}-{controlledToken.address} |
| prizePool   | PrizePool! | Relation to prize pool entity                 |
| balance     | BigInt     | Credit balance                                |
| timestamp   | BigInt     | Credit balance timestamp                      |
| initialized | Boolean    | Checks wether crdit balance is initialized    |


# DripTokenPlayer

| Field       | Type         | Description                                                |
| ----------- | ------------ | ---------------------------------------------------------- |
| id          | ID!          | {comptroller.address}-{dripToken.address}-{player.address} |
| comptroller | Comptroller! | Relation to comptroller entity                             |
| dripToken   | Bytes!       | Address for drip token                                     |
| address     | Bytes!       | Player wallet address                                      |
| balance     | BigInt!      | Claimable balance                                          |


# BalanceDripPlayer 

| Field       | Type         | Description                        |
| ----------- | -------------| -----------------------------------|
| id          | ID!          | {balanceDripId}-${player.address}  |
| balanceDrip | BalanceDrip! | Relation to balance drip entity    |
| address     | Bytes!       | Player wallet address              |


# BalanceDrip 

| Field                | Type                  | Description                         |
| -------------------- | --------------------- | ----------------------------------------------------------------------------------------- |
| id                   | ID!                   | {comptroller.address}-${sourceToken.address}-${measureToken.address}-${dripToken.address} |
| comptroller          | Comptroller!          | Relation to comptroller entity                                                            |
| sourceAddress        | Bytes!                | Source address                                                                            |
| measureToken         | Bytes!                | Measure token address                                                                     |
| dripToken            | Bytes!                | Drip token address                                                                        |
| dripRatePerSecond    | BigInt                | Drip rate per second                                                                      |
| exchangeRateMantissa | BigInt                | exchange rate mantissa                                                                    |
| timestamp            | BigInt                | Balance drip timestamp                                                                    |
| players              | [BalanceDripPlayer!]! | Data derived at query time from field:"balanceDrip"                                       |
| deactivated          | Boolean!              | Checks wether balance drip is deactivated                                                 |


# VolumeDripPlayer

| Field       | Type        | Description                       |
| ----------- | ----------- | --------------------------------- |
| id          | ID!         | {volumeDripId}-${player.address}  |
| volumeDrip  | VolumeDrip! | Relation to volume drip entity    |
| address     | Bytes!      | Player wallet address             |
| periodIndex | BigInt!     | Period index                      |
| balance     | BigInt!     | Claimable balance                 |


# VolumeDripPeriod 

| Field       | Type        | Description                    |
| ----------- | ----------- | ------------------------------ |
| id          | ID!         | ${volumeDripId}-${periodIndex} |
| volumeDrip  | VolumeDrip! | Relation to volume drip entity |
| periodIndex | BigInt!     | Period index                   |
| totalSupply | BigInt      | Volume drip total supply       |
| dripAmount  | BigInt      | Drip amount                    |
| endTime     | BigInt      | Drip end time                  |
| isDripping  | Boolean!    | Checks wether drip is active   |


# VolumeDrip  

| Field         | Type                 | Description                         |
| ------------- | -------------------- | ----------------------------------- |
| id            | ID!                  | ${comptroller.address}-${sourceToken.address}-${measureToken.address}-${dripToken.address}-${isReferral} |
| comptroller   | Comptroller!         |                                                            |
| sourceAddress | Bytes!               |                                        |
| measureToken  | Bytes!               |                                 |
| dripToken     | Bytes!               |                                |
| referral      | Boolean!             |                       |
| periodSeconds | BigInt               |                       |
| dripAmount    | BigInt               |                     |
| periodCount   | BigInt               |                     |
| deposits      | [VolumeDripPlayer!]! | @derivedFrom(field: "volumeDrip")    |
| periods       | [VolumeDripPeriod!]! | @derivedFrom(field: "volumeDrip")    |
| deactivated   | Boolean!             |                                    |
  

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


