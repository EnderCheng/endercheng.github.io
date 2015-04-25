---
layout: minimal_post
title: Registering a .bit domain with namecoin. 
published: true 
comments: true
introduction: A DNS type service
---

Before you do anything, you should probably go and read about [namecoin](http://namecoin.info).
To cut a long story short, namecion is basically a decentralized (no one mother or root single copy) dictionary of key/value pairs which are synced using the same principals that enable bitcion mining/transactions and so on.
The key (your domain name, example.bit) holds the value which specifies the location of your server, its IP address and other pieces of metadata.
The current draft specification for this `.bit` TLD scheme is [here](http://dot-bit.org/Namespace:Domain_names_v2.0).
You should know that a number of [namespaces](http://dot-bit.org/Namespace) are present under the `.bit` umbrella, `d/<domain>` for domain names, `id/<your name>` for online identifications and so on - all of which are stores of key/value pairs. 

## Acquire NMC
In order to register a key/value pair a fee of 0.01 NMC is payable.
[Where do you get namecoins from](http://dot-bit.org/HowToGetNamecoins)?
You get some given to you, buy them, or mine them; I bought some on an [exchange](https://btc-e.com) for BTC.
So this is where we begin - NMC in a wallet on some exchange.

## Installation
Here I reproduced some of the content found [on the namecoin wiki](https://github.com/namecoin/namecoin/wiki/Install-and-Configure-Namecoin), for operating systems other than Linux, you will also find the relevant information.

Download and extract the most current version:

    wget -O /tmp/namecoin.tgz http://dot-bit.org/files/namecoin_linux`getconf LONG_BIT`.tgz
    tar xfz /tmp/namecoin.tgz -C ~/usr/local/bin/

Setup a default configuration:

    mkdir ~/.namecoin && \
    echo "rpcuser=`whoami` \n\
    rpcpassword=`openssl rand -hex 20` \n\
    rpcport=8336" > ~/.namecoin/namecoin.conf

That is it.
Running namecoin as below will automatically create a new (and empty) wallet on your machine.

    ./namecoind -daemon

If this is the first time you have ever run namecoin you will have to wait a while (maybe an hour?) for a local copy of the blockchain to be populated.
Have a look at the [namecoin block explorer](http://explorer.dot-bit.org/) to find out the ID for the latest block.
You can compare this to the block reported by the namecoin daemon you are running locally:

    ./namecoind getinfo

If the 'blocks' field is the same as the current block ID reported on the explorer, you are up-to-date.

## Depositing NMC to your wallet
Ok, you have a wallet. What is its address?
Assuming the daemon is running, this will return the address (and NMC balance) for your wallet:

    ./namecoind listreceivedbyaddress 0 true

The address field (a string starting with 'N') is what you need to know.
Generally the exchange or online wallet you are using will have some sort of  withdrawal functionality.
Specify now much NMC you want to transfer, and provide the address of your local wallet.
Wait for a few confirmations of your transfer to occur, and eventually the previous command will show you have an NMC balance greater than zero (in fact what ever the amount you sent to your wallet was).

## Registering your domain name
Now we have NMC to spend, you are ready to follow the [instructions on the namecoin wiki](https://github.com/namecoin/namecoin/wiki/How-to-register-and-configure-.bit-domains).
First check the availability of your desired domain name using a [search tool](http://dot-bit.org/tools/domainSearch.php).
If the name you want is free (where d/ indicates you are trying to register a key/value pair in the domain namespace, or id/ for the identification namespace for example):

    ./namedcoind name_new d/<the name you want>

This will return a long and short hex string.
Wait at least 12 blocks (according to the official wiki), then you can register the details of your domain.
After you do this, you will be the owner of the key/value pair, not before.

    ./namecoind name_firstupdate d/<the name you want> <short hex string> '{"ip": "<server IP>", "email": "<optional email>", "map": {"": "<server IP>", "www": "<server IP>"}}'

The 'map' field is used to specify subdomain information.
That is all there is to it.
You may also like to register a public identification in the id/ namespace:

    ./namecoind name_new id/<your name>
    ./namecoind name_firstupdate  id/<your name> <short hex string> '{"email": "<email address>", "bitcoin": "<bitcoin accress>", "litecoin": "<litecoin address>"}'

You can pretty much put what ever information you want into this namespace, enabling others to find you.

## Browsing .bit domains
There are a few proxies and DNS type servers available to help you resolve .bit addresses.
You can find out more about this [here](http://dot-bit.org/How_To_Browse_Bit_Domains). 

On a final note, if you do not care about owning the key/value pair directly, you can [use a registrar](http://dot-bit.org/HowToRegisterAndConfigureBitDomains#Register_a_domain_with_a_registrar).

