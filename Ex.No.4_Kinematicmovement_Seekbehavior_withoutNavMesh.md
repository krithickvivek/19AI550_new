# Ex.No: 4  Implementation of Kinematic movement -seek behavior in Unity
### DATE:                                                                            
### REGISTER NUMBER : 212223240075
### AIM: 
To write a program to simulate the process of seek behavior in Unity without NavigationMeshAgent. 
### Algorithm:
1. Create a New Unity Project by Open the  Unity Hub and create a new 3D Project,Name the project (e.g., SeekBehaviorDemo).
2. Create the Moving Object
   In the Hierarchy, right-click → 3D Object → Cube (or Sphere).
   Rename it to Seeker and Reset its position:Select the Seeker, go to Inspector → Transform → Set Position to (0,0,0).
3. Create the Target Object
   Right-click in the Hierarchy → 3D Object → Sphere (or any other shape).
   Rename it to Target. Move it away from Seeker, e.g., set Position to (5, 0, 5).
   Select the Target, add a Material, and change the color. (if needed) 
4. Adding the Seek Behavior Script
   Create the Script-In the Project Window, go to the Assets folder.
   Right-click → Create → C# Script.
5. Write a script for seek behavior and save it
6. Attach the Script
   Select Seeker in the Hierarchy - Drag & Drop the SeekBehavior script onto the Inspector Panel.
   Drag & Drop the Target from the Hierarchy into the "Target" field in the script component.
12. Run the game 
13. Stop the program
    
### Program:
```
using UnityEngine;

public class Seek : MonoBehaviour
{
    // Start is called before the first frame update
    public Transform Target;
    public float speed;
    void Start()
    {

    }
    void Update()
    {
        Vector3 direction = (Target.position- transform.position).normalized;
        transform.position += direction * speed * Time.deltaTime;
    }
}


```
### Output:
<img width="1917" height="1079" alt="image" src="https://github.com/user-attachments/assets/a94f9d4f-e08a-49eb-a9c6-7085e5ed5e47" />

### Result:
Thus the simple seek behavior was implemented successfully.
