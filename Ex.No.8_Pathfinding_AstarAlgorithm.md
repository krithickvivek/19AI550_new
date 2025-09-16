# Ex.No: 8  Implementation of Path finding using A* algorithm

#### DATE:                                                                            
#### REGISTER NUMBER : 212223240075 

### Aim  
To write a program to create graph using waypoints and use A* algorithm to find path between source and destination.  

### Algorithm  
1. Create a New Unity Project by opening the Unity Hub and create a new 3D Project. Name the project (e.g., Pathfinding).  
2. Create Waypoints in Scene → Create empty or sphere GameObjects (minimum 4) and name them as Waypoint1, Waypoint2, ..., Waypoint4. Position them freely in the scene (not on a grid).  
3. Write a waypoint script to draw the lines between neighbors.  
4. Attach Waypoint.cs script to each waypoint GameObject and manually assign neighbors in the Inspector to form a graph.  
5. Create an empty GameObject and name it as WaypointManager – to manage all waypoints.  
6. Attach WaypointGraph.cs script to it.  
7. Write a Pathfinding algorithm using A* search.  
8. Create a GameObject for Player (choose capsule or any others) and attach the script to move player from start to end waypoints.  

### Program  
#### 1. Waypoint.cs
```csharp
using UnityEngine;
using System.Collections.Generic;

public class Waypoint : MonoBehaviour {
    public List<Waypoint> neighbors = new List<Waypoint>();

    // Optional: Draw connections in the editor
    private void OnDrawGizmos() {
        Gizmos.color = Color.yellow;
        foreach (var neighbor in neighbors) {
            if (neighbor != null) {
                Gizmos.DrawLine(transform.position, neighbor.transform.position);
            }
        }
    }
}
```
#### 2. WaypointGraph.cs
```csharp
using UnityEngine;

public class WaypointGraph : MonoBehaviour {
    public Waypoint[] allWaypoints;

    void Awake() {
        allWaypoints = FindObjectsOfType<Waypoint>();
    }
}
```
#### 3. Pathfinding.cs
```
using System.Collections.Generic;
using UnityEngine;

public class Pathfinding : MonoBehaviour {
    public static List<Waypoint> FindPath(Waypoint start, Waypoint goal) {
        var openSet = new List<Waypoint>();
        var cameFrom = new Dictionary<Waypoint, Waypoint>();
        var gScore = new Dictionary<Waypoint, float>();
        var fScore = new Dictionary<Waypoint, float>();

        foreach (var wp in FindObjectsOfType<Waypoint>()) {
            gScore[wp] = float.PositiveInfinity;
            fScore[wp] = float.PositiveInfinity;
        }

        gScore[start] = 0f;
        fScore[start] = Vector3.Distance(start.transform.position, goal.transform.position);
        openSet.Add(start);

        while (openSet.Count > 0) {
            Waypoint current = openSet[0];
            foreach (var wp in openSet) {
                if (fScore[wp] < fScore[current]) {
                    current = wp;
                }
            }

            if (current == goal) {
                return ReconstructPath(cameFrom, current);
            }

            openSet.Remove(current);

            foreach (var neighbor in current.neighbors) {
                float tentativeG = gScore[current] + Vector3.Distance(current.transform.position, neighbor.transform.position);
                if (tentativeG < gScore[neighbor]) {
                    cameFrom[neighbor] = current;
                    gScore[neighbor] = tentativeG;
                    fScore[neighbor] = tentativeG + Vector3.Distance(neighbor.transform.position, goal.transform.position);

                    if (!openSet.Contains(neighbor)) {
                        openSet.Add(neighbor);
                    }
                }
            }
        }

        return null; // No path found
    }

    private static List<Waypoint> ReconstructPath(Dictionary<Waypoint, Waypoint> cameFrom, Waypoint current) {
        var path = new List<Waypoint> { current };
        while (cameFrom.ContainsKey(current)) {
            current = cameFrom[current];
            path.Insert(0, current);
        }
        return path;
    }
}
```
#### 4. AICharacter.cs
```csharp
using UnityEngine;
using System.Collections.Generic;

public class AICharacter : MonoBehaviour {
    public Waypoint startWaypoint;
    public Waypoint goalWaypoint;
    public float speed = 3f;

    private List<Waypoint> path;
    private int currentIndex = 0;

    void Start() {
        path = Pathfinding.FindPath(startWaypoint, goalWaypoint);
    }

    void Update() {
        if (path == null || currentIndex >= path.Count) return;

        Vector3 target = path[currentIndex].transform.position;
        transform.position = Vector3.MoveTowards(transform.position, target, speed * Time.deltaTime);

        if (Vector3.Distance(transform.position, target) < 0.1f) {
            currentIndex++;
        }
    }
}
```
### Output
<img width="1919" height="1075" alt="Screenshot 2025-09-16 142117" src="https://github.com/user-attachments/assets/2e0dce1d-86f8-4f89-8b89-91e146b751d2" />
<img width="1919" height="1079" alt="Screenshot 2025-09-16 142142" src="https://github.com/user-attachments/assets/9647bf56-53d6-4d08-b57f-39c84a35bb03" />
<img width="1919" height="1078" alt="Screenshot 2025-09-16 143021" src="https://github.com/user-attachments/assets/de098200-6e6c-495a-8390-459a4fde016e" />

### Result
Thus, the pathfinding algorithm was successfully implemented using the A* algorithm.
