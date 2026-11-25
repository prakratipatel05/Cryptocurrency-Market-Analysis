# Data Dictionary --- CoinGecko Cryptocurrency Market Data

## 1. Dataset Overview

This dataset is retrieved from the CoinGecko **Coins Markets API**:

`https://api.coingecko.com/api/v3/coins/markets`

The endpoint returns market information for cryptocurrencies, including
their current prices, market capitalisation, trading volume, supply, and
recent price changes.

**Purpose:** To analyse cryptocurrency market performance, compare coins
by market capitalisation, monitor price movements, and build dashboards
or reports.

**Data format:** JSON (typically an array of cryptocurrency objects)\
**Currency:** USD (`vs_currency=usd`)\
**Sort order:** Market capitalisation, highest first
(`order=market_cap_desc`)\
**Records requested:** Up to 100 (`per_page=100`)\
**Page:** 1 (`page=1`)\
**Price-change periods requested:** 24 hours and 7 days
(`price_change_percentage=24h,7d`)

> Note: The API returns live market data. Values can change whenever the
> endpoint is requested. Some fields may be `null` when data is
> unavailable for a particular coin.

## 2. API Request Parameters

  -----------------------------------------------------------------------
  Parameter                   Value                 Description
  --------------------------- --------------------- ---------------------
  `vs_currency`               `usd`                 Returns prices and
                                                    market values in US
                                                    dollars.

  `order`                     `market_cap_desc`     Sorts
                                                    cryptocurrencies by
                                                    market capitalisation
                                                    in descending order.

  `per_page`                  `100`                 Requests up to 100
                                                    cryptocurrency
                                                    records per page.

  `page`                      `1`                   Retrieves the first
                                                    page of results.

  `price_change_percentage`   `24h,7d`              Requests price-change
                                                    percentage data for
                                                    the previous 24 hours
                                                    and 7 days.

  `authuser`                  `1`                   An additional query
                                                    parameter in the
                                                    supplied URL; it is
                                                    not a standard
                                                    CoinGecko market-data
                                                    parameter and is not
                                                    required by the
                                                    endpoint.
  -----------------------------------------------------------------------

## 3. Column / Field Descriptions

