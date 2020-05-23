# GATH
gath is the central SW to run an own node. There are a lot of options for gath
as specified when You run

    gath -help
    
when running gath as an own node please be aware that there are a lot of people
trying to harvest Your Atheios. So when You setup Your own node, make sure
You do not expose RPC to the internet.

You can prevent that by

* having a firewall like ufw up and running and disable the 8545 port 
* define all rpc connections as local  


    gath --rpc --rpcaddr 127.0.0.1 --rpccorsdomain http://localhost --rpcapi personal,db,eth,net,web3 --syncmode=full  
    
    
would only allow local connections.

