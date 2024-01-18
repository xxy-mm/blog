# Types

## mapping

syntax:

```solidity
mapping(KeyType KeyName? => ValueType ValueName?) VariableName
```

example:

```solidity
mapping(address => uint) public balances;
mapping(address user => uint balance) public balances;
mapping(address => mapping(address => uint256)) private _allowances;
```

## struct

```solidity
struct Funder {
  address addr;
  uint amount;
}

struct Campaign {
  address payable beneficiary;
  uint fundingGoal;
  /// uint amount;
  mapping(uint => Funder) funders;
}
```

## Event

```solidity
event EventName(ArgType ArgName, ArgType ArgName, ...);

emit EventName(arg1, arg2, ...);
```

## modifier

```solidity
modifier onlyOwner() {
  require(msg.sender == owner, "only owner can call this" );
  _;
}

function abort() public view onlyOwner {
  // ...
}
```

multiple modifiers will be executed in order.

```solidity
modifier anotherModifier() {
  require(msg.value > 0, "not enough gas");
  _;
}
// onlyOwner first, followed by anotherModifier
function test() public onlyOwner, anotherModifier {

}

```

## function visibility specifiers

- private
  - only visible in current contract
- internal
  - only visible in current and derived contracts
- external
  - only visible externally (only for functions) - i.e. can only be message-called (via this.func)
- public
  - visible both internally and externally
  - creates a getter function for state/storage variables
