Documentation for Team Squonk Fall 2022 Project

CORI ALBRITTON

FrmMenu.cs
    - The FrmMenu.cs file adds the new main menu for the game. It plays a cutscene first before showing the actual menu.

    METHODS
    1) quitBtn_Click(object sender, EventArgs e)
        - Triggers when the quitBtn on the main menu form is clicked. This closes the entire application

    2) playBtn_Click(object sender, EventArgs e)
        - Triggers when the playBtn on the main menu form is clicked. Currently it hides the current menu form then start's the gcharacter select form.
        - It starts the game form by calling FrmLevel.GetInstance(0) and assigning it to the variable theGame and then showing that varibale.
        - The 0 input tells the function that this is calling a new game and needs to return a new FrmLevel()
    
    3) helpBtn_Click(object sender, EventArgs e)
        - Triggers when the helpBtn on the main menu form is clicked. Its pops up the help screen. 
        
    4) skipBtn_Click(object sender, EventArgs e)
        - Skips the cutscene and goes to the menu.
Program.cs
    - When first starting up the application, the game now starts by loading up the FrmMenu() form instead of the FrmLevel() form

FrmLevel.cs
    - The map that the game takes place on.
    
    METHODS
    1) GetInstance(int flag)
        - The method is used to either open up a new, fresh version of the FrmLevel() form or reset the instance of the form if the game has ended, either by the player winning or dying in battle. 
        - An input of 0 tells the function to return a new FrmLevel form while an input of 1 tells the function to reset the instance to null

FrmDeath.cs
    - The death screen that pop ups when the game ends, specifically after the player's health has reached 0 while fighting. It displays a specific image for each character option.

    METHODS
    1) menuBtn_Click(object sender, EventArgs e)
        - Triggers when the menuBtn on the death screen is clicked. It creates a new instance of the FrmMenu form and shows it then closes the FrmDeath form.
    
    2) quitBtn_Click(object sender, EventArgs e)
        - Triggers when the quitBtn on the death screen is clicked. This closes the entire application

FrmCharacterSelect.cs
    - The character selection screen the players reaches before starting the game. All three of the click methods in this form start the game by calling FrmLevel.GetInstance(0) which creates a new instance of the FrmLevel form and shows the form

    METHODS
    1) selectMr_Click(object sender, EventArgs e)
        - This function sets the player model and stats to the Mr. Peanut class

    2) selectMs_Click(object sender, EventArgs e)
        - This function sets the player model and stats to the Ms. Peanut class
        
    3) selectBaby_Click(object sender, EventArgs e)
        - This function sets the player model and stats to the Baby Peanut class
        
FrmBattle.cs
    - The battle screen. The player picture displays the image for the specific character chosen. The player also now has the option to do a special attack that is unique for each character.
    
    METHODS
    1) btnAttack_Click(object sender, EventArgs e)
        - Function now checks the health of the player and pops up the death form
        - Also checks if the player is playing as baby and if so, checks if the baby has used the special attack so it can know if it needs to deal extra damage or not.
        
    2) specialAttack_Click(object sender, EventArgs e)
        - New function that will do damage based on a special attack unique to the character
        - Mr. Peanut's special attack is just a stronger one time attack he can do once
        - Mrs. Peanut's is a health steal that takes health from the enemy and heals her for that amount
        - Baby Peanut has a bleed attack that will continuously do damage for the next three attacks
        
    3) DeathCheck(object sender, EventArgs e)
        - New function that checks if either the player or the enemy's health reaches zero. 
        - If the enemy reaches zero, then the battle is closed and the player is able to continue playing.
        - If the player reaches zero, then the battle and level is closed and a new instance of FrmDeath.cs pops up.
        
    4) helpBtn_Click(object sender, EventArgs e)
        - Triggers when the helpBtn on the main menu form is clicked. Its pops up the help screen. 

FrmHelp.cs
    - A help screen that the player will be able to access on the menu, battle screens, and level screen in pause. 
    
    METHODS
    1) closeBtn_Click(object sender, EventArgs e)
        - Triggers when the closeBtn on the help screen is clicked. Simply closes the help screen.

COREY BELK-SCROGGINS

FrmLevel.cs
    
    METHODS
    1) StopMusic()
        - Globally controls stopping the music for the main level audio.

    2) StartMusic()
        - Globally controls playing the music for the main level audio.

    3) PauseGame()
        - Responsible for creating and showing the new Windows Form that pauses all process related to gameplay.

    4) OnKeyUp(KeyEventArgs e)
        - Overrides the built-in KeyEventUp method to raise an event every time a key on the Keyboard is released.
        - Changes Character Class position array to simulate which direction is triggered.
        - e.x. Press left changes position[4] to 1, and all other indecies (5,6,7) to 0.

    5) OnKeyDown(KeyEventArgs e)
        - Overrides the built-in KeyEventDown method to raise an event every time a key on the Keyboard is pressed.
        - Changes Character Class position array to simulate which direction is triggered.
        - e.x. Release left changes position[0] to 1, and all other indecies (1,2,3) to 0.

    6) ReturnKeyDownInt()
        - Returns 0 or 1 to check which arrow key has been pressed.
        - e.x. Left key is pressed then l is set to 1.
        - e.x. No key is pressed then return 0.

    7) ReturnKeyDownInt()
        - Returns 0 or 1 to check which arrow key has been released.
        - e.x. Left key is released then l is set to 1.
        - e.x. No key is released then return 0.

    8) UpdateKeyValues(object source, System.Timers.ElapsedEventArgs e)
        - Globally sets 8 key press variables to the values corresponding to each 4 cardinal directions.
        - e.x. Right key is tapped then RightKeyDown and RightKeyUp equals 1.

    9) ResetKeyValues()
        - Resets the values after each KeyEventArg.

    10) FrmLevel_KeyDown(object sender, KeyEventArgs e)
        - Determines if user presses the letter 'p' on the keyboard to pause the game.
        - Determines if user presses the Ctrl key on the keyboard to shrink the player.
            - Determines which character was selected and adjusts their stats after shrunken.
        - Contains a timer called clock that updates the level at 60 frames per second.
        - Sends the triggered key data to Character Class to execute movement of the player

Character.cs

    METHODS
    1) CharacterSelectedSpeed(int s)
        - Sets the speed of the player based on the character selected.

    2) KeysPressed(KeyEventArgs e, int up_key_down, int left_key_down, int down_key_down, int right_key_down, int up_key_up, int left_key_up, int down_key_up, int right_key_up)
        - Takes the key data from FrmLevel_KeyDown and determines which direction the player should move in.
        - Uses original arrow key value to perform the first movement then compares position array values.
        - e.x If left key and position[0] is 1, move player left and up.
        - If no data was passed then reset move speed vector to 0.

FrmPause.cs
    
    - New Windows Form used to pause the game.

    METHODS
    1) Resume_Click(object sender, EventArgs e)
        - Closes form.
        - Sets pausedTime variable to false.
        - Starts the FrmLevel music again.

    2) Restart_Click(object sender, EventArgs e)
        - Creates new FrmMenu form
        - Closes current FrmLevel instance
        - Shows new FrmMenu form
        - Closes Pause form

    3) Quit_Click(object sender, EventArgs e)
        - Exits the application

    4) help_button_Click(object sender, EventArgs e)
        - Creates a new FrmHelp form
        - Shows the new FrmHelp form