---
title: Contracts
---

<head>
    <title>Staking Contracts</title>
</head>

There are a few different contracts involved in EOS staking.

1. `eosio.system` - The system and staking contract.
2. `eosio.reward` - An intermediate reward dispersal contract.
3. `eosio.rex` - Account that holds all funds in the staking protocol.

## eosio.system

The system contract is wider than just staking and controls the entire EOS network with 
capabilities like account creation, chain governance, and resource management.

The staking portions of the system contract are responsible for managing the staking
and unstaking of EOS tokens, as well as the distribution of rewards from the pre-allocated
staking rewards pool.

### Depositing Funds

In order to use EOS inside the staking portion of the system contract, you need to deposit them first. 

```cpp
void deposit( const name& owner, const asset& amount )
```

This will transfer your funds to the `eosio.rex` account and register them as deposited into the staking protocol.
This will **not** stake them for you yet though, they are simply held within the protocol.

> **Parameters**   
> The parameter `owner` is the account that is depositing the funds.

### Staking Deposited Funds

Once you have deposited funds into the staking protocol, you can stake them to receive rewards.

```cpp
void buyrex( const name& from, const asset& amount )
```

This will stake the funds that you have deposited into the staking protocol and issue you REX tokens in return.


### Staking Funds From Voting Rights

On EOS you can have your EOS staked as voting rights. You may also use those funds as a source for staking.

```cpp
void unstaketorex( const name& owner, const name& receiver, const asset& from_net, const asset& from_cpu )
```

This will move your voting rights staked funds into rewards staked funds, and issue you REX tokens in return.
You will still retain your voting rights.

> **Note**   
> All staked funds within the staking protocol have voting rights attached to them.


### Unstaking Funds

```cpp
void mvfrsavings( const name& owner, const asset& rex )
```

This will move funds out of eternally locked "savings" account and begin the 21 day unstaking period. Any funds you 
move out of that savings account within the same day will be attributed to the same unstaking bucket and mature within
the same 21-day period.

### Withdrawing Funds

Once the 21-day unstaking/maturation period has finished, you can sell your position and withdraw your funds.
You will need to do this in two steps.

```cpp
void sellrex( const name& from, const asset& rex )
```

This action will convert your REX tokens back into EOS and register them as available to withdraw.

```cpp
void withdraw( const name& owner, const asset& amount )
```

This action will withdraw your EOS tokens from the staking protocol and transfer them to your account.


> **Note**   
> Any action you take within the staking protocol once a 21-day unstaking period has finished will trigger an 
> automatic `sellrex` on your fully matured REX tokens. This will convert them back into EOS and register them as 
> available to withdraw.

### Tables

The system contract has a few tables that are relevant to staking.

#### rexbal

[The `rexbal` table](https://eosauthority.com/account/eosio?network=eos&scope=eosio&table=rexbal&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables) holds information about staked balances for users.

- `version`
- `owner`
- `vote_stake`
- `rex_balance` - the amount of REX owned
- `matured_rex` - matured REX available for selling
- `rex_maturities` - An array of maturity dates and amounts

#### rexfund

[The `rexfund` table](https://eosauthority.com/account/eosio?network=eos&scope=eosio&table=rexfund&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables&lower_bound=)
holds information about the deposited but unstaked EOS funds for users. 

- `version`
- `owner`
- `balance` - the amount of EOS deposited

#### rexmaturity

[The `rexmaturity` table](https://eosauthority.com/account/eosio?network=eos&scope=eosio&table=rexmaturity&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables)
holds information about the maturity dates of REX tokens for users.

- `num_of_maturity_buckets` - The number of days until a position fully matures
- `sell_matured_rex` - A flag that indicates if to sell matured positions on any action
- `buy_rex_to_savings` - A flag that indicates if staked funds go directly to savings or not

#### rexpool

[The `rexpool` table](https://eosauthority.com/account/eosio?network=eos&scope=eosio&table=rexpool&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables)
holds information about the staking pool.

- `version`
- `total_lent` - total amount of EOS in open rex_loans
- `total_unlent` - total amount of EOS available to be lent (connector)
- `total_rent` - fees received in exchange for lent (connector)
- `total_lendable` - total amount of EOS that have been lent (total_unlent + total_lent)
- `total_rex` - total number of REX shares allocated to contributors to total_lendable
- `namebid_proceeds` the amount of EOS to be transferred from namebids to REX pool
- `loan_num` increments with each new loan

This is useful if you want to calculate the price of EOS vs REX. 

```typescript
static convertEosToRex(eos:number){
    const pool = get(rexpool);
    if(!pool) return 0;
    const S0 = parseFloat(pool.total_lendable.split(' ')[0]);
    const S1 = S0 + eos;
    const R0 = parseFloat(pool.total_rex.split(' ')[0]);
    const R1 = (S1 * R0) / S0;
    return parseFloat(parseFloat((R1 - R0).toString()).toFixed(4));
}

static convertRexToEos(rex:number){
    const pool = get(rexpool);
    if(!pool) return 0;
    const S0 = parseFloat(pool.total_lendable.split(' ')[0]);
    const R0 = parseFloat(pool.total_rex.split(' ')[0]);
    const R1 = R0 + rex;
    const S1 = (S0 * R1) / R0;
    return parseFloat(parseFloat((S1 - S0).toString()).toFixed(4));
}
```

If you'd like to view full code for this example, [see here](https://github.com/eosnetworkfoundation/rex-staking-portal/blob/6f1297bbb5cc5e4d1e39ac5e52e815ea69a29803/src/lib/wharf.ts#L142-L143).

#### rexretpool

[The `rexretpool` table](https://eosauthority.com/account/eosio?network=eos&scope=eosio&table=rexretpool&limit=10&index_position=1&key_type=i64&reverse=0&mode=contract&sub=tables)
holds information about the return pool for REX tokens.

- `version`
- `last_dist_time` - the last time proceeds from renting, ram fees, and name bids were added to the rex pool
- `pending_bucket_time` - timestamp of the pending 12-hour return bucket
- `oldest_bucket_time` - cached timestamp of the oldest 12-hour return bucket
- `pending_bucket_proceeds` proceeds in the pending 12-hour return bucket,
- `current_rate_of_increase` the current rate per dist_interval at which proceeds are added to the rex pool,
- `proceeds` the maximum amount of proceeds that can be added to the rex pool at any given time

## eosio.reward

The [reward contract](https://eosauthority.com/account/eosio.reward) is an intermediate contract that is responsible for 
dispersing the rewards from the staking rewards pool to the various strategies aimed at rewarding the EOS community via 
various mechanisms.



## eosio.rex