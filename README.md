-- Open-source script for Roblox
-- Compatible with Krnl executor

local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)
Frame.BackgroundTransparency = 0.5 -- Meio transparente

-- Criando barra lateral para abas
local Tabs = Instance.new("Frame")
Tabs.Parent = Frame
Tabs.Size = UDim2.new(0, 80, 1, 0) -- Barra lateral ocupando toda a altura
Tabs.Position = UDim2.new(0, 0, 0, 0) -- Alinhada à esquerda
Tabs.BackgroundColor3 = Color3.fromRGB(200, 100, 100)
Tabs.BackgroundTransparency = 0.5 -- Meio transparente

-- Criando um pequeno quadrado de minimização
local MinimizedFrame = Instance.new("Frame")
MinimizedFrame.Parent = ScreenGui
MinimizedFrame.Size = UDim2.new(0, 50, 0, 50)
MinimizedFrame.Position = UDim2.new(0.5, -25, 0.5, -25)
MinimizedFrame.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
MinimizedFrame.Visible = false -- Começa oculto

local MinimizedButton = Instance.new("TextButton")
MinimizedButton.Parent = MinimizedFrame
MinimizedButton.Size = UDim2.new(1, 0, 1, 0)
MinimizedButton.Text = "+"
MinimizedButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)

MinimizedButton.MouseButton1Click:Connect(function()
    Frame.Visible = true -- Restaura a interface principal
    Tabs.Visible = true
    MinimizedFrame.Visible = false
end)

-- Criando o texto inicial "Emilli❤️"
local InitialMessage = Instance.new("TextLabel")
InitialMessage.Parent = Frame
InitialMessage.Text = "Emilli❤️"
InitialMessage.Size = UDim2.new(1, -80, 1, -50) -- Ocupa o espaço das abas
InitialMessage.Position = UDim2.new(0, 80, 0, 50)
InitialMessage.BackgroundTransparency = 1
InitialMessage.TextColor3 = Color3.fromRGB(255, 255, 255)
InitialMessage.TextScaled = true

-- Criando abas (posicionadas à direita da barra lateral)
local TrollTab = Instance.new("Frame")
TrollTab.Parent = Frame
TrollTab.Size = UDim2.new(1, -80, 1, -50)
TrollTab.Position = UDim2.new(0, 80, 0, 50)
TrollTab.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
TrollTab.BackgroundTransparency = 0.5
TrollTab.Visible = false

local PlayerTab = Instance.new("Frame")
PlayerTab.Parent = Frame
PlayerTab.Size = UDim2.new(1, -80, 1, -50)
PlayerTab.Position = UDim2.new(0, 80, 0, 50)
PlayerTab.BackgroundColor3 = Color3.fromRGB(100, 255, 100)
PlayerTab.BackgroundTransparency = 0.5
PlayerTab.Visible = false

local OthersTab = Instance.new("Frame")
OthersTab.Parent = Frame
OthersTab.Size = UDim2.new(1, -80, 1, -50)
OthersTab.Position = UDim2.new(0, 80, 0, 50)
OthersTab.BackgroundColor3 = Color3.fromRGB(100, 100, 255)
OthersTab.BackgroundTransparency = 0.5
OthersTab.Visible = false

-- Alternância entre abas (fazendo a mensagem "Emilli❤️" desaparecer)
local function ShowTab(tab)
    InitialMessage.Visible = false -- Remove a mensagem inicial ao clicar em uma aba
    TrollTab.Visible = false
    PlayerTab.Visible = false
    OthersTab.Visible = false
    tab.Visible = true
end

-- Criando botões na barra lateral esquerda
local TrollButton = Instance.new("TextButton")
TrollButton.Parent = Tabs
TrollButton.Text = "Troll"
TrollButton.Size = UDim2.new(1, 0, 0.2, 0)
TrollButton.Position = UDim2.new(0, 0, 0, 0)
TrollButton.MouseButton1Click:Connect(function() ShowTab(TrollTab) end)

local PlayerButton = Instance.new("TextButton")
PlayerButton.Parent = Tabs
PlayerButton.Text = "Player"
PlayerButton.Size = UDim2.new(1, 0, 0.2, 0)
PlayerButton.Position = UDim2.new(0, 0, 0.2, 0)
PlayerButton.MouseButton1Click:Connect(function() ShowTab(PlayerTab) end)

local OthersButton = Instance.new("TextButton")
OthersButton.Parent = Tabs
OthersButton.Text = "Others"
OthersButton.Size = UDim2.new(1, 0, 0.2, 0)
OthersButton.Position = UDim2.new(0, 0, 0.4, 0)
OthersButton.MouseButton1Click:Connect(function() ShowTab(OthersTab) end)

-- Botão de minimizar dentro da barra lateral
local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Parent = Tabs
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(1, 0, 0.2, 0)
MinimizeButton.Position = UDim2.new(0, 0, 0.6, 0)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)

MinimizeButton.MouseButton1Click:Connect(function()
    Frame.Visible = false -- Esconde a interface principal
    Tabs.Visible = false
    MinimizedFrame.Visible = true -- Mostra o quadrado móvel
end)

-- Botão de fechar dentro da barra lateral
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Tabs
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(1, 0, 0.2, 0)
CloseButton.Position = UDim2.new(0, 0, 0.8, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)
