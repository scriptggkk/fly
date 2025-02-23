local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0.3, 0, 0.3, 0)
frame.Position = UDim2.new(0.35, 0, 0.35, 0)
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)

local closeButton = Instance.new("TextButton", frame)
closeButton.Size = UDim2.new(0.1, 0, 0.1, 0)
closeButton.Position = UDim2.new(0.9, 0, 0, 0)
closeButton.Text = "X"
closeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

local flyButton = Instance.new("TextButton", frame)
flyButton.Size = UDim2.new(0.5, 0, 0.1, 0)
flyButton.Position = UDim2.new(0.25, 0, 0.4, 0)
flyButton.Text = "Fly"
flyButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)

local flying = false
local bodyVelocity

local function fly()
    if not flying then
        flying = true
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
        
        bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.Parent = humanoidRootPart
        bodyVelocity.Velocity = Vector3.new(0, 25, 0)
        bodyVelocity.MaxForce = Vector3.new(4000, 4000, 4000)

        while flying do
            bodyVelocity.Velocity = Vector3.new(mouse.Hit.LookVector.X * 25, 25, mouse.Hit.LookVector.Z * 25)
            wait()
        end

        bodyVelocity:Destroy()
    end
end

local function stopFly()
    flying = false
end

closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

flyButton.MouseButton1Click:Connect(function()
    if flying then
        stopFly()
        flyButton.Text = "Fly"
    else
        fly()
        flyButton.Text = "Stop"
    end
end)
