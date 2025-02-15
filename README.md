local player = game.Players.LocalPlayer -- Get the local player
local character = player.Character or player.CharacterAdded:Wait() -- Get the character
local flying = false -- State to check if player is flying
local speed = 50 -- Speed of flying

-- Create a ScreenGui to hold the button
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
local flyButton = Instance.new("TextButton", screenGui)

-- Configure the button properties
flyButton.Size = UDim2.new(0, 100, 0, 50) -- Button size
flyButton.Position = UDim2.new(0.5, -50, 0.5, -25) -- Center the button
flyButton.Text = "Fly" -- Button text
flyButton.BackgroundColor3 = Color3.new(0, 1, 0) -- Green color

-- Function to toggle flying
local function toggleFly()
    flying = not flying -- Toggle the flying state
    if flying then
        flyButton.Text = "Stop" -- Change button text to 'Stop'
        character.Humanoid.PlatformStand = true -- Disable character controls
        local bodyVelocity = Instance.new("BodyVelocity", character) -- Create BodyVelocity for flying
        bodyVelocity.Velocity = Vector3.new(0, speed, 0) -- Set upward velocity
        bodyVelocity.MaxForce = Vector3.new(0, math.huge, 0) -- Max force for vertical movement

        -- Fly loop
        while flying do
            bodyVelocity.Velocity = Vector3.new(0, speed, 0) -- Continue flying upward
            wait(0.1) -- Wait for a short duration
        end
        
        bodyVelocity:Destroy() -- Remove BodyVelocity when flying stops
    else
        flyButton.Text = "Fly" -- Change button text back to 'Fly'
        character.Humanoid.PlatformStand = false -- Re-enable character controls
    end
end

-- Connect the button click to the toggleFly function
flyButton.MouseButton1Click:Connect(toggleFly)
