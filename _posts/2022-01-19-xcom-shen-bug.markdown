---
layout: single
title: "Of XCOM 2, ironman, and bugs."
date: 2022-01-19 01:00:00 +100
last_modified_at:
categories:
tags: xcom gaming bug console shen
---
tl;dr: turn on the console and type `DropUnit losttowersshen`

I can usually be found about five years behind the gaming curve, so naturally I'm playing through xcom2 for the first time. I play ironman because I like hurting myself I suppose.

Xcom2 is a little buggy, one bug in particular put my game into a broken state where I could not progress:

1. I was playing the 'Lost Towers' mission from the "Shen's Last Gift" DLC.
2. A character, Shen, tags along for the mission, they must not die or the mission will be failed, and you'll be given a chance to restart
3. Shen is necessary to activate something in stage 2
4. The mission is played in three stages. If you restart the mission, you will restart to the stage you most recently reached.
5. Shen died in stage one, but due to some corner case the game didn't force a mission restart and instead immediately sent me to stage 2[^1]
6. I didn't have Shen in stage 2.
7. Without Shen I couldn't complete the objective (see point 3)
8. The mission cannot be aborted
9. If all the soldiers die, I will restart at the beginning of stage 2, without Shen
10. It's impossible to progress with the game in this state
11. As I'm playing ironman, I cannot load another save, and it would appear my only option is to discard this campaign and start a new one.

I really didn't want to throw out all my progress, some frantic googling turned up this reddit thread from some years ago, but no solution:

[https://www.reddit.com/r/Xcom/comments/5do0e6/xcom_2_command_to_autocomplete_a_level/](https://www.reddit.com/r/Xcom/comments/5do0e6/xcom_2_command_to_autocomplete_a_level/)

I'm pleased to announce that I _have found_ a solution to this problem. You can just spawn a new Shen via the console, the tricky part is knowing what code corrresponds to Shen[^2].

Anyway, here's the how-to in case anyone else finds themselves in this spot. 

# Shut up and tell me how to fix it

Firstly, exit the game.

You'll want to enable the console[^3]. Right click the game in your steam library, select `Properties`, `General`, and in the `Launch Options` box type `-allowconsole`.

Start the game, load your save, and bring down the console with the `~` key.

Put your cursor where you want Shen to be. Type `DropUnit losttowersshen` and press enter. You should get a brand new Lily Shen, who can activate the necessary thing to progress the level.

The new Shen won't be marked as 'must survive' however. It appears that when the level loads the game instead marks one of your soldiers with the 'must survive' property, so be careful.

When you return to base you'll see an entry for Lily Shen on your memorial wall. The game won't otherwise notice that she's dead, and she'll happily inhabit your engineering bay as if nothing ever happened.

![F]({{ "/assets/images/2022-01-19-shen-memorial.png" | absolute_url}})

[^1]: If you're interested, what happened is all my other soldiers had evacuated to the next stage, Shen was the last person left. Shen was at the elevator to escape to the next stage but then died to a self-destructing murderbot. As soon as she died the next stage loaded, lol.
[^2]: A very special thanks to steam user 'Cyber von Cerberus' for his extensive list of spawnables [here](https://steamcommunity.com/sharedfiles/filedetails/?id=1223925683)
[^3]: Visual reference [here](https://commands.gg/xcom2/blog/console-help)
