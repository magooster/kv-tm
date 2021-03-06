## kv-tm: KeyVault Transaction manager for use with Web3j

## Features



## Maven

TBD

## Gradle

TBD

## Prerequisites

Azure key vault with an Azure Service Principal or Managed Identity with get and sign permissions to the respective key vault.

When using Azure Managed Identity - AzureCryptoClient will leverage the DefaultAzureCredential

Alternately set the following environment variables

AZURE_CLIENT_ID = (appId),
AZURE_CLIENT_SECRET = (password),
AZURE_TENANT_ID = (tenant)

For development can leverage the Azure cli to generate credentials

## Usage

Web3j web3j = Web3j.build(new HttpService("http://localhost:8545"));

KeyVaultClient kvc = new AzureCryptoClient("https://mykeyvault.vault.azure.net/keys/keyname/keyversion");

KeyVaultTransactionManager transactionManager = new KeyVaultTransactionManager(web3j, kvc, chainId);

## Sending Raw Transactions

Use the KeyVaultTransactionManager signAndSend method

RawTransaction rawTransaction = ...
EthSendTransaction ethSendTransaction = transactionManager.signAndSend(rawTransaction);

## Signing Raw transactions

Use the KeyVaultTransactionManager sign method

RawTransaction rawTransaction = ...
EthSendTransaction ethSendTransaction = transactionManager.sign(rawTransaction);

## Smart Contract Wrappers

Smart contract wrappers generated using web3j work out the box.

The only difference is that you'll need to use one of the KeyVaultTransactionManager:

YourSmartContract contract = YourSmartContract.deploy(
    <web3j>, transactionManager, GAS_PRICE, GAS_LIMIT,
    <param1>, ..., <paramN>).send();

## Warning

This is very much work-in-progress so should only be use for guidance or testing   