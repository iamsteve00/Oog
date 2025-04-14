-- Serviços do Roblox
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")

-- Mensagem de boas-vindas antes da interface aparecer
local function ShowWelcomeMessage()
    local WelcomeScreen = Instance.new("ScreenGui")
    local WelcomeLabel = Instance.new("TextLabel")

    WelcomeScreen.Parent = game.CoreGui

    WelcomeLabel.Parent = WelcomeScreen
    WelcomeLabel.Text = "Bem-vindo ao script Emilli Hub"
    WelcomeLabel.Size = UDim2.new(1, 0, 1, 0)
    WelcomeLabel.TextScaled = true
    WelcomeLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    WelcomeLabel.TextColor3 = Color3.fromRGB(255, 255, 255)

    wait(2) -- Aguarda 2 segundos antes de carregar a interface

    WelcomeScreen:Destroy()
end

ShowWelcomeMessage()

-- Criando GUI principal
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Parent = game.CoreGui
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)
Frame.BackgroundTransparency = 0.5 -- Meio transparente

-- Barra lateral para abas
local Tabs = Instance.new("Frame")
Tabs.Parent = Frame
Tabs.Size = UDim2.new(0, 80, 1, 0)
Tabs.Position = UDim2.new(0, 0, 0, 0)
Tabs.BackgroundColor3 = Color3.fromRGB(200, 100, 100)
Tabs.BackgroundTransparency = 0.5

-- Mensagem dentro da interface
local InitialMessage = Instance.new("TextLabel")
InitialMessage.Parent = Frame
InitialMessage.Text = "Emilli❤️"
InitialMessage.Size = UDim2.new(1, -80, 1, -50)
InitialMessage.Position = UDim2.new(0, 80, 0, 50)
InitialMessage.BackgroundTransparency = 1
InitialMessage.TextColor3 = Color3.fromRGB(255, 255, 255)
InitialMessage.TextScaled = true

-- Criando abas
local TrollTab = Instance.new("Frame")
local PlayerTab = Instance.new("Frame")
local OthersTab = Instance.new("Frame")

TrollTab.Parent = Frame
TrollTab.Size = UDim2.new(1, -80, 1, -50)
TrollTab.Position = UDim2.new(0, 80, 0, 50)
TrollTab.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
TrollTab.Visible = false

PlayerTab.Parent = Frame
PlayerTab.Size = UDim2.new(1, -80, 1, -50)
PlayerTab.Position = UDim2.new(0, 80, 0, 50)
PlayerTab.BackgroundColor3 = Color3.fromRGB(100, 255, 100)
PlayerTab.Visible = false

OthersTab.Parent = Frame
OthersTab.Size = UDim2.new(1, -80, 1, -50)
OthersTab.Position = UDim2.new(0, 80, 0, 50)
OthersTab.BackgroundColor3 = Color3.fromRGB(100, 100, 255)
OthersTab.Visible = false

-- Criando barra de entrada de nome
local InputBox = Instance.new("TextBox")
InputBox.Parent = Frame
InputBox.Size = UDim2.new(0, 200, 0, 30)
InputBox.Position = UDim2.new(0, 90, 0, 10)
InputBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
InputBox.Text = "Digite o nome do jogador"

-- Botões para Void Player e View
local VoidButton = Instance.new("TextButton")
VoidButton.Parent = TrollTab
VoidButton.Size = UDim2.new(0, 100, 0, 30)
VoidButton.Position = UDim2.new(0.5, -50, 0.2, 0)
VoidButton.Text = "Void Player"

VoidButton.MouseButton1Click:Connect(function()
    local playerName = InputBox.Text
    local targetPlayer = game.Players:FindFirstChild(playerName)
    if targetPlayer then
        targetPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(9999, 9999, 9999))
    end
end)

local ViewOnButton = Instance.new("TextButton")
ViewOnButton.Parent = OthersTab
ViewOnButton.Size = UDim2.new(0, 100, 0, 30)
ViewOnButton.Position = UDim2.new(0.5, -50, 0.2, 0)
ViewOnButton.Text = "View ON"

local ViewOffButton = Instance.new("TextButton")
ViewOffButton.Parent = OthersTab
ViewOffButton.Size = UDim2.new(0, 100, 0, 30)
ViewOffButton.Position = UDim2.new(0.5, -50, 0.4, 0)
ViewOffButton.Text = "View OFF"

ViewOnButton.MouseButton1Click:Connect(function()
    local playerName = InputBox.Text
    local targetPlayer = game.Players:FindFirstChild(playerName)
    if targetPlayer then
        game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character.Humanoid
    end
end)

ViewOffButton.MouseButton1Click:Connect(function()
    game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
end)

-- Alternância entre abas
local function ShowTab(tab)
    InitialMessage.Visible = false
    TrollTab.Visible = false
    PlayerTab.Visible = false
    OthersTab.Visible = false
    tab.Visible = true
end

local TrollButton = Instance.new("TextButton")
TrollButton.Parent = Tabs
TrollButton.Text = "Troll"
TrollButton.Size = UDim2.new(1, 0, 0.2, 0)
TrollButton.MouseButton1Click:Connect(function() ShowTab(TrollTab) end)

local PlayerButton = Instance.new("TextButton")
PlayerButton.Parent = Tabs
PlayerButton.Text = "Player"
PlayerButton.Size = UDim2.new(1, 0, 0.2, 0)
PlayerButton.MouseButton1Click:Connect(function() ShowTab(PlayerTab) end)

local OthersButton = Instance.new("TextButton")
OthersButton.Parent = Tabs
OthersButton.Text = "Others"
OthersButton.Size = UDim2.new(1, 0, 0.2, 0)
OthersButton.MouseButton1Click:Connect(function() ShowTab(OthersTab) end)
