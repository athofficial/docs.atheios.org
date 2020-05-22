# The websocket protocol for games

We have designed a gaming protocol on top of websocket. This protocol does all the game resul handling.
The endpoint of that protocol is wss.atheios.org. From there You might be directed to other domains
from a load distribution perspective.

## The details
The communication is done via json and can be done in any language. We have developed supporting 
modules in order to simplify the integration. 

Here we focus though on the protocol itself.

A word of warning: we are in a very early stage of API development, so there will 
be significant changes over time.

Currently we are in version 0.1.4. We are using the following definitions:

* Alpha stage: version below 0.5.0
    Compatibility breaking changes can happen, though we try to minimize it
* Beta stage version: below 1.0.0:
    Smaller changes potential compatibility breaking changes are prevented.
* Release versions like 1.x.x,2.x.x etc
    In this stage we keep compatibility. New releases are published well ahead and 
    test pools are provided for early integration
    
## Game authentication: AuthenticatedConnectRequest
### Availablility:  
from 0.1.4

### Functionality:  
This function is a mandatory start of all communication with the websocket.
It is invoked with a websocket address url constructed in the following way:

    url="wss://wss.atheios.org/ws/<GAMETOKEN>/<PROTOCOLID>"
where 

    <GAMETOKEN> Tokenid from portal.atheios.org
    <PROTOCOLID> Protocol id

Once that has happened there will be a a back and forth communication
ensuring that the game is authenticated. If the communication is successful
the wss protocol will reply a session ID which is stored as a state.

### Successful case:  
The case is successful when wss returns a session ID

    {
    	"@class": ".AuthenticatedConnectResponse",
    	"requestId": "0",
    	"sessionId": "Guwui-r7H4P-G7pNg-4p7OU-3rzth"
    }


### Error cases:  
A single error case can occure, when the <GAMETOKENID> cannot be found.

    {
    	"@class": ".AuthenticatedConnectResponse",
    	"error": "Unknown GameID ",
    	"requestId ": "0"
    }

## Authenticate user: 
Availablility:  
from 0.1.4

### Functionality:  
This request sends user credentials for validation by the portal.

### Request
The websocket message sent jas the following JSON format:

    {
    	"@class": ".AuthenticationRequest",
    	"username": "<USERNAME>",
    	"userpass": "<USERPASSWORD>",
    	"apikey": "<GAMETOKENID>",
    	"requestId": "1590177530798_1"
    }
    
### Successful case:  
The successful response is rendered according to the following:

    {
      "@class" : ".AuthenticationResponse",
      "authToken" : "Qt4pzdX3JQtM8kZwFUjWoZ5d",
      "displayName" : "Lars",
      "newPlayer" : false,
      "userId" : "3",
      "gameId" : "27",
      "wage" : "1",
      "requestId" : "1590177530798_1"
    }
    
The response provides essential information for the game as the display name, userId, 
gameId and the wage to be used for the game play.

### Error cases:  
In case the api key is not matching:

    {
    	"@class": ".AuthenticationResponse",
    	"authToken": "Qt4pzdX3JQtM8kZwFUjWoZ5d",
    	"error": {
    		"details": "API key not matching."
    	},
    	"requestId": "1590177530798_1"
    }
    
In case of a user / password mismatch: 

    {
        "@class": ".AuthenticationResponse",
        "authToken": "Qt4pzdX3JQtM8kZwFUjWoZ5d",
        "error": {
            "details": "User password unrecognized ."
        },
        "requestId": "1590177530798_1"
    }

