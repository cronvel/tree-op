# TOC
   - [Operator behaviours](#operator-behaviours)
<a name=""></a>
 
<a name="operator-behaviours"></a>
# Operator behaviours
mixing + and * for the same base key should preserve operation order (first *, then +).

```js
var creature = {
	hp: 8 ,
	attack: 5 ,
	defense: 3 ,
	move: 1
} ;

var shield = {
	"+defense": 3 ,
} ;

var enchantedArmor = {
	"*defense": 2 ,
	"+defense": 1 ,
	"+magic": 1
} ;

expect( treeOps.stack( creature , shield , enchantedArmor ) ).to.eql( {
	hp: 8 ,
	attack: 5 ,
	defense: 3 ,
	move: 1 ,
	"+defense": 4 ,
	"*defense": 2 ,
	"+magic": 1
} ) ;

expect( treeOps.reduce( creature , shield , enchantedArmor ) ).to.eql( {
	hp: 8 ,
	attack: 5 ,
	defense: 10 ,
	move: 1 ,
	"+magic": 1
} ) ;
```

- and / should be converted to + and *.

```js
var creature = {
	hp: 8 ,
	attack: 5 ,
	defense: 8 ,
	move: 1
} ;

var cursedAmulet = {
	"-defense": 2 ,
} ;

var cursedRing = {
	"/defense": 2 ,
} ;

expect( treeOps.stack( cursedAmulet ) ).to.eql( {
	"+defense": -2 ,
} ) ;

expect( treeOps.stack( cursedRing ) ).to.eql( {
	"*defense": 0.5 ,
} ) ;

expect( treeOps.stack( cursedAmulet , cursedRing ) ).to.eql( {
	"+defense": -2 ,
	"*defense": 0.5
} ) ;

expect( treeOps.stack( creature , cursedAmulet , cursedRing ) ).to.eql( {
	hp: 8 ,
	attack: 5 ,
	defense: 8 ,
	"+defense": -2 ,
	"*defense": 0.5 ,
	move: 1
} ) ;

expect( treeOps.reduce( creature , cursedAmulet , cursedRing ) ).to.eql( {
	hp: 8 ,
	attack: 5 ,
	defense: 2 ,
	move: 1
} ) ;
```

