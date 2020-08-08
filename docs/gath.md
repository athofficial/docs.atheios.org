# GATH - The go-lang implementation of Atheios
gath is the central SW to run an own node. There are a lot of options for gath
as specified when you run

    gath -help
    
when running gath as an own node please be aware that there are a lot of people
trying to harvest Your Atheios. So when you setup your own node, make sure
you do not expose RPC to the internet.

You can prevent that by

* having a firewall like ufw up and running and disable the 8545 port 
* define all rpc connections as local  


    gath --rpc --rpcaddr 127.0.0.1 --rpccorsdomain http://localhost --rpcapi personal,db,eth,net,web3 --syncmode=full  
    
    
would only allow local connections.

There is a lot of inormation available which also applies to gath from the ethereum project. Checkout  their documentation at

* [Ethereum WIKI](https://geth.ethereum.org/docs/getting-started)

## Useful functions
When You are running a local version of gath You are mining. Over time You will have some Atheios mined and
You will be able to retrieve the value with the following command:

    geth attach http://127.0.0.1:8545

### How much has been mined
This command allows You to attach to a running instance of gath. Make sure You have a running instance though.
In the console You can then issue the following command:

    > web3.fromWei(eth.getBalance(eth.coinbase), "ether")
    6.5
    
This should how much has been mined sofar.

### Get all accounts and balances
For this we first write a small function and save it locally:


    function checkAllBalances() {
        var totalBal = 0;
        for (var acctNum in eth.accounts) {
            var acct = eth.accounts[acctNum];
            var acctBal = web3.fromWei(eth.getBalance(acct), "ether");
            totalBal += parseFloat(acctBal);
            console.log("  eth.accounts[" + acctNum + "]: \t" + acct + " \tbalance: " + acctBal + " ether");
        }
        console.log("  Total balance: " + totalBal + " ether");
    };

Let's assume we stored it under the following path:

    vi /home/fdm/balance.js
    
Now we just need to load the function when being attached to the gath concol

    geth attach http://127.0.0.1:8545
    
Then in the console:

    > loadScript("/home/fdm/balance.js")
    true
    
Now we just call the function

    > checkAllBalances();
      eth.accounts[0]:      0xb78f905a61f390a3d232a149806816ebbf7e0899      balance: 296.08295988 ether
      eth.accounts[1]:      0xe2428284687db3355b64262088d84b941b73a389      balance: 0.0100001 ether
      eth.accounts[2]:      0x2e28b65fd67e31d08b230761723cdbd0d59cb4f8      balance: 0 ether
      eth.accounts[3]:      0xbbd1bb38292fb49cefef8c55d80bfd18aab34ee6      balance: 0 ether
      eth.accounts[4]:      0x73c6ef7b610ffd30ea4d873fe90924f3da6e678d      balance: 0 ether
      eth.accounts[5]:      0xe7d9a2bee10bf7aaa4dee5471c22e2e3c714ee9a      balance: 49.99958 ether
        ...
      eth.accounts[42]:     0x8fa9e5bc7f06059b6cb0efb474d1ba1d5eb10353      balance: 0 ether
      eth.accounts[43]:     0xac5f98003b397d46ccbe3023d1639949f72a1ab9      balance: 0 ether
      eth.accounts[44]:     0x0ad57e51a0a8c18798eb8904f26b10031cbb0079      balance: 0 ether
      Total balance: 375.2978199999999 ether



    
