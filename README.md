## Cygnus Tool: Adding Canisters

The Cygnus Tool provides users with three different implementation types for adding canisters:

1. **Cygnus Library**: Import Cygnus code into your Canister using one of the following programming languages:
   - [Motoko](https://github.com/CygnusIC/SDK/tree/master/motoko)

   In addition, you can view a list of controllers and withdraw cycles from this type of canister.

2. **Blackhole Canister**: This option grants access to an immutable canister.
   - [Cygnus Blackhole Canister](https://github.com/CygnusIC/Blackhole_Canister)

   Similar to the Cygnus Library, you can view a list of controllers for the Blackhole Canister. However, withdrawing cycles is not possible.

3. **Available Cycles** (Public method): This method exposes the `availableCycles` function in your code, commonly used in ext NFT token standards.
   An example implementation is provided below:

	```motoko
	public query func availableCycles() : async Nat {	
		return Cycles.balance();
	};
	```
   You can also whitelist the following two PrincipalIds to restrict access and only Cygnys can retrive the cycles data. 
   
  CYGNUS_CANISTER_ID: "dowzh-nyaaa-aaaai-qnowq-cai"
  CYGNUS_IDENTIRY_ID: ""
  
 For this type of canister, controllers and the ability to withdraw cycles are not visible.

## There are two ways to add a canister to the Cygnus Tool:

1. **Using the Front-End Tool**: Utilize the front-end tool provided.
2. **Using Cygnus Candid File**: Add the canister using the [Cygnus candid file](https://github.com/CygnusIC/implementation-/blob/main/Cygnus.did).

   An example is provided below in Motoko:

```Motoko
let CYGNUS_CANISTER_ID = "dowzh-nyaaa-aaaai-qnowq-cai";

public type implementationType = {
	#AvailableCycles;
	#BlackholeCanister;
	#CygnusLibrary;
};

let CygnusCanitser = actor (CYGNUS_CANISTER_ID) : actor {
                      registerProjectCanister : shared (
                      projectId : Text,
                      canisterId : Text,
                      canisterName : Text,
                      implementationType : implementationType,
                    ) -> (Text);
};

//Example
public shared(msg) func registerCanister() : async Text {
	await CygnusCanitser.registerProjectCanister("upr_7X32NXTQD304NABSZVMM6MB4R3", "mpaq5-4aapa-nqaag-qlppa-cai", "NFT", "CygnusLibrary");
};

```

Please note that in the **registerProjectCanister** function, you need to provide the appropriate values for **projectId**, **canisterId**, **canisterName**, and **implementationType** to register the desired canister.
