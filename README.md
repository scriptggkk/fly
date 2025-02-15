```lua
-- Cria uma aba na tela do jogador
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui")
local frame = Instance.new("Frame")
local closeButton = Instance.new("TextButton")
local flyButton = Instance.new("TextButton")

-- Configurações da aba
screenGui.Parent = player:WaitForChild("PlayerGui")
frame.Size = UDim2.new(0, 300, 0, 200) -- Tamanho da aba
frame.Position = UDim2.new(0.5, -150, 0.5, -100) -- Centraliza a aba
frame.BackgroundColor3 = Color3.new(1, 1, 1) -- Cor da aba
frame.Parent = screenGui

-- Configuração do botão de fechar
closeButton.Size = UDim2.new(0, 30, 0, 30) -- Tamanho do botão de fechar
closeButton.Position = UDim2.new(1, -35, 0, 5) -- Localização do botão de fechar
closeButton.Text = "X" -- Texto do botão de fechar
closeButton.Parent = frame

-- Configuração do botão de voar
flyButton.Size = UDim2.new(0, 100, 0, 50) -- Tamanho do botão de voar
flyButton.Position = UDim2.new(0.5, -50, 0.5, -25) -- Localização do botão de voar
flyButton.Text = "Fly" -- Texto do botão de voar
flyButton.Parent = frame

-- Função para fechar a aba
local function closeFrame()
    frame.Visible = false -- Esconde a aba
end

-- Função para ativar o voo
local function enableFly()
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    local bodyVelocity = Instance.new("BodyVelocity") -- Cria um BodyVelocity para voar
    bodyVelocity.Velocity = Vector3.new(0, 50, 0) -- Define a velocidade de voo
    bodyVelocity.MaxForce = Vector3.new(0, math.huge, 0) -- Permite que o personagem voe
    bodyVelocity.Parent = character:WaitForChild("HumanoidRootPart") -- Adiciona ao personagem

    -- Remove o BodyVelocity após 5 segundos
    wait(5)
    bodyVelocity:Destroy()
end

-- Conecta as funções aos botões
closeButton.MouseButton1Click:Connect(closeFrame) -- Fecha a aba ao clicar
flyButton.MouseButton1Click:Connect(enableFly) -- Ativa o voo ao clicar
```
