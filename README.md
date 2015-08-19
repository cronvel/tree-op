

# Tree Operation

Early alpha.

# TOC
   - [Basic tests](#basic-tests)
<a name=""></a>
 
<a name="basic-tests"></a>
# Basic tests
.

```js
var creature = {
	hp: 8,
	attack: 5,
	defense: 3,
	move: 1
} ;

var shield = {
	"+defense": 3,
	"?:evasion": 1
} ;

var enchantedArmor = {
	"*defense": 2,
	"+defense": 1,
	"+magic": 1
} ;

expect( treeOps.stack( creature , shield , enchantedArmor ) ).to.eql( {
	hp: 8,
	attack: 5,
	defense: 3,
	move: 1,
	"+defense": 4,
	"?:evasion": 1,
	"*defense": 2,
	"+magic": 1
} ) ;

expect( treeOps.reduce( creature , shield , enchantedArmor ) ).to.eql( {
	hp: 8,
	attack: 5,
	defense: 10,
	move: 1,
	"?:evasion": 1,
	"+magic": 1
} ) ;
```

