EasyIB: Unofficial Wrapper for Interactive Brokers API
======================================================

.. image:: https://img.shields.io/pypi/v/easyib
    :target: https://pypi.org/pypi/easyib/
.. image:: https://img.shields.io/pypi/pyversions/easyib
    :target: https://pypi.org/pypi/easyib/
.. image:: https://img.shields.io/pypi/l/easyib
    :target: https://pypi.org/pypi/easyib/
.. image:: https://readthedocs.org/projects/easyib/badge/?version=latest
    :target: https://easyib.readthedocs.io/en/latest/?badge=latest
    :alt: Documentation Status


|
|   EasyIB is an unofficial python wrapper for `Interactive Brokers Client Portal Web API <https://interactivebrokers.github.io/cpwebapi/>`__.

Features
---------
Notable functionality includes:

* Pull account info, portfolio, cash balance, net value
* Pull market historical data
* Submit, modify, cancel orders
* Get order status, list of live orders
* Ping (tickle) server, get authentication status, re-authenticate

How to install
--------------
.. code-block:: bash

    pip install easyib

EasyIB assumes a gateway session is active and authenticated.
Follow instructions at https://interactivebrokers.github.io/cpwebapi/ for authentication.
A custom package such as `Voyz/IBeam <https://github.com/voyz/ibeam>`__ can be also used for setting up an active session.

Quick start
------------
Historical data

.. code-block:: python

    import easyib

    api = easyib.REST()

    bars = api.get_bars("AAPL", period="1w", bar="1d")
    print(bars)

Submitting an order

.. code-block:: python

    list_of_orders = [
        {
            "conid": api.get_conid("AAPL"),
            "orderType": "MKT",
            "side": "BUY",
            "quantity": 7,
            "tif": "GTC",
        }
    ]
    
    api.submit_orders(list_of_orders)
