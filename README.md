   ASSESSMENT 2 REQUIREMENTS:
       
    1. Your contract will have public variables that store the details about your coin (Token Name, Token Abbrv., Total Supply)
    2. Your contract will have a mapping of addresses to balances (address => uint)
    3. You will have a mint function that takes two parameters: an address and a value. 
       The function then increases the total supply by that number and increases the balance 
       of the “sender” address by that amount
    4. Your contract will have a burn function, which works the opposite of the mint function, as it will destroy tokens. 
       It will take an address and value just like the mint functions. It will then deduct the value from the total supply 
       and from the balance of the “sender”.
    5. Lastly, your burn function should have conditionals to make sure the balance of "sender" is greater than or equal 
       to the amount that is supposed to be burned.



    pragma solidity ^0.8.18;
       
This line specifies the version of the Solidity compiler to use for this contract. Here, it uses version 0.8.18.


      contract CustomToken {
This line declares a new contract named CustomToken. In Solidity, contracts are similar to classes in object-oriented programming.


    
    string public name;
    string public symbol;
    uint public totalTokens;
    
These lines declare three public variables:
name: Stores the name of the token (e.g., "MyToken").
symbol: Stores the abbreviated symbol of the token (e.g., "MTK").
totalTokens: Stores the total supply of the tokens in circulation.
The public keyword makes these variables accessible from outside the contract.


    
    mapping(address => uint) public balances;
    
This line declares a mapping named balances:
mapping(address => uint): Maps each address to its respective token balance.
The public keyword allows external contracts and users to view balances.


    
    constructor(string memory _name, string memory _symbol, uint _initialSupply) {
        name = _name;
        symbol = _symbol;
        totalTokens = _initialSupply;
        balances[msg.sender] = _initialSupply; // Assign the initial supply to the contract creator
    }

    
This is the constructor function, which is called once when the contract is deployed:
It takes three parameters: _name, _symbol, and _initialSupply.
name = _name; sets the token's name.
symbol = _symbol; sets the token's symbol.
totalTokens = _initialSupply; sets the total supply of tokens to the initial supply value.
balances[msg.sender] = _initialSupply; assigns all the initial tokens to the address that deployed the contract (msg.sender).

    
    function mint(address _recipient, uint _amount) public {
        totalTokens += _amount;
        balances[_recipient] += _amount;
    }
    
This function mints (creates) new tokens:
It takes two parameters: _recipient (the address receiving the new tokens) and _amount (the number of tokens to mint).
totalTokens += _amount; increases the total supply of tokens by the specified amount.
balances[_recipient] += _amount; increases the balance of the recipient address by the specified amount.

   
    function burn(address _account, uint _amount) public {
        require(balances[_account] >= _amount, "Not enough tokens to burn");
        totalTokens -= _amount;
        balances[_account] -= _amount;
    }
    
This function burns (destroys) tokens:
It takes two parameters: _account (the address from which tokens will be burned) and _amount (the number of tokens to burn).
require(balances[_account] >= _amount, "Not enough tokens to burn"); checks if the account has enough tokens to burn. If not, it throws an error with the message "Not enough tokens to burn".
totalTokens -= _amount; decreases the total supply of tokens by the specified amount.
balances[_account] -= _amount; decreases the balance of the account by the specified amount.

This code represents a basic ERC20-like token contract in Solidity, where you can mint new tokens to increase the total supply and burn tokens to decrease it, while keeping track of each address's token balance.
