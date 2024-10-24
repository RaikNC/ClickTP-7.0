-- Criação do GUI
local ScreenGui = Instance.new("ScreenGui")
local OpenButton = Instance.new("TextButton")
local Frame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local TeleportButton = Instance.new("TextButton")

-- Propriedades do ScreenGui
ScreenGui.Name = "TeleportMenu"
ScreenGui.Parent = game.CoreGui

-- Propriedades do OpenButton
OpenButton.Name = "OpenButton"
OpenButton.Parent = ScreenGui
OpenButton.Text = "Abrir Menu"
OpenButton.Size = UDim2.new(0, 100, 0, 50)
OpenButton.Position = UDim2.new(0, 10, 0, 10)

-- Propriedades do Frame
Frame.Name = "MenuFrame"
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 200, 0, 200)
Frame.Position = UDim2.new(0.5, -100, 0.5, -100)
Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255) -- Cor branca
Frame.Visible = false
Frame.Active = true
Frame.Draggable = true

-- Propriedades do Title
Title.Name = "Title"
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0.3, 0)
Title.Font = Enum.Font.SourceSansBold
Title.Text = "RaikHub"
Title.TextColor3 = Color3.fromRGB(0, 0, 0) -- Cor inicial preta
Title.TextScaled = true

-- Propriedades do TeleportButton
TeleportButton.Name = "TeleportButton"
TeleportButton.Parent = Frame
TeleportButton.Text = "Ativar Teleporte"
TeleportButton.Size = UDim2.new(0, 180, 0, 50)
TeleportButton.Position = UDim2.new(0.5, -90, 0.5, -25)

-- Variáveis de controle
local teleportEnabled = false

-- Função para abrir/fechar o menu
OpenButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)

-- Função para ativar/desativar o teleporte
TeleportButton.MouseButton1Click:Connect(function()
    teleportEnabled = not teleportEnabled
    if teleportEnabled then
        TeleportButton.Text = "Desativar Teleporte"
    else
        TeleportButton.Text = "Ativar Teleporte"
    end
end)

-- Função para teleporte
game.Players.LocalPlayer:GetMouse().Button1Down:Connect(function()
    if teleportEnabled then
        local player = game.Players.LocalPlayer
        local character = player.Character
        local mouse = player:GetMouse()
        if character then
            character:SetPrimaryPartCFrame(CFrame.new(mouse.Hit.p))
        end
    end
end)

-- Função para gerar cores aleatórias, excluindo cinza e branco
local function getRandomColor()
    local colors = {
        Color3.fromRGB(255, 0, 0), -- Vermelho
        Color3.fromRGB(0, 255, 0), -- Verde
        Color3.fromRGB(0, 0, 255), -- Azul
        Color3.fromRGB(255, 255, 0), -- Amarelo
        Color3.fromRGB(0, 255, 255), -- Ciano
        Color3.fromRGB(255, 0, 255), -- Magenta
        Color3.fromRGB(255, 165, 0), -- Laranja
        Color3.fromRGB(128, 0, 128), -- Roxo
        Color3.fromRGB(0, 128, 128), -- Verde-azulado
        Color3.fromRGB(255, 20, 147) -- Rosa
    }
    return colors[math.random(1, #colors)]
end

-- Função para mudar a cor do título periodicamente
spawn(function()
    while true do
        wait(1)
        Title.TextColor3 = getRandomColor()
    end
end)
