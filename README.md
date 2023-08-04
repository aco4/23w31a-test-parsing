I was interested in how the new 23w31a snapshot parses commands using the new `\` multi-line feature. My testing is below. Post-authored comments are indicated by `/* */`, and all commands are executed by my player.

# Leading/trailing whitespace
```
   say hi
say bye   /* Trailing whitespace */
```
Output:
```
Executed 2 command(s) from function 'foo:test'
[Crayola_God] hi
[Crayola_God] bye
```
_I was unable to tell if there was trailing whitespace in the output_

# Simple comments
```
#This file will test
# simple comments
   say hi#This command says hi
say bye   #This one says bye
   say one# This says "one"
say two   # This says "two"
```
Output:
```
Executed 4 command(s) from function 'foo:test'
[Crayola_God] hi#This command says hi
[Crayola_God] bye   #This one says bye
[Crayola_God] one# This says "one"
[Crayola_God] two   # This says "two"
```

# Multi-line comments/commands

```
# Reset the game \
for the next round

scoreboard players set \
@a gold_collected 0

scoreboard players set \
  @a ammo 100
  
scoreboard players set \
  #count zombies_killed 0

say The game \
has been reset!

say Please proceed \
  to the lobby

say The next round starts in \         /* Trailing whitespace */
3 minutes!

say Everyone celebrate! \(^o^)/

say And \ remember \ to \ get \ healed \ up\!
```
Output:
```
Executed 8 command(s) from function 'foo:test'
[Crayola_God] The game has been reset!
[Crayola_God] Please proceed to the lobby
[Crayola_God] The next round starts in 3 minutes!
[Crayola_God] Everyone celebrate! \(^o^)/
[Crayola_God] And \ remember \ to \ get \ healed \ up\!
```
All 3 scores were successfully set.

# Macros
Input:
```
/function foo:test {"message":"Zombies are here", "location":"the church"}
```
`foo:test`:
```
$\
say $(message)

$say Go to \
$(location)!
```
Output:
```
Executed 2 command(s) from function 'foo:test'
[Crayola_God] Zombies are here
[Crayola_God] Go to the church!
```

---

> Written with [StackEdit](https://stackedit.io/).
