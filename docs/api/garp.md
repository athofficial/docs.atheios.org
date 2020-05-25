# The GARP protocol

We have designed a game resolution protocol (GARP) on top of websocket. This 
protocol does all the game resolution handling.
The endpoint of that protocol is wss.atheios.org. From there You might be directed to other domains
from a load distribution perspective.

## The details
The communication is done via json and can be done in any language. We have developed supporting 
modules in order to simplify the integration. 

Here we focus though on the protocol itself.

A word of warning: we are in a very early stage of API development, so there will 
be significant changes over time.

Currently we are in version 0.1.4. We are using the following definitions:

* Alpha stage: version below 0.5.0:  
Compatibility breaking changes can happen, though we try to minimize it
* Beta stage version: below 1.0.0:  
    Smaller changes potential compatibility breaking changes are prevented.
* Release versions like 1.x.x, 2.x.x etc:  
    In this stage we keep compatibility. New releases are published well ahead and 
    test pools are provided for early integration
    
There will be a live server which will contain the production environment which
started with wss.atheios.org.

Then there will be a staging server which will contain the next version of the
framework. Once the version is deemed to be production, we will switch that version 
over. The staging server will be called wss-test.atheios.org.

The next version of the SW will be called 0.1.5 and is available now.

* [GARP V1.4.0](/garp_v140/)    
* [GARP V1.5.0](/garp_v150/)    

