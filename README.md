# CryptoTGYM

[![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=plastic)](CONTRIBUTING.md)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg?style=plastic)](https://opensource.org/licenses/Apache-2.0)
![completion](https://img.shields.io/badge/completion%20state-90%25-blue.svg?style=plastic)

# A cryptocurrency-focused branch of Trading Gym (Python 3.x)

This is derived from a Python 3.x fork of https://github.com/Prediction-Machines/Trading-Gym. Just a hobby project.

Trading Gym is an open-source project for the development of reinforcement learning algorithms in the context of trading.

## Installation

`pip install tgym`

if you clone the project to local, run

`python setup.py install` or
`python setup.py develop`

We strongly recommend using virtual environments. A very good guide can be found at http://python-guide-pt-br.readthedocs.io/en/latest/dev/virtualenvs/.

## Installation notes:

`pip install` fails on Windows 7. Manual installation required. Make sure Keras is installed with Tensorflow backend before installing tgym. 

## The trading environment:
`TickTrading`
`TickTrading` is a trading environment with input bid/ask tick data, it is very useful to forex (currency) trading. Currently, the profit-taking and stop-loss are fixed. will work on these parameters are a part of action for better ML. There is workable DQN example under ./examples/dqn_agent.py  


`SpreadTrading`

`SpreadTrading` is a trading environment allowing to trade a *spread* (see https://en.wikipedia.org/wiki/Spread_trade). We feed the environment a time series of prices (bid and ask) for *n* different products (with a `DataGenerator`), as well as a list of *spread coefficients*. The possible actions are then buying, selling or holding the spread. Actions cannot be taken on one or several legs in isolation. The state of the environment is defined as: prices, entry price and position (whether long, short or flat).

![](https://media.giphy.com/media/l4FGI4K3kHnBfUoIE/giphy.gif)

## Create your own `DataGenerator`

To create your own data generator, it must inherit from the `DataGenerator` base class which can be found in the file 'tgym/core.py'. It consists of four methods. Only the private `_generator` method which defines the times series needs to be overridden. Example can be found at `examples/generator_random.py`. For only one product, the `_generator` method **must** yield a `(bid, ask)` tuple, one element at a time. For two or more products, you must return a tuple consisting of bid and ask prices for each product, concatenated. For instance for two products, the method should yield `(bid_1, ask_1, bid_2, ask_2)`. The logic for the time series is encoded there.

## Compatibility with OpenAI gym

Our environments API is strongly inspired by OpenAI Gym. We aim to entirely base it upon OpenAI Gym architecture and propose Trading Gym as an additional OpenAI environment.

## Examples

Some examples are available in `tgym/examples/`

To run the `dqn_agent.py` example, you will need to also install keras with `pip install keras`. By default, the backend will be set to Theano. You can also run it with Tensorflow by installing it with `pip install tensorflow`. You then need to edit `~/.keras/keras.json` and make sure `"backend": "tensorflow"` is specified.

## To Do List

1. Get the thing to work
    - [ ] a. Include .csv files to run examples
    - [ ] b. Possibly other stuff
    
2. Add Cryptocurrency functionality
    - [ ] a. Support for price feed APIs
    - [ ] b. Support for exchange trading APIs

## Reference Paper:
 1. [Human-level control through deep reinforcement
learning](https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf)
 2. [Double Q-Learning](https://arxiv.org/pdf/1509.06461.pdf)
 3. [Dueling Double Q-learning](https://arxiv.org/pdf/1511.06581.pdf)
 4. [A Deep Reinforcement Learning Framework for the
Financial Portfolio Management Problem]（https://arxiv.org/pdf/1706.10059.pdf）
 

