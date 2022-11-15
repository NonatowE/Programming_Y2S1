# Tutorial 1
## Third person character movement

This is a tutorial on how to create a script where the player can move the character in a 3D environment.


Within your scene, create a plane for our ground and a capsule for our player. Attach the camera on the player so that the camera will follow as the player moves.

We will be using a component within the player called the character controller. This will allow the player to move depending on the environment without needing to use physics. We will need to create a script also attached to the player called "movement" for the character controller to be used.

*** The Script:

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Movement : MonoBehaviour
{
    Vector3 playerMove = Vector3.zero;
    CharacterController characterController;
  
    // A reference to the character controller to use this for movement

    public float gravity;
    public float playerSpeed;
    public float playerJumpSpeed;
     // This will allow us to control the gravity and speed of the player in the scene through    
       the inspector view

    // Start is called before the first frame update
    void Start()
    {
        characterController = GetComponent<CharacterController>();
    }

    // Update is called once per frame
    void Update()
    {
        playerMove.x = Input.GetAxis("Horizontal") * playerSpeed;
        playerMove.z = Input.GetAxis("Vertical") * playerSpeed;
        // The player movement forward, backwards and side to side using WASD with the 
           speed to be adjusted through the inspector

        if (characterController.isGrounded && Input.GetButton("Jump"))
            playerMove.y = playerJumpSpeed
        // For the player to be able to jump using the space bar 

        playerMove.y -= gravity * Time.deltaTime;

        characterController.Move(playerMove * Time.deltaTime);
    }
}

