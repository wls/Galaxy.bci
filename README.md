# Galaxy.bci
An original real-time multiplayer game of Galaxy on the Data General MV/10000 written in BASIC using ASCII text graphics.

## Description
Players sign on to the game, create a ship, and jump into an extremely large galaxy.  They have visual short range scanner, textual long range scanners, shields, impulse engines, a warp drive, thrusters, phasers, intership radios, energy capsules, remote transmitters, ship computer, and a home base.

The galaxy is filled with planets that you must discover, conquer, and defend.  The idea is total conquest, though this is pretty much impossible to do with multiple players and competing strategies.  As such, raw point accumulations, minimal death counts, huge phaser battles, and other metrics make it fun to play.

Of particular interest is that planet locations _move_, even when no one is playing it.  What's even more interesting is that the game isn't a daemon.

## Configuration
Lines 00180-00187 define the configuration files useds for storing state.  You will need to alter this for your system.

The game was designed on a system with extremely small filespace quotas for students. As such, game resources were distributed between accounts.

Much like Unix uses /home/username, the filesystem notation is :SDD:UDD:username.  There are four accounts, KALLAN, 150A.MONROE, PER.STONEY, and 280.STONEY.  There is no requirement that the files be distributed if one account has enough space.  Historically, KALLAN was used for administrative files, 150A.MONROE was used for temporary files, PER.STONEY was used for development, and 280.STONEY was used for overflow.

Much like Unix uses 777 to indicate read/write/execute for user/group/other, the notation is _username_,OWARE for Owner/Write/Append/Read/Execute.  A plus sign meant all users.  As such, in line 00187, the two accounts have full ownership over the files, but the rest of the world is allowed to read and write them.

GALAXY.ACCESS determined who could play and other configuration items, GXY.USERS kept track of users playing the game, GXY.SHIPS kept track of each ship (users could fly more than one ship concurrently with enough real terminals), GXY.COMMUNICATION handled the ship-to-ship messages (useful if playing from all over campus), and GXY.SHARED maintained the galaxy state for when objects were left floating in space.

Lines 00330-00456 show the configuration parameters. Where the game could be ENABLED or DISABLED, a WELCOME message could be displayed, a list of MANAGER (highest level) accounts that could control the game, PRIVILEGED accounts that could do more in-game settings for keeping players abiding by the rules, a TYPE, STATUS, IF, IF NOT, COMMENT, MESSAGE, PLAYERS max, RESPONSE time, and other ship settings like PHASER, WARP, UNIVERSE size, TRIANGULATOR, starting ENERGY, and starting SHIELDS made the game tunable.

The Data General MV/10000 we played on had a work environment called CEO and it also had an early version of Word Perfect as well as some statical package like SPSS.  Problem was, when even three or four users ran these, the system couldn't handle the load -- as such, the RESPONSE directive would not let the game be played if the system was not more idle.  Additionally the PLAYERS directive prevented users from allocating all the terminals as ships.

## In game commands
Lines 05130 to 05160 are the command line interface to start play.  

BYE, EXIT, QUIT, and STOP are used to exit the game.  (The exception is that if you are PER.STONEY, the development account, then STOP returns you to the BASIC interpreter for debugging; normally users run the compiled version. If you're trying out the game, change this to your own account.)

HELP shows a list of commands.

BUILD will build a new ship.  PLAY will enter the game with the specified ship.

SHIPS will list your ships, and if you're one of the manager accounts, then the /ALL option will show all ships and who owns them. Normally ship ownership is anonymous, so that players can play both good cop and bad cop on two different terminals.

USERS will show who plays the game and what their score is.

MONITOR will provide metrics about the mainframes response times.

GALAXY will allow managers to see a visual representation of the galaxy.  This is useful for campaigns where managers are actually game moderators watching for objectives.


## The Big Bang
When the game is first started, if there are no state files, at line 00750 the system creates the universe and sets the access control list. Records are defined and game play begines.

## Your Starbase
Ship metrics (00918) and the captain's startbase (00920-00925) are created.  If someone found destroyed your starbase while you weren't in game, the "computers" that held your accomplishments were destroyed.

## Planets
You can take over a planet by getting near it and firing phasers to the surface. Planets are hostile if owned by other players, and they will get notifications of your attack.  When you subdue the planet, it then will extend its defenses to your orbiting ship, meaning if you're trying to resupply and regain energy, you aren't completely defenseless.

More enjoyable, when you take over a planet, you get to name it.  This customization can be quite amusing, as planets exchange hands.

## Energy Capsules
It's possible to store a bunch of energy into a capsule and eject it into space, then recharge.  During a massive fire fight, which can depelete reserves, flying back to the that capsule (as if you're fleeing a fight) can allow the captain to quickly recharge their ship and deliver a surprise volley.

Energy capsules can be discovered by other players, who can drain them, leaving a useless husk.

## Transmitters
It's possible to leave transmitters floating in space as watchdogs, and when another ship passes within its range, it send you a communication.  Very useful for when your long-range shields are no longer effective.

## Shields
Shields are a ship's defense against incoming phaser fire and other general damage. The more shields you have, the more drain on your reactor.  It is possible, for a brief while, to overcharge the shields.

## Reactor and Energy Stores
Each ship is equiped with a reactor that generates energy, and a huge battery for energy stores.  When you are using your ships subsystems, it drains your reserves.  When you are idle, it replenishes them.  It is possible to acquire an energy capsule from space and add it to your reserves for a super boost of power.

## Death
It's possible to be killed by other players, hostile planets, and even your own stupidity.

### Multiple Ships
All ships flown by an account are part of the same team.  And thus killing your own ships isn't all that useful.

## Docking and Quitting
If you can get to a non-hostile planet and dock with the station there, then you can exit the game without leaving your ship floatingin space.

If you try to quit the game after being immediately engaged in combat to get away from the fight, then it's considered cheating and a heavy penalty is applied to the score.

## Ship Damage
If a ship takes damage, then various subsystems start to fail, can't be used, report wrong information, or become severely crippled until repaired.

## Other things in space
Energy capsules and transmitters aren't the only thing that's out there.  There's hyperspace ports, strange pulsating objects, ship debris, energy fluctuations, ...there's much to explore independently, and there's plenty to lure you into traps.

## Final Notes
The source code appears to be riddled with trivial spelling errors. Feel free to submit fixes, if anyone is using this or decides to port.
