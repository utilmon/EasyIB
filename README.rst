EasyIB: Python Wrapper for Interactive Brokers API
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

.. figure:: https://raw.githubusercontent.com/ashpipe/EasyIB/main/docs/logo.png
    :width: 400
    :align: center
    
"Logo for 'EasyIB'" according to Midjourney

|
|   EasyIB is an unofficial python wrapper for `Interactive Brokers Client Portal Web API <https://interactivebrokers.github.io/cpwebapi/>`__. The motivation for the project was to build a Python wrapper that can run on Linux/cloud environments. Thus, Client Portal API was preferred over Trader Workstation (TWS) API.

Please see https://easyib.readthedocs.io for the full documentation.

Features
---------
Notable functionality includes:

* Pull account info, portfolio, cash balance, the net value
* Pull historical market data
* Submit, modify, cancel orders
* Get order status, list of live orders
* Ping (tickle) server, get authentication status, re-authenticate

How to install
--------------

EasyIB assumes a gateway session is active and authenticated.
Follow instructions at https://interactivebrokers.github.io/cpwebapi/ for authentication.
A custom package such as `Voyz/IBeam <https://github.com/voyz/ibeam>`__ can also be used for setting up an active session.
Part Time Larry has an excellent youtube tutorial on this topic: https://www.youtube.com/watch?v=O1OhiiCx6Ho.

EasyIB was developed under the Voyz/Ibeam docker image environment.

Once a gateway session is running, ``pip`` command can be used to install EasyIB:

.. code-block:: bash

    pip install easyib

Quick start
------------
Historical data
^^^^^^^^^^^^^^^^

.. code-block:: python

    import easyib

    ib = easyib.REST()

    bars = ib.get_bars("AAPL", period="1w", bar="1d")
    print(bars)

Submitting an order
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    list_of_orders = [
        {
            "conid": ib.get_conid("AAPL"),
            "orderType": "MKT",
            "side": "BUY",
            "quantity": 7,
            "tif": "GTC",
        }
    ]
    
    order = ib.submit_orders(list_of_orders)
    print(order)


Reference
-------------
For the complete reference, please visit https://easyib.readthedocs.io/en/latest/reference.html.

REST
^^^^^
By default, EasyIB assumes the gateway session is open at https://localhost:5000 without an SSL certificate. A custom URL and SSL certificate can be set by:

.. code-block:: python

    ib = easyib.REST(url="https://localhost:5000", ssl=False)

API REST Methods
^^^^^^^^^^^^^^^^^
Documentation of available functions is at https://easyib.readthedocs.io/en/latest/reference.html.

See the official documentation of the End Point at https://www.interactivebrokers.com/api/doc.html.

.. list-table:: 
   :widths: 50 50 25
   :header-rows: 1

   * - REST Method
     - End Point
     - Result
   * - ``get_accounts()``
     - ``Get portfolio/accounts``
     - ``list``
   * - ``switch_account(accountId: str)``
     - ``Post iserver/account/{accountId}``
     - ``dict``
   * - ``get_cash()``
     - ``Get portfolio/{accountId}/ledger``
     - ``float``
   * - ``get_netvalue()``
     - ``Get portfolio/{accountId}/ledger``
     - ``float``
   * - ``get_conid(symbol: str, instrument_filters: Dict, contract_filters: Dict = {"isUS": True})``
     - ``Get trsv/stocks``
     - ``int``
   * - ``get_fut_conids(symbol: str)``
     - ``Get trsv/futures``
     - ``list``
   * - ``get_portfolio()``
     - ``Get portfolio/{accountId}/positions/0``
     - ``dict``
  
   * - ``reply_yes(id: str)``
     - ``Post iserver/reply/{id}``
     - ``dict``

   * - ``submit_orders(list_of_orders: list, reply_yes=True)``
     - ``Post iserver/account/{acountId}/orders``
     - ``dict``

   * - ``get_order(orderId: str)``
     - ``Get iserver/account/order/satus/``
     - ``dict``

   * - ``get_live_orders(filters=None)``
     - ``Get iserver/account/orders``
     - ``dict``

   * - ``cancel_order(orderId: str)``
     - ``Delete iserver/account/{accountId}/order/{orderId}``
     - ``dict``

   * - ``modify_order(orderId=None, order=None, reply_yes=True)``
     - ``Post iserver/account/{accountId}/order/{orderId}``
     - ``dict``

   * - ``get_bars(symbol: str, period="1w", bar="1d", outsideRth=False, conid="default")``
     - ``Get iserver/marketdata/history``
     - ``dict``

   * - ``ping_server()``
     - ``Post tickle``
     - ``dict``
   * - ``get_auth_status()``
     - ``Post iserver/auth/status``
     - ``dict``
   * - ``re_authenticate()``
     - ``Post iserver/reauthenticate``
     - ``None``
   * - ``log_out()``
     - ``Post logout``
     - ``None``

