# FPS-Unlocker-fix
Regarding Roblox games, I have been informed of multiple issues of which I have been asked to create a few lines to fix. I have made this public for everyone to use.

What does FPS stands for?

FPS stands for Frames Per Second, which corresponds to how often the image will refresh on the monitor.
Monitors have a refresh rate, which is basically the maximum amount of FPS the monitor can handle, the refresh rate of a monitor is usually one of these numbers:

30hz
60hz
120hz
144hz
240hz

The amount of frames per seconds an user can have depends on their hardware and on how optimized the game is.
Roblox locks the amount of FPS to 60 FPS, which means your screen will be limited to refresh the image 60 times a second.
There is a software that allows a player to “unlock” their FPS and remove that limit when playing a Roblox game, which is called a FPS Unlocker.

How does this help me as a scripter?

RunService has a few events that run every frame, RenderStepped, Stepped and Heartbeat. (Those three events will soon become deprecated and be replaced by PreRender, PreAnimation, PreSimulation and PostSimulation)
Those events all have a “delta” argument, which is the amount of time elapsed between the last frame and the current one, if you calculate 1/delta, it gives you the user’s FPS.

Let’s say you wanted to create a projectile that would move by CFraming, if I didn’t know how to use the delta argument, it would go like this:

```lua local RunService = game:GetService("RunService")

RunService.Hearbeat:Connect(function()
    -- I know the maximum amount of FPS a player can have on Roblox is 60, therefore, the projectile will travel 100 studs in one second.
    projectile.CFrame = projectile.CFrame * CFrame.new(0, 0, -100/60)
end)
```
This is code I used to create before knowing about the delta argument, so what happened when I started using a FPS Unlocker? The projectile would fly off at a way greater speed than 100 studs/s.
There would also be the issue of players will mobile devices, who are not able to play at constant 60 FPS, the projectile would be slower for them.

If I want to fix this, I need to know how I can get the player’s FPS.
Delta is exactly that, 1/delta gives us the player’s FPS.
I can then modify my code above.

```lua local RunService = game:GetService("RunService")

RunService.Hearbeat:Connect(function(delta)
    -- I could code -100/(1/delta) but it's simpler to just multiply by delta.
    projectile.CFrame = projectile.CFrame * CFrame.new(0, 0, -100 * delta)
end)
```
This code is going to make the projectile move at a speed of 100 studs a second, no matter what the client’s FPS is.
This means the projectile will move exactly 100/FPS studs every frame.

Please take your own time to add this into a game, it shouldnt take too long.
