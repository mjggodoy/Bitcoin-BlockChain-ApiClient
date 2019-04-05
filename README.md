# Bitcoin-BlockChain-ApiClient
This a JAVA api client for retrieving data from https://blockchain.info . It can be extended by any developers. The design of the client is very OOP. Enjoy it!

## Requirements

Building the API client library requires:
1. Java 1.7+
2. Maven

## Installation

To create the  api client library .jar, execute the following command:

### Manual Installation with Maven

The command below generates .jars, which can be manually included to your project.


```shell
mvn clean package
```

### Manual Installation in Local Repo

In order to add the api client dependency to your maven local repo, execute this command:

```shell
mvn clean install
```
Refer to the following link to include third parties libraries to yout maven local repository [How to include third parties libraries to your local mvn repository](https://www.mkyong.com/maven/how-to-include-library-manully-into-maven-local-repository/)

### Maven users

You can add this dependency to your pom.xml file:

```xml
<dependency>
  <groupId>com.github.mjggodoy</groupId>
  <artifactId>com.github.mjggodoy</artifactId>
  <version>0.0.1-SNAPSHOT</version>
</dependency>
```

## Getting Started

```java

public class ApiCallMain {

	public static void main(String[] args) throws IOException, ParseException {

		// Set parameters. In order to get the bitcoins transactions per second,
		// the parameters to include are
		// the timespan and the rollingAverage, which correspond to 5 weeks and
		// 8 hours, respectively.

		LinkedHashMap<String, String> params = new LinkedHashMap<String, String>();
		params.put("timespan", "5weeks");
		params.put("start", "1551444600");
		params.put("sampled", "true");
		params.put("rollingAverage", "8hours");
		params.put("format", "csv");
		
		Statistic statistic = new Statistic(params);
		Chart graphic = statistic.getResourcesTransactionPerSecond();
		
		// Retrieve charts (type=transaction per second).
		// No parameters

		String chartype2 = "transactions-per-second";
		Statistic statistic4 = new Statistic(chartype2);
		Chart graphic2 = statistic4.getResourcesTransaction();

		// The method getStats returns the summary of bitcoin statistics

		Statistic statistic2 = new Statistic();
		Stat stats = statistic2.getStats();
		

		// The method getPools() retrieves all the mining pools. In this case,
		// the parameter
		// is the timespan that corresponds to 5 days.

		LinkedHashMap<String, String> params2 = new LinkedHashMap<String, String>();
		params2.put("timespan", "5days");

		Statistic statistic3 = new Statistic(params2);
		Pool pool = statistic3.getPools();

		// The method getRateExchanges() returns the market prices for each
		// currency

		LinkedHashMap<String, LinkedHashMap<String, Object>> output3 = new LinkedHashMap<String, LinkedHashMap<String, Object>>();
		ExchangeRates exchange = new ExchangeRates();
		output3 = exchange.getRateExchanges();

		// The method getRateExchanges() returns the exchange rates currency X
		// -> bitcoin. The parameters to add are the currency (EUR)
		// and its value. The method returns a float with the ratio of the
		// exchange.

		LinkedHashMap<String, String> params4 = new LinkedHashMap<String, String>();
		params4.put("currency", "EUR");
		params4.put("value", "5000");
		ExchangeRates exchange2 = new ExchangeRates(params4);
		Rate rate = exchange2.getBitcoinExchange();
		

		// Get information from a block with a specific hash

		String hash = "0000000000000bae09a7a393a8acded75aa67e46cb81f7acaa5ad94f9eacd103";
		BlockChainData blockchain = new BlockChainData(hash);
		Block block = blockchain.getBlockDataInformation();

		// Some examples about how to extract from block of the blockchain i ->
		System.out.println("Previous block " + block.getPrev_block());
		System.out.println("Next block " + block.getNext_block().toString());
		System.out.println("Transactions " + block.getTx().toString());
		System.out.println("Block" + block.toString());
		

		// Get information from a single transaction by providing the hash

		String hashTransaction = "b6f6991d03df0e2e04dafffcd6bc418aac66049e2cd74b80f14ac86db1e3f0da";
		BlockChainData trasnsactionBlock = new BlockChainData(hashTransaction);
		TransactionData transactionData = trasnsactionBlock.getTransactionData();
		
		///Retrieve information from a block given its height
		String height = "154595";
		LinkedHashMap<String, String> paramsHeight = new LinkedHashMap<String, String>();
		paramsHeight.put("format", "json");
		BlockChainData trasnsactionBlockHeight = new BlockChainData(paramsHeight, height);
		ArrayList<Block> listBlocks = trasnsactionBlockHeight.getBlockInformationfromHeight();
		
		//Retrieve information about a bitcoing given its address
		String address = "1AJbsFZ64EpEfS5UAjAfcUG8pH8Jn3rn1F";
		BlockChainData bitcoinAddress = new BlockChainData(address);
		BitcoinInfo bitcoinInfo = bitcoinAddress.getBitcoinInformationFromAddress();
		
		//Get bitcoin's information from multiple addresses
		LinkedHashMap<String, String> paramsAdresses = new LinkedHashMap<String, String>();
		paramsAdresses.put("active", "1A8JiWcwvpY7tAopUkSnGuEYHmzGYfZPiq|1MDUoxL1bGvMxhuoDYx6i11ePytECAk9QK");
		BlockChainData bitcoinTwoAddress = new BlockChainData(paramsAdresses);
		ArrayList<Object> multipleAddresses = bitcoinTwoAddress.getBitcoinsMultipleAddresses();
		
		//Get information about the unspent outputs
		LinkedHashMap<String, String> paramsAdressOutputs = new LinkedHashMap<String, String>();
		paramsAdressOutputs.put("active","1MDUoxL1bGvMxhuoDYx6i11ePytECAk9QK");
		BlockChainData outputSpent = new BlockChainData(paramsAdressOutputs);
		ArrayList<UnspentOutput> unspentOutputList = outputSpent.getUnspentOutputs();

		//Get information about the balance
		LinkedHashMap<String, String> paramsBalance = new LinkedHashMap<String, String>();
		paramsBalance.put("active","1MDUoxL1bGvMxhuoDYx6i11ePytECAk9QK|1A8JiWcwvpY7tAopUkSnGuEYHmzGYfZPiq");
		BlockChainData balance = new BlockChainData(paramsBalance);
		ArrayList<Balance> balanceList = balance.getBalance();
		
		//Get information about the latest block
		BlockChainData latestBlock = new BlockChainData();
		Block lastblock = latestBlock.getLastBlock();
		
		//Get unconfirmed transactions
		LinkedHashMap<String, String> paramsTransactions = new LinkedHashMap<String, String>();
		paramsTransactions.put("format","json");
		BlockChainData transactions = new BlockChainData(paramsTransactions);
		ArrayList<Transaction>unconfirmedTransactions = transactions.getUnconfirmedTransactions();
		
		//Get blocks from a specific pool (e.g., Bitclub Network)
		LinkedHashMap<String, String> paramsPools = new LinkedHashMap<String, String>();
		paramsPools.put("format","json");
		String poolName =  "BitClub%20Network";
		BlockChainData blockPool = new BlockChainData(paramsPools, poolName);
		ArrayList<Block> blocks = blockPool.getBlocksfromParameter();
		
		//Get blocks from a specific pool (e.g., Bitclub Network)
		LinkedHashMap<String, String> paramsTime = new LinkedHashMap<String, String>();
		paramsTime.put("timespan", "1day");
		paramsTime.put("format","json");
		BlockChainData blockChain = new BlockChainData(paramsTime);
		ArrayList<Block> blocksfromASpecificTime = blockChain.getBlocksfromParameter();

	}
```

## API documentation

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*Chart* | **getResourcesTransactionPerSecond()** | **GET** | This method retrieves the number of daily bitcoins transactions. The parameters to include are: 1) timespan or duration of the chart, 2) rollingAverage or duration over which the data should be averaged, 3) start or the datatime when the chart starts (optional), 3) the format that is in JSON, 4) Sample that limits the number of points.
*Stat* | **getStats()** | **GET** | This method retrieves the stats which refer to a summary of blocks and transactions. For example, the hash rate, the total fees, the total number of transactions or mined blocks.
*Pool* | **getPools()** | **GET** | This method retrieves information about the mining pools.
*Rate* | **getBitcoinExchange()** | **GET** | This method retrieves the value of the currency in bitcoins.
*Block* | **getBlockDataInformation()** | **GET** | This method provides the information related to a block matching with its corresponding hash.
*TransactionData* | **getTransactionData()** | **GET** | This method provides the information from a single transaction with a given hash.
*Chart* | **getResourcesTransaction()** | **GET** | This method retrieves the transactions regarding the parameter chart type that was specified.
*Block* | **getBlockInformationfromHeight()** | **GET** | This method retrieves an array of one or more blocks at the height specified as parameter.
*BitcoinInfo* | **getBitcoinInformationFromAddress()** | **GET** | This method retrieves bitcoin information from a specified address.
*AddressBitcoin*, *Wallet*, *Transaction* | **getBitcoinsMultipleAddresses()** | **GET** | This method retrieves bitcoin information (List of AddressBitcoin, Wallet, Transaction) putting as parameter multiple addresses.
*UnspentOutput* | **getUnspentOutputs()** | **GET** | This method retrieves information (List of UnspentOutput) about the unspent outputs by providing as parameter the address.
*Block* | **getLastBlock()** | **GET** | This method returns the last generated block of a blockchain. 
*Transaction* | **getUnconfirmedTransactions()** | **GET** | This method returns all the unconfirmed transactions. 
*Block* | **getBlocksfromParameter()** | **GET** | This method returns the blocks generated for a day or a specific pool (e.g., putting as parameters 1day or BitClub%20Network as mining pool, respectively)




