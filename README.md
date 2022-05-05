# ComS_327_Path-Finding

COM S 327, Spring 2022
Programming Project 1.02
Path Finding
Next week we’ll be introducing adversary trainers to our game. We’ll have trainers who just stand by the
road and don’t move. We’ll have trainers who walk back and forth within a region, and we’ll have trainers
that chase the PC1
. We’ll have two different kinds of trainers that pathfind: hikers, who can go anywhere,
and rivals, who can’t walk over rocks or trees. If you’ve introduced other types of terrain in your maps, treat
it logically; probably even hikers can’t cross lakes, but if you were to introduce swimmers, they could.
This week we’ll calculate movement paths for hikers and rivals. Both of these trainer classes can see the
PC wherever it is and take the shortest path to the PC so they can engage in a Pokemon battle. Shortest time ´
is defined in terms of travel time. We’ll define travel times through terrain in game turns—where a game
turn is the smallest length of time that can pass in the game—as follows:
Terrain↓\Trainer→ Hiker Rival PC Others
Boulder ∞ ∞ ∞ ∞
Tree ∞ ∞ ∞ ∞
Path 10 10 10 10
Pokemart ´ ∞ ∞ 10 ∞
Pokemon Center ´ ∞ ∞ 10 ∞
Tall Grass 15 20 20 20
Clearing 10 10 10 10
Mountain 15 ∞ ∞ ∞
Forest 15 ∞ ∞ ∞
In my maps, I have mountains and forests which are separate entities from boulders and trees. There was
no requirement that you do this, and there is no requirement that you add it now. However, You will want
to prevent NPCs from accessing the border of a map. By making boulders impassible (∞), and marking my
border with boulders, I implicitly prevent NPCs from entering the border. As a result, I also get a random
terrain element that stops all characters. I use trees the same way, and could use them in my map borders if
I wanted to. By having separate mountain and forest terrain (using the same symbols but different internal
representation, I have a terrain that those hardy hikers can cross (at a small movement penalty) but nobody
else can, including the PC. If you have boulders but not mountains and you don’t want to add mountains,
probably the easiest change is to create a border terrain which is displayed using your boulder symbol and
has infinite movement cost.
Given these movement costs, we’re going to calculate shortest paths from all locations to the PC. This
implies that the PC will have to appear in the map as well. To generate the PC, choose a random location
anywhere on a road and not on the border. Use an @ to represent the PC when you draw it. It would probaly
be wise to add a placeholder pc datatype at this point and put the PC’s position data inside it.
Movement can occur in all 8 directions. Use Dijkstra’s Algorithm (or A*) to calculate the distance to
the PC from every location in the map for hikers and rivals.
Dijkstra’s Algorithm is described here: http://en.wikipedia.org/wiki/Dijkstra%27s algorithm. Scroll
down to find the pseudocode under “Using a priority queue”. Obviously, you’ll need a priority queue,
1
I think I’ve used this before without defining it. In case you’re not hip to all the lingo the gamer kids are using, the PC is the
player character, while NPCs and non-player characters.
one with a decrease priority operation. You may use the Fibonacci queue that I provided with my solution to
1.01, or you may implement (or use a properly-attributed third party implementation of) any other priority
queue you like.
My corridor building code uses Dijkstra’s algorithm, so you may start with that (it won’t require much
modification) or start from scratch.
Your program should display the hiker and rival distance maps. Use two digits per distance and display
distance mod 100 with a space between each distance (example output to follow, after I’ve implemented it).
All code is to be written in C.