Each object in the API response represents one cryptocurrency. The
following fields are commonly returned by the `/coins/markets` endpoint.

  -------------------------------------------------------------------------------
  Column / Field                       Data Type           Description
  ------------------------------------ ------------------- ----------------------
  `id`                                 String              Unique CoinGecko
                                                           identifier for the
                                                           cryptocurrency. Useful
                                                           for identifying a coin
                                                           independently of its
                                                           name or ticker symbol.

  `symbol`                             String              Short ticker symbol of
                                                           the cryptocurrency,
                                                           such as `btc` or
                                                           `eth`.

  `name`                               String              Full name of the
                                                           cryptocurrency, such
                                                           as Bitcoin or
                                                           Ethereum.

  `image`                              String (URL)        URL of the
                                                           cryptocurrency's logo
                                                           or image.

  `current_price`                      Number              Latest available price
                                                           of one unit of the
                                                           cryptocurrency in the
                                                           selected currency (USD
                                                           in this request).

  `market_cap`                         Number              Total market value of
                                                           the cryptocurrency,
                                                           generally calculated
                                                           as current price
                                                           multiplied by
                                                           circulating supply.

  `market_cap_rank`                    Integer             Cryptocurrency's
                                                           ranking based on
                                                           market capitalisation.
                                                           A lower rank indicates
                                                           a larger market
                                                           capitalisation.

  `fully_diluted_valuation`            Number / Null       Estimated total market
                                                           value if the maximum
                                                           or fully diluted
                                                           supply were in
                                                           circulation, based on
                                                           the current price.

  `total_volume`                       Number              Total value of the
                                                           cryptocurrency traded
                                                           across tracked markets
                                                           during the last 24
                                                           hours, expressed in
                                                           USD.

  `high_24h`                           Number / Null       Highest recorded price
                                                           during the previous 24
                                                           hours.

  `low_24h`                            Number / Null       Lowest recorded price
                                                           during the previous 24
                                                           hours.

  `price_change_24h`                   Number / Null       Absolute price
                                                           difference over the
                                                           previous 24 hours, in
                                                           USD for this request.

  `price_change_percentage_24h`        Number / Null       Percentage change in
                                                           price over the
                                                           previous 24 hours.
                                                           Positive values
                                                           indicate an increase;
                                                           negative values
                                                           indicate a decrease.

  `market_cap_change_24h`              Number / Null       Absolute change in
                                                           market capitalisation
                                                           over the previous 24
                                                           hours.

  `market_cap_change_percentage_24h`   Number / Null       Percentage change in
                                                           market capitalisation
                                                           over the previous 24
                                                           hours.

  `circulating_supply`                 Number / Null       Estimated number of
                                                           coins currently
                                                           circulating in the
                                                           market.

  `total_supply`                       Number / Null       Total number of coins
                                                           that currently exist
                                                           or are expected to
                                                           exist, excluding coins
                                                           that have been
                                                           permanently removed
                                                           where applicable.

  `max_supply`                         Number / Null       Maximum number of
                                                           coins that can ever
                                                           exist, if a maximum
                                                           supply is defined.

  `ath`                                Number / Null       All-time-high price
                                                           recorded for the
                                                           cryptocurrency, in USD
                                                           for this request.

  `ath_change_percentage`              Number / Null       Percentage difference
                                                           between the current
                                                           price and the
                                                           all-time-high price.

  `ath_date`                           String (date-time)  Date and time when the
                                       / Null              cryptocurrency reached
                                                           its all-time-high
                                                           price.

  `atl`                                Number / Null       All-time-low price
                                                           recorded for the
                                                           cryptocurrency, in USD
                                                           for this request.

  `atl_change_percentage`              Number / Null       Percentage difference
                                                           between the current
                                                           price and the
                                                           all-time-low price.

  `atl_date`                           String (date-time)  Date and time when the
                                       / Null              cryptocurrency reached
                                                           its all-time-low
                                                           price.

  `roi`                                Object / Null       Return-on-investment
                                                           information, when
                                                           available. It may
                                                           contain `times`,
                                                           `currency`, and
                                                           `percentage`.

  `last_updated`                       String (date-time)  Date and time when
                                                           CoinGecko last updated
                                                           the market data for
                                                           that cryptocurrency.
  -------------------------------------------------------------------------------

### Additional price-change fields requested

Because the URL includes `price_change_percentage=24h,7d`, the response
can also include:

  ---------------------------------------------------------------------------------
  Column / Field                              Data Type          Description
  ------------------------------------------- ------------------ ------------------
  `price_change_percentage_24h_in_currency`   Number / Null      Price percentage
                                                                 change over 24
                                                                 hours in the
                                                                 selected quote
                                                                 currency (USD).

  `price_change_percentage_7d_in_currency`    Number / Null      Price percentage
                                                                 change over 7 days
                                                                 in the selected
                                                                 quote currency
                                                                 (USD).
  ---------------------------------------------------------------------------------

**Important:** CoinGecko API versions and plans can affect field
availability and naming. Confirm the actual JSON keys returned by your
request before finalising a cleaned dataset or Power BI model. Do not
assume every field will be populated for every cryptocurrency.

## 4. Nested Field: `roi`

The `roi` field is an object and may contain the following sub-fields:

  -----------------------------------------------------------------------
  Sub-field               Data Type               Description
  ----------------------- ----------------------- -----------------------
  `times`                 Number                  Investment return
                                                  multiple.

  `currency`              String                  Currency used for the
                                                  return calculation.

  `percentage`            Number                  Return on investment
                                                  expressed as a
                                                  percentage.
  -----------------------------------------------------------------------

If `roi` is `null`, ROI information is unavailable for that
cryptocurrency.

