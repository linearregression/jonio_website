Title: Placing your first Forex trade with Python
Tags: algotrading
Date: 2015-10-20 22:48

Time to talk about brokers, how to place a trade programmatically and most importantly how not to get scammed.

This is the third part of the series: [How to build your own algotrading platform](how-to-build-your-own-algorithmic-trading-platform.html).

A broker is nothing more than a company that lets you trade (buy or sell) assets on a market through their platform. What is very important for algotrading is: 

1. The broker offers an API in order for us to place orders
2. You can have a demo account to run your staging environment and experiment
3. The spread is as small as possible

In our case, we don't really care about spread as we won't be doing High Frequency Trading any time soon.

Even though brokers are regulated, there have been incidents in the past couple of years, were brokers folded due to certain conditions. Be *very* wary if 

1. There are no reviews of the broker on the internet (or most of them are bad)
2. If the broker offers you some crazy leverage (like 1:200)
3. If the broker seems to be in a very strange country


What could happen is that you start making some money and you aren't be able to pull them out. Seriously. Super stressful situation.

But let's switch to a happier note which is opening an account and placing our first programmatic trade. Whooha!

I am using [Oanda](http://www.oanda.com/) as a broker (I am not affiliated with them) and they offer a pretty decent API, libraries on github and a free demo account. 

Go and open a free [fxTrade Practice account](https://fxtrade.oanda.com/your_account/fxtrade/register/gate).

After you get your free demo account, go to your profile 
<img src="https://dl.dropboxusercontent.com/u/757245/jonio/oanda.png" />

and you can change your leverage (switch it to 50:1) and then go back to your **Manage API Access**. There you can find your API key which we are going to use in our system to place trades. **MAKE SURE YOU DON'T SHARE THIS KEY**.

The code for this is and all other posts is on my [github](https://github.com/jonromero/Forex-algotrading) and you can install it and run it pretty easily.

The code is straight-forward. We connect to Oanda, to a practice account with our token 

	:::python
 
	oanda = oandapy.API(environment="practice",
                       access_token=OANDA_ACCESS_TOKEN)
	response = oanda.get_prices(instruments="EUR_USD")
	prices = response.get("prices")
	buy_price = prices[0].get("bid")

and we are requesting the prices (bid/ask) for the pair EUR_USD. 

We print the buy price and then we place a *market* order. 

	:::python
	print "Buy at", buy_price
	trade_id = oanda.create_order(OANDA_ACCOUNT_ID,instrument="EUR_USD", units=1000,
                      side='buy',
                      type='market')


Super easy. Don't worry about what EURUSD is or how many units we are buying or what a market order is. For now, we have placed our first trade from our laptop and we are going to build our own API to place trades. Exciting stuff!

You can read Oanda's documentation [here](http://developer.oanda.com/) to see what else you can do with their API.

Coming up next, connecting to a real **LIVE** algotrading system, running from my RaspberryPI at home. 

<img src="https://dl.dropboxusercontent.com/u/757245/jonio/trades-nov.jpg" />

You'll be able to see the (almost) final program running and we'll talk more about Forex and strategies. 

If you have more feedback, ping me at [jonromero](http://www.twitter.com/jonromero) or signup to the [newsletter](http://eepurl.com/bGbOnb). 

Legal outro. This is an engineering tutorial on how to build an algotrading platform for experimentation and FUN. Any suggestions here are not financial advices. 
If you lose any (or all) you money because you followed any trading advices or deployed this system in production, you cannot blame this random blog (and/or me). Enjoy at your own risk. 


