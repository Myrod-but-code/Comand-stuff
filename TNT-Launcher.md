You will learn here how to do a TNT launcher (using a bow) but also any entity (that can have Motion) !

To start off, create an scoreboard using
> /scoreboard objectives add bow_shot minecraft.used:minecraft.bow
This creates a variable that increases each time you use a bow

Then, do :
> /scoreboard players add #checker bow_shot 1
This creates a fake player named checker that has bow_shot to 1, which we will use to compare later on.

Final step before the command blocks, run :
> /scoreboard players add @a bow_shot 0

Then, put in a repeating, unconditional, needs redstone command block, with a powered lever on top (you can put always active, but I like needs redstone, because you can disable it with a lever) :
> execute at @a if score @n bow_shot >= #checker bow_shot if items entity @n weapon.* bow[minecraft:custom_data={"tnt_bow":"yes"}] run summon minecraft:tnt ~ ~1.5 ~ {Tags:["bow_shot"]}
This makes it so at every player, if their score is greater or equal to 1 (the #checker fake player), therefore if they used a bow, and if they are holding the custom bow, summoning a tnt at their head.
This TNT has a tag bow_shot, which we can later on detect.
You can change that TNT to any entity, by replacing minecraft:tnt (in run summon at the end) with the entity you want

Then, at the end of the repeating command block's arrow, put a row of 4 chain, unconditional, always active command blocks, with the arrows poiting into the next one.

In the first one, paste :
> execute at @e[type=tnt,tag=bow_shot] if entity @n[type=arrow] run data modify entity @n[type=tnt] Motion set from entity @n[type=minecraft:arrow,distance=..3] Motion
This makes it so every TNT with the tag bow_shot gets the bow's arrow motion (speed). 
If you decided to change TNT to an other entity, replace @e[type=tnt,tag=bow_shot], by  @e[type=the entity you want,tag=bow_shot], and change, in run data modify entity @n[type=tnt] by @n[type=the entity you want]

In the second one, add :
> execute at @e[type=tnt,tag=bow_shot] run kill @n[type=minecraft:arrow,distance=..3]
This removes the arrow shot by the bow, because you only want to shoot a TNT.
Once again, if you changed the entity, use @e[type=the entity you want,tag=bow_shot]

In the third, put :
> execute at @e[type=tnt,tag=bow_shot] run tag @n remove bow_shot
This removes the tag bow_shot to any tnt, so it acts as a normal tnt, and can't be moved again by arrows.
If you replaced the TNT, replace @e[type=tnt,tag=bow_shot] by @e[type=the entity you want,tag=bow_shot]

Finally, paste in the fourth command block :
> execute at @a if score @n bow_shot >= #checker bow_shot run scoreboard players set @n bow_shot 0
This reset the counter of the usage of bows of every player, so that the first command doesn't spawn infinite TNT.
Nothing to change here if you replaced the TNT.

Hope you enjoyed, and have fun !

Note : I wanted to do stuff using command blocks because of BlockerLocker (youtube channel). If you liked this, go check them out !
