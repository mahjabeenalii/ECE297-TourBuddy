# ECE297-TourBuddy

TourBuddy is a GIS-based application designed to aid tourists in efficiently navigating the intricacies of various cities with confidence. It does so by providing a custom-tailored experience and a vibrant social hub for connecting with fellow tourists. Leveraging Geographic Information Systems (GIS) technology, TourBuddy provides real-time information on attractions, such as restaurants, cafes, banks, tourist attractions, etc. 

## Key Features

<h3> 1. Search Mode </h3>
Users can click under search mode to search two streets and find the resulting intersection.

![search_mode](https://github.com/mahjabeenalii/ECE297-TourBuddy/blob/abc9851938f3ed33716f3197f17aa3d6a0ec94e0/src/search_mode.png)

<h3> 2. Direction Mode (A* and Dijkstra algorithms)</h3>
Tourists can find the shortest path between two intersections to their destination. Once the ‘starting point’ and ‘destination’ are entered/clicked, an animated view of the shortest path will appear on the map. These animations are pausable. TourBuddy also allows users to click ‘show directions’ for clear & concise travel directions with intuitive icons per direction, even for those who may be unfamiliar with the city. <br><br>
Finding the shortest path was implemented with <strong>A* Althorithm</strong>. Process: <br>
1. Initialize: Create a graph. <br>
2. Explore: Traverse legally connected intersections. <br>
3. Evaluate: Determine if the destination is reached or calculate the cost. <br>
4. Return: Backtrack and return the path if it exists. <br><br>
<strong>Dijkstra</strong>, a breadth first search algorithm, was used to find the paths to multiple destinations. This algorithm repeats until it has visited all destinations, then stores all the path times in a time matrix and paths in a path matrix. Using this matrix, we find a “greedy path”, which chooses the closest legal stop. We do this 2500 times and always saves the top best paths. <br><br>
<strong>Local search optimization</strong> was implemented using various iterative methods. <br>
<strong>Iterative methods used:</strong>
      <ul>
      <li><strong>Two-opt</strong>
        <ul>
          <li>Swap two edges and reverse segment between them</li>
          <li>Check if path is legal (pickup before dropoff)</li>
          <li>Retry swaps until legal or attempts exceeded</li>
        </ul>
      </li>
      <li><strong>Random shifting (time-optimal)</strong>
        <ul>
          <li>Move pickup before its dropoff, or dropoff after pickup</li>
          <li>Always produces a legal path</li>
          <li>Faster than checking full-path legality</li>
        </ul>
      </li></ul>
<strong>Escaping local minima:</strong> <br>
<ul>
      <li><strong>Simulated annealing</strong>
        <ul>
          <li>Uses decreasing temperature to sometimes accept worse moves</li>
          <li>Helps reach global minimum</li>
          <li>Increases perturbation attempts when stuck</li>
        </ul>
      </li>
      <li><strong>Greedy variation</strong>
        <ul>
          <li>Use second-best greedy path (~3% of the time) to diversify search</li>
        </ul>
      </li>
    </ul>

![direction_mode1](https://github.com/mahjabeenalii/ECE297-TourBuddy/blob/eabba8e7e270f2db29b88840986c0ab21d280c35/src/direction_mode1.png)

![direction_mode2](https://github.com/mahjabeenalii/ECE297-TourBuddy/blob/4e665bd220da4d5e199eae826f23aa95acccbcfb/src/direction_mode2.png)

<h3> 3. Easily recognizable icons </h3>
   <ul>
      <li>Subway Mode</li>
      <li>Night Mode</li>
      <li>Help Mode</li>
      <li>Points of Interest (POIs) such as Restaurants, Cafes, Banks, Entertainment, Tourist Attractions, Health Care, Sports, Shopping
      <li>When clicked on the heat map, the user can visualize both the heatmap and icon. The biggest circle heatmap represents the area with the most of that specific poi icon. </li>
   </ul>
   
   ![icons](https://github.com/mahjabeenalii/ECE297-TourBuddy/blob/5015c5d48f0b8fc921119f04b9992f4ca1552758/src/icons%2Bheatmap.png)

<h3> 4. Subway Mode </h3>
TourBuddy is also capable of displaying subway routes so tourists can navigate around the city on their own.

![subway_mode](https://github.com/mahjabeenalii/ECE297-TourBuddy/blob/7fec3927292fb20cc8a3cf239d231cc9fd5e5eef/src/subway_mode.png)

<h3> 5. Night Mode </h3>
To reduce eye strain and improve readability, our team has implemented night mode… ultimately the same, intuitive map with a darker colour scheme.

![night_mode](https://github.com/mahjabeenalii/ECE297-TourBuddy/blob/fa04ebf15f41ce77fad4835c4e3a53e3c125c6c4/src/night_mode.png)

<h3> 6. Parallel Programming </h3>
We utilized OpenMP to multithread. Thus, in cases such as filling the Multi-dijkstra matrix or finding the best paths from starting at different depots, each core can accomplish a different task, making it much more efficient than using one core. <br>
As a whole, employing diverse iterative methods to determine the most efficient routes to multiple destinations will enrich the experience for tourists seeking a GIS capable of intricately planning their personalized tours.
