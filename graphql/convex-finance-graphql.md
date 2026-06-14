# Convex Finance GraphQL API

## Description

Convex Finance is a DeFi yield-boosting protocol built on top of Curve Finance. It allows liquidity providers and CRV stakers to earn boosted rewards via pooled CVX staking without individually locking CRV. This GraphQL API is powered by The Graph protocol and indexes on-chain data from the Convex Booster contract on Ethereum mainnet.

## Endpoint

```
https://api.thegraph.com/subgraphs/name/convex-community/convex-subgraph
```

## Documentation

- Developer Docs: https://docs.convexfinance.com/
- Subgraph Source: https://github.com/convex-community/convex-subgraph
- The Graph Explorer: https://thegraph.com/explorer/subgraphs?search=convex

## Key Entity Types

| Type | Description |
|------|-------------|
| Pool | Convex pool wrapping a Curve gauge, including TVL, APR, and token info |
| DailyPoolSnapshot | Daily aggregate of pool metrics: deposits, withdrawals, APRs, TVL |
| DailyRevenueSnapshot | Daily revenue breakdown across CRV, CVX, FXS, bribes, treasury |
| FeeRevenue | Fee revenue events attributed to the platform |
| Deposit | Individual user deposit events into a pool |
| Withdrawal | Individual user withdrawal events from a pool |
| User | User account tracking deposits and withdrawals |
| ExtraReward | Extra reward token contracts attached to a pool |
| PoolReward | CRV reward harvest events per pool |
| Platform | Global platform-level aggregate stats and cumulative revenue |

## Example Query

```graphql
{
  pools(first: 5, orderBy: tvl, orderDirection: desc) {
    id
    poolid
    name
    tvl
    crvApr
    cvxApr
    baseApr
    active
  }
}
```

## Notes

- The subgraph is maintained by the Convex Community and indexes the Convex Booster contract.
- Revenue data includes CRV, CVX, FXS, and bribe revenue streams distributed to LP providers, CvxCrv stakers, CVX stakers, callers, and the treasury.
- Pool APR fields cover CRV rewards, CVX rewards, extra token rewards, and base Curve APR.
- The `Platform` entity aggregates cumulative protocol-level revenue across all reward types.
- Schema source: https://raw.githubusercontent.com/convex-community/convex-subgraph/master/subgraphs/convex/schema.graphql
