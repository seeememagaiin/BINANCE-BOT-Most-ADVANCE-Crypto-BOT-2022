<h2 align="center">⭐️BINANCE-BOT-Most-ADVANCE-Crypto-BOT-2022 (WINDOWS LINUX MAC)⭐️</h2>
 
<h4 align="center">⭐️ DO YOU TIRED OF BEAR MARKET ? USE BOTS FOR 24H TRADES ⭐️</h4>

<h4 align="center">⭐️ This is an experimental bot for auto trading the binance.com exchange with Notifications ⭐️</h4>
 
 
 
![Screenshot](https://cryptocoinname.com/wp-content/uploads/2022/01/1641497870_maxresdefault-768x432.jpg)

### Notifications with Apprise

Apprise allows the bot to send notifications to all of the most popular notification services available such as: Telegram, Discord, Slack, Amazon SNS, Gotify, etc.

To set this up you need to create a apprise.yml file in the config directory.

There is an example version of this file to get you started.

If you are interested in running a Telegram bot, more information can be found at [Telegram's official documentation](https://core.telegram.org/bots).

# binance-trade-bot
> Automated cryptocurrency trading bot


The way the bot takes advantage of the observed behaviour is to always downgrade from the "strong" coin to the "weak" coin, under the assumption that at some point the tables will turn. It will then return to the original coin, ultimately holding more of it than it did originally. This is done while taking into consideration the trading fees.


The bot jumps between a configured set of coins on the condition that it does not return to a coin unless it is profitable in respect to the amount held last. This means that we will never end up having less of a certain coin. The risk is that one of the coins may freefall relative to the others all of a sudden, attracting our reverse greedy algorithm.


## Tool Setup

### Install Python dependencies

Run the following line in the terminal: `pip install -r requirements.txt`.

### Configuration

1. [Signup](https://www.binance.com/) for Binance
2. Go API Center, [Create New](https://www.binance.com/) Api Key

5. Get an API and Secret Key, insert into `user.cfg`

**The configuration file consists of the following fields:**

-   **api_key** - Binance API key generated in the Binance account setup stage.
-   **api_secret_key** - Binance secret key generated in the Binance account setup stage.
-   **current_coin** - This is your starting coin of choice. This should be one of the coins from your supported coin list. If you want to start from your bridge currency, leave this field empty - the bot will select a random coin from your supported coin list and buy it.
-   **bridge** - Your bridge currency of choice. Notice that different bridges will allow different sets of supported coins. For example, there may be a Binance particular-coin/USDT pair but no particular-coin/BUSD pair.
-   **tld** - 'com' or 'us', depending on your region. Default is 'com'.
-   **hourToKeepScoutHistory** - Controls how many hours of scouting values are kept in the database. After the amount of time specified has passed, the information will be deleted.
-   **scout_sleep_time** - Controls how many seconds are waited between each scout.
-   **use_margin** - 'yes' to use scout_margin. 'no' to use scout_multiplier.
-   **scout_multiplier** - Controls the value by which the difference between the current state of coin ratios and previous state of ratios is multiplied. For bigger values, the bot will wait for bigger margins to arrive before making a trade.
-   **scout_margin** - Minimum percentage coin gain per trade. 0.8 translates to a scout multiplier of 5 at 0.1% fee.
-   **strategy** - The trading strategy to use. See [`binance_trade_bot/strategies`](binance_trade_bot/strategies/README.md) for more information
-   **buy_timeout/sell_timeout** - Controls how many minutes to wait before cancelling a limit order (buy/sell) and returning to "scout" mode. 0 means that the order will never be cancelled prematurely.
-   **scout_sleep_time** - Controls how many seconds bot should wait between analysis of current prices. Since the bot now operates on websockets this value should be set to something low (like 1), the reasons to set it above 1 are when you observe high CPU usage by bot or you got api errors about requests weight limit.

#### Environment Variables

All of the options provided in `user.cfg` can also be configured using environment variables.

```
CURRENT_COIN_SYMBOL:
SUPPORTED_COIN_LIST: "XLM TRX ICX EOS IOTA ONT QTUM ETC ADA XMR DASH NEO ATOM DOGE VET BAT OMG BTT"
BRIDGE_SYMBOL: USDT
API_KEY: vmPUZE6mv9SD5VNHk4HlWFsOr6aKE2zvsw0MuIgwCIPy6utIco14y7Ju91duEh8A
API_SECRET_KEY: NhqPtmdSJYdKjVHjA7PZj4Mge3R5YNiP1e3UZjInClVN65XAbvqqM6A7H5fATj0j
SCOUT_MULTIPLIER: 5
SCOUT_SLEEP_TIME: 1
TLD: com
STRATEGY: default
BUY_TIMEOUT: 0
SELL_TIMEOUT: 0
```

### Paying Fees with BNB
You can [use BNB to pay for any fees on the Binance platform](https://www.binance.com/en/support/faq/115000583311-Using-BNB-to-Pay-for-Fees), which will reduce all fees by 25%. In order to support this benefit, the bot will always perform the following operations:
-   Automatically detect that you have BNB fee payment enabled.
-   Make sure that you have enough BNB in your account to pay the fee of the inspected trade.
-   Take into consideration the discount when calculating the trade threshold.


### Run

```shell
python -m binance_trade_bot
```

### Docker

The official image is available [here](https://hub.docker.com/r/edeng23/binance-trade-bot) and will update on every new change.

```shell
docker-compose up
```

If you only want to start the SQLite browser

```shell
docker-compose up -d sqlitebrowser
```

## Backtesting

You can test the bot on historic data to see how it performs.

```shell
python backtest.py
```

Feel free to modify that file to test and compare different settings and time periods

## Developing

To make sure your code is properly formatted before making a pull request,
remember to install [pre-commit](https://pre-commit.com/):

```shell
pip install pre-commit
pre-commit install
```

The scouting algorithm is unlikely to be changed. If you'd like to contribute an alternative
method, [add a new strategy](binance_trade_bot/strategies/README.md).
