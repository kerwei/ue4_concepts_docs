UE4 Starter Cheatsheet

1. Create Animation blueprint (>> Animation > Animation blueprint)
    - Set parent class -- ACFAnimInstance
    - Set skeleton mesh -- ParagonShinbi
    - Import Anim Graph from ACFBaseABP

    ![alt text](AnimGraph%20AO%20during%20Switch.png)

    ![alt text](AnimGraph%20Additives.png)

    ![alt text](AnimGraph%20Leaning%20and%20AO.png)

    ![alt text](AnimGraph%20moveset%20switch.png)

    ![alt text](AnimGraph%20Riding.png)

    ![alt text](AnimGraph%20actions%20and%20montages.png)

    ![alt text](AnimGraph%20IK%20stuff.png)

2. Create movement blendspace (>> Animation > BlendSpace)
    - Set horizontal axis name to Direction
    - Set minmax value to -180, 180
    - Number of grid division to 8
    - Set vertical axis name to Speed
    - Set minmax value to 0, 1
    - Number of grid division to 4
    - Set animation sequence
        - Row 0, col 4 -> TravelMode_Fwd
        - Row 1, col 0 -> Jog_Bwd
        - Row 1, col 2 -> Jog_Right_Combat
        - Row 1, col 4 -> Jog_Fwd
        - Row 1, col 6 -> Jog_Left_Combat
        - Row 1, col 8 -> Jog_Bwd

3. Create idle blendspace (>> Animation > BlendSpace)
    - Set horizontal axis name to Angle
    - Set minmax value to -0.3, 0.3
    - Number of grid division to 4

4. Create Player blueprint (>> Blueprints > Blueprint class)
    - Set parent class -- ACFCharacter
    - Set skeleton mesh -- ParagonShinbi
    - Set Anim Class (>> Details > Animation)
        - Set Animation Mode to Use Animation Blueprint
        - Set Anim Class -- <created in #1>
    - Add Spring Arm to skeleton mesh
    - Add Camera to Spring Arm
    - Adjust Spring Arm location to align with skeleton mesh

5. Create game tags (>> Project settings > GameplayTags)
    - Add Action-Death
    - Add Action-Hit
    - Add Action-Idle

6. Set tags and blendspaces for the Animation blueprint (>> ACF > Movesets > *add element*)
    - Set TagName="Moveset"
    - Set Movement blendspace to BS_Movement
    - Set Idle blendspace to BS_Idle
    - Set Aim offset blendspace to Idle_AO_Blendspace
    - Set Jump Start blendspace to Jump_Start
    - Set Jump Loop blendspace to Jump_Apex
    - Set Jump End blendspace to Jump_Land

    ![alt text](Anim%20movesets.png)

7. Create Player Controller blueprint (>> Blueprints > Blueprint class)
    - Set parent class -- ACFPlayerController
    - Add the ATSTargeting component (>> + Add component > ATSTargeting)
    - Import Event Graph from ACFPlayerController Blueprint
    - Add a new variable
        - set variable name to BaseLookUpRate
        - set variable type to Float
    - Add a new variable
        - set variable name to BaseTurnRate
        - set variable type to Float

8. Add Engine Input mappings
    - Add Action Mappings
        - (Name: Target, Input: Middle Mouse Button)
    - Add Axis Mappings
        - (Name: Turn, (Mouse X, 1.0))
        - (Name: LookUp, (Mouse Y, -1.0))
        - (Name: TurnRate, (None, 1.0))
        - (Name: LookUp, (None, -1.0))
        - (Name: MoveForward, (W, Scale: 1.0), (S, Scale: -1.0))
        - (Name: MoveRight, (D, Scale: 1.0), (A, Scale: -1.0))

9. Create GameMode blueprint (>> Blueprints > Blueprint class)
    - Set Player Controller Class -- <created in #7>
    - Set Default Pawn Class -- <created in #4>

10. Update World Settings to use the GameMode -- <created in #9>

11. Set up event graph for Character blueprint -- <created in #4>
    - Keyboard Input

    ![alt text](Keyboard%20Input.png)

    - Input for sprinting

    ![alt text](Input%20for%20sprinting.png)

    - Input for walking

    ![alt text](Input%20for%20walking.png)