# OpenGL Pong Game

## About the Project
This game was inspired by LearnOpenGL's Breakout game. The game mechanics and physics are a bit different and you will see that the inverted rendering is used here but with different mechanics. A pause state, AI state and fruit drop state were added for fun. A second player was added that uses AI to return the ball each time. Users can select AI from the main menu to have two AI players play the game instead.  

## Controls
Default game controls: Move the fox with WASD and UP, DOWN, LEFT, RIGHT. Key P will pause the game. Player 2 is AI. 

<div style="text-align: center;">
  <p><strong>Watch the YouTube Video <a href="https://www.youtube.com/watch?v=pD-pY-KDddw" target="_blank">here</a>.</strong></p>
</div>


![S3](https://user-images.githubusercontent.com/110789514/211897662-295f3fce-f186-4402-bbb7-642dbc6867e4.png)

## Keyboard Controls
We set the key controls in the processInput(dt) function where delta time is a parameter. 
With the following code, we set WASD and  UP, DOWN, LEFT, RIGHT to contol the fox's movement. Key P will pause the game. 

```cpp
if (this->State == GAME_ACTIVE)
// ...
    {
        if (this->Keys[GLFW_KEY_P] && !this->KeysProcessed[GLFW_KEY_P])
        {
            int pausepoints = points;
            points = pausepoints;
            this->State = GAME_PAUSE;
            this->KeysProcessed[GLFW_KEY_P] = true;
        }
        if (this->Keys[GLFW_KEY_A])
        {

            if (Player->Position.x >= 0.0f)
            {

                Player->Position.x -= velocity;
                if (Player->Position.x <= 0)
                    Player->Position.x = 0;

                if (Ball->Stuck)
                    Ball->Position.x -= velocity;
            }
        }
        if (this->Keys[GLFW_KEY_D])
        {

            if (Player->Position.x <= this->Width - Player->Size.x)
            {
                Player->Position.x += velocity;
                if (Ball->Stuck)
                    Ball->Position.x += velocity;
            }
        }
        if (this->Keys[GLFW_KEY_W])
        {
            keycounter += 1;
            if (Player->Position.y >= 0.0f)
            {
                Player->Position.y -= velocity;
                if (Ball->Stuck)
                    Ball->Position.y -= velocity;
            }
        }
        if (this->Keys[GLFW_KEY_S])
        {
            keycounter += 1;
            if (Player->Position.y <= this->Height - Player->Size.y)
            {
                Player->Position.y += velocity;
                if (Ball->Stuck)
                    Ball->Position.y += velocity;
            }
        }
// ...
}
```

## AI Controls

AI controls are added in the ProcessInput function. Random fruit drops and effects are added for fun. 

```cpp
    if (this->State == GAME_AI)
    {    
        if (this->Keys[GLFW_KEY_P] && !this->KeysProcessed[GLFW_KEY_P])
        {
            int pausepoints = points;
            points = pausepoints;
            this->State = GAME_PAUSE;
            this->KeysProcessed[GLFW_KEY_P] = true;
        }
        //  random effects
        if (keycounter > 200) { Effects->Chaos = true; }
        if (keycounter > 470) { Effects->Chaos = false; }
        if (keycounter > 600) { Effects->Confuse = true; }
        if (keycounter > 800) { Effects->Confuse = false;}
        if (keycounter > 810) { Effects->Shake = false; }
        if (keycounter > 880) { Effects->Shake = false; }

        Ball->Stuck = false;
        float velocity = PLAYER_VELOCITY * dt;
        if (Player->Position.y <= Ball->Position.y)
        {
            keycounter += 1;
            Player->Position.y += velocity;

            // keep player 2 in the upper bounds of the screen

            if (Player->Position.y >= this->Height - Player->Size.y)
            {
                Player->Position.y = this->Height - Player->Size.y;
            }
        }
        if (Player->Position.y >= Ball->Position.y)
        {
            // keep player 2 in the lower bounds of the screen
            if (Player->Position.y <= 0)
            {
                Player->Position.y = 0;
            }
            Player->Position.y -= velocity;

        }
        // AI player 2 is auto
        if (Player2->Position.y <= Ball->Position.y)
        {

            Player2->Position.y += velocity;

            // keep player 2 in the upper bounds of the screen

            if (Player2->Position.y >= this->Height - Player2->Size.y)
            {
                Player2->Position.y = this->Height - Player2->Size.y;
            }
        }
        if (Player2->Position.y >= Ball->Position.y)
        {
            // keep player 2 in the lower bounds of the screen
            if (Player2->Position.y <= 0)
            {
                Player2->Position.y = 0;
            }
            Player2->Position.y -= velocity;

        }
        // AI player 2 vertical

        if (this->Keys[GLFW_KEY_SPACE])
            Ball->Stuck = false;

        // fruit drops
        Fruit->Position.y += velocity / 2.0f;
        Fruit2->Position.y += velocity / 1.1f;
        Fruit3->Position.y += velocity / 3.0f;
        Fruit4->Position.y += velocity;
        Fruit5->Position.y += velocity;

    }
```
## Photoshop Tutorials

I added a Photoshop tutorial where I design the [spaceships and other game assets](https://youtu.be/WE-DJ-A5yTY). I also added a tutorial that demonstrates how to [configure your projects in Visual Studio](https://youtu.be/ZFx30Zmo1yI).

## References

Gmarc. (n.d.). Animal Set in Flat Style. https://www.freepik.com/free-vector/animals-set-in-flat-style_4767470.htm

Hui_u. (n.d.). colorful night sky. https://as1.ftcdn.net/v2/jpg/02/52/77/50/1000_F_252775020_qBF1RXgDQXKS7QFeu0Hd34GHLjYOWSWD.jpg

Infraction. 2022. Boobass. Boobass. 2022.

Jakkapan (n.d.). white angel wing isolated. https://as1.ftcdn.net/v2/jpg/00/90/60/84/1000_F_90608445_4CoFVuHPIIx4oSvNE4FQ3dKf2pa3SH8M.jpg

DeVries, J. (n.d.). LearnOpenGL/LICENSE.md at master · JoeyDeVries/LearnOpenGL. GitHub. https://github.com/JoeyDeVries/LearnOpenGL/blob/master/LICENSE.md

Learn OpenGL, extensive tutorial resource for learning Modern OpenGL. (n.d.-d). https://learnopengl.com/

<div style="text-align: center;">
  <p><strong>Proudly crafted with ❤️ by <a href="https://github.com/sheraadams" target="_blank">Shera Adams</a>.</strong></p>
</div>
