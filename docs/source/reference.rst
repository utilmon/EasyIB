Reference
==================

Reference for easyib.REST class.

.. currentmodule:: easyib
.. autoclass:: REST

Account info
-----------------
.. automethod:: REST.get_accounts
.. automethod:: REST.switch_account
.. automethod:: REST.get_portfolio
.. automethod:: REST.get_cash
.. automethod:: REST.get_netvalue

Instrument info
-----------------
.. automethod:: REST.get_conid
.. automethod:: REST.get_fut_conids
.. automethod:: REST.get_bars


Orders
----------
.. automethod:: REST.submit_orders
.. automethod:: REST.modify_order
.. automethod:: REST.cancel_order
.. automethod:: REST.get_order
.. automethod:: REST.get_live_orders
.. automethod:: REST.reply_yes


Communication with server
--------------------------
.. automethod:: REST.ping_server
.. automethod:: REST.get_auth_status
.. automethod:: REST.re_authenticate
.. automethod:: REST.log_out
