# Ex.No: 2  Welcome Script in Unity
### DATE:                                                                            
### REGISTER NUMBER : 212223240075
## AIM: 
 To learn the basic scripting in Unity and print welcome message in Console window. 
## Procedure:
1. Start the program
2. Open the Unity hub and Create a new 3D project
3. In Assets window, create the new folder and name it as Scripts
4. Create a new script with file name as FirstScript
5. Open the Script and print message "Welcome to Unity" inside the start function
6. Save the script
7. Create a new 3D game object in Hierarchy window and name it as 3D Object.
8. Add the component Firstscript in inspector window of 3D object.
9. Run the program
10. Stop the program.
## Program 
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class FirstScript : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        print("Welcome to Unity");
    }

    // Update is called once per frame
    void Update()
    {
        transform.Translate(0, 0.2f, 0.2f);
    }
}
```
## Output:

<img width="1918" height="1051" alt="image" src="https://github.com/user-attachments/assets/5f2bb647-2e96-441d-9926-ac4e3d7a27e9" />


## Result:
Thus the welcome script was printed on Console Window  sucessfully.