## 5. Important Business Terms

  ---------------------------------------------------------------------
  Term                               Description
  ---------------------------------- ----------------------------------
  Cryptocurrency                     A digital asset that uses
                                     cryptography and a distributed
                                     ledger or blockchain technology.

  Market Capitalisation              The estimated total market value
                                     of a cryptocurrency, commonly
                                     calculated as price × circulating
                                     supply.

  Trading Volume                     The total value of trades
                                     completed during a specified
                                     period; this endpoint reports the
                                     24-hour volume.

  Circulating Supply                 The number of coins currently
                                     available in the market.

  Total Supply                       The total number of coins
                                     currently created or issued,
                                     subject to the provider's supply
                                     methodology.

  Maximum Supply                     The maximum number of coins that
                                     can ever be created, if a limit
                                     exists.

  Fully Diluted Valuation (FDV)      An estimate of market value if the
                                     maximum or fully diluted supply
                                     were in circulation at the current
                                     price.

  All-Time High (ATH)                The highest price recorded for an
                                     asset.

  All-Time Low (ATL)                 The lowest price recorded for an
                                     asset.

  Price Change                       The difference in an asset's price
                                     between two points in time.

  Price Change Percentage            The relative price movement
                                     expressed as a percentage.
  ---------------------------------------------------------------------

## 6. Suggested Data Types for Analysis

When importing the JSON into Excel, Power BI, Python, or a database, the
following data types are generally appropriate:

-   **Text:** `id`, `symbol`, `name`, `image`, `ath_date`, `atl_date`,
    `last_updated`
-   **Whole number:** `market_cap_rank` (and counts, if any)
-   **Decimal number:** price, market capitalisation, volume, supply,
    valuation, and percentage fields
-   **Date/Time:** `ath_date`, `atl_date`, `last_updated`
-   **Nested record/object:** `roi`

Use a nullable type for fields that may contain `null`. Avoid converting
missing values to zero unless that is an intentional business rule; zero
and unavailable are not the same.

## 7. Data Quality and Preparation Notes

1.  **Check missing values:** Fields such as `max_supply`,
    `fully_diluted_valuation`, `high_24h`, `low_24h`, and ROI may be
    null.
2.  **Check duplicate records:** Use `id` as the preferred unique
    identifier for each cryptocurrency.
3.  **Standardise symbols:** Symbols are not guaranteed to be unique. Do
    not use `symbol` alone as a primary key.
4.  **Preserve precision:** Cryptocurrency prices can be very small, so
    avoid rounding values too early.
5.  **Handle timestamps:** Convert date-time fields to a consistent
    timezone, preferably UTC, before time-based analysis.
6.  **Validate units:** Price and market-value fields use the requested
    quote currency (USD here); supply fields represent coin units.
7.  **Refresh awareness:** This is live market data. Store a retrieval
    timestamp separately if you need to compare snapshots over time.
8.  **Treat percentage fields correctly:** A value such as `2.5` means a
    2.5% change, not 0.025%, unless your transformation explicitly
    converts it to a decimal fraction.

## 8. Suggested Analysis and Dashboard Metrics

This dataset can support the following analyses:

-   Top 10 or Top 100 cryptocurrencies by market capitalisation.
-   Current price comparison across cryptocurrencies.
-   Highest and lowest 24-hour price performers.
-   Highest and lowest 7-day price performers.
-   Market capitalisation distribution.
-   Trading volume comparison.
-   Circulating supply versus total or maximum supply.
-   ATH gap analysis to show how far current prices are below historical
    peaks.
-   Comparison of market capitalisation and 24-hour trading volume.

## 9. Limitations

-   The API response is a snapshot of market information at retrieval
    time, not a complete historical price series.
-   The first page contains up to 100 results based on the selected sort
    order; it does not represent every cryptocurrency listed on
    CoinGecko.
-   Some assets may have missing or unavailable values.
-   Market data may vary across exchanges and data providers.
-   This dataset is intended for analysis and learning; it should not be
    treated as investment advice.

## 10. Source

**Provider:** CoinGecko\
**Endpoint:** `/api/v3/coins/markets`\
**Documentation:** https://docs.coingecko.com/reference/coins-markets\
**API URL supplied for this project:**\
https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&price_change_percentage=24h,7d&authuser=1

## 11. Official API Response Reference

The field list and parameter descriptions in this dictionary are based
on CoinGecko's official Coins List with Market Data API documentation.
The API response may contain additional optional fields depending on
request parameters, API version, and plan.

Official reference: https://docs.coingecko.com/reference/coins-markets
