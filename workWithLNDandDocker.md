## General Workflow to recreate the BitcoinNetwork(Alice - Channel - Bob) and send a payment from Alice to Bob:

1) Create a ```btcd``` node running on a private ```simnet```
2) Create ```Alice```, one of the ```lnd``` nodes in our simulation network
3) Create ```Bob```, the other ```lnd``` node in our simulation network
4) Mine some blocks to send ```Alice``` some bitcoins
5) Open channel between ```Alice``` and ```Bob```
6) Send payment from ```Alice``` to ```Bob```
7) Close the channel between ```Alice``` and ```Bob```
8) Check that on-chain ```Bob``` balance was changed

Start ```btcd``` and then create an address for ```Alice``` that we'll directly mine bitcoin into

