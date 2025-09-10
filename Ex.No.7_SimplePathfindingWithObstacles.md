# Ex.No: 7  Implementation of Simple Pathfinding with Obstacles
### DATE:                                                                            
### REGISTER NUMBER : 212223240075
### AIM: 
To write a program to pathfinding using AI navigation 
### Algorithm:

#### 1. Create a New Unity Project
- Open Unity Hub → Create a new 3D Project  
- Name the project: Pathfinding

#### 2. Set Up the Scene (Ground)
- Go to: GameObject → 3D Object → Plane  
- Rename: Ground  
- Scale: (10, 1, 10) (adjust if needed)

#### 3. Add Obstacles
- Go to: GameObject → 3D Object → Cube  
- Scale: (3, 3, 1) (wall-like shape)  
- Rename: Obstacle  
- Position: Place it anywhere to block AI movement  
- Duplicate: Ctrl + D to create multiple obstacles  
- Tag all obstacles with the same name  

#### 4. Bake the NavMesh
- Go to: Window → AI → Navigation  
- Select Ground → In Navigation Window, check Navigation Static  
  - Or add a Navigation Surface component  
- Click Bake

#### 5. Create the AI Character
- Go to: GameObject → 3D Object → Capsule  
- Rename: AICharacter  
- Scale: (1, 2, 1)  
- In Inspector → Add Component → NavMeshAgent  
  - Speed: 3.5  
  - Stopping Distance: 1  
  - Obstacle Avoidance: High

#### 6. Create the Script
- Go to: Assets → Right Click → Create → C# Script  
- Rename: AIPathfinder.cs

#### 7. Attach the Script
- Drag and Drop AIPathfinder.cs onto the AICharacter

#### 8. Assign the Target
- Go to: GameObject → 3D Object → Sphere  
- Rename: Target  
- In AICharacter Inspector → AIPathfinder → Drag the Target Sphere into the target field

#### 9. Add NavMeshObstacle
- Select an Obstacle (Cube)  
- In Inspector → Add Component → NavMeshObstacle  
- Check Carve

#### 10. Move the Obstacle with Code
- Attach a movement script to the Obstacle

#### 11. Run the Program
- Press Play  
- The AI character will pathfind toward the target while avoiding moving obstacles
  
### Program:
#### AIPathFinder:
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.AI;
using static UnityEngine.GraphicsBuffer;

public class AIPathfinder : MonoBehaviour
{
    // Start is called before the first frame update
    public Transform target; // Assign the target in the Inspector
    private NavMeshAgent agent;
    void Start()
    {
        agent = GetComponent<NavMeshAgent>(); // Get the NavMeshAgent
    }

    // Update is called once per frame
    void Update()
    {
        agent.SetDestination(target.position);
    }
}
```
#### Moving Obstacle
```
using UnityEngine;

public class Moving : MonoBehaviour
{
    public float moveDistance = 3f;
    public float moveSpeed = 2f;
    private Vector3 startPos;

    void Start()
    {
        startPos = transform.position;
    }

    void Update()
    {
        float movement = Mathf.PingPong(Time.time * moveSpeed, moveDistance) - (moveDistance / 2);
        transform.position = startPos + new Vector3(movement, 0, 0);
    }
}
```

### Output:
<img width="1919" height="1079" alt="Screenshot 2025-09-09 150712" src="https://github.com/user-attachments/assets/6cccc88f-0104-426f-9c6f-7b062c0ccae9" />
<img width="1919" height="1079" alt="Screenshot 2025-09-09 150732" src="https://github.com/user-attachments/assets/8fc40361-e283-4383-b8c4-1fe2e3d97681" />

### Result:
Thus the simple path finding  behavior was implemented using AI navigation successfully.
