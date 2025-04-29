-- Criação da Interface Principal
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "EmilliHub"

-- Mensagem de Boas-Vindas
local Welcome = Instance.new("TextLabel", ScreenGui)
Welcome.Size = UDim2.new(0.3, 0, 0.1, 0)
Welcome.Position = UDim2.new(0.35, 0, 0.45, 0)
Welcome.Text = "Bem-vindo ao Emilli Hub!"
Welcome.TextScaled = true
Welcome.TextColor3 = Color3.new(1, 1, 1)
Welcome.BackgroundTransparency = 1
Welcome.Font = Enum.Font.GothamBold

-- Fade in/out
task.spawn(function()
	for i = 0, 1, 0.05 do
		Welcome.TextTransparency = i
		task.wait(0.05)
	end
	Welcome:Destroy()
end)

-- Janela Principal
local Main = Instance.new("Frame", ScreenGui)
Main.Size = UDim2.new(0, 600, 0, 400)
Main.Position = UDim2.new(0.3, 0, 0.2, 0)
Main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Main.BorderSizePixel = 0
Main.Visible = true

-- Título
local Title = Instance.new("TextLabel", Main)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "Brookhaven RP | Português"
Title.TextScaled = true
Title.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.GothamBold

-- Botões de Minimizar e Fechar
local Close = Instance.new("TextButton", Title)
Close.Size = UDim2.new(0, 40, 0, 40)
Close.Position = UDim2.new(1, -40, 0, 0)
Close.Text = "X"
Close.TextColor3 = Color3.new(1, 0, 0)
Close.BackgroundTransparency = 1
Close.Font = Enum.Font.GothamBold
Close.MouseButton1Click:Connect(function() ScreenGui:Destroy() end)

local Minimize = Instance.new("TextButton", Title)
Minimize.Size = UDim2.new(0, 40, 0, 40)
Minimize.Position = UDim2.new(1, -80, 0, 0)
Minimize.Text = "_"
Minimize.TextColor3 = Color3.new(1, 1, 0)
Minimize.BackgroundTransparency = 1
Minimize.Font = Enum.Font.GothamBold

local ContentFrame = Instance.new("Frame", Main)
ContentFrame.Position = UDim2.new(0, 50, 0, 40)
ContentFrame.Size = UDim2.new(1, -50, 1, -40)
ContentFrame.BackgroundTransparency = 1

-- Aba Lateral com Ícones
local Tabs = Instance.new("Frame", Main)
Tabs.Size = UDim2.new(0, 50, 1, 0)
Tabs.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Tabs.BorderSizePixel = 0

-- Função para criar botões de aba
local function createTab(name, icon, callback)
	local tab = Instance.new("TextButton", Tabs)
	tab.Size = UDim2.new(1, 0, 0, 50)
	tab.Text = icon
	tab.Font = Enum.Font.SourceSansBold
	tab.TextSize = 24
	tab.TextColor3 = Color3.fromRGB(255, 255, 255)
	tab.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	tab.BorderSizePixel = 0
	tab.MouseButton1Click:Connect(callback)
end

-- Exemplo de Criação de Abas (continuaremos na Parte 6)
createTab("Troll", "😈", function()
	-- mostrar conteúdo da aba troll
end)

createTab("Mov", "🏃", function()
	-- mostrar conteúdo da aba movimentação
end)

createTab("Visual", "👁", function()
	-- mostrar conteúdo da aba visual
end)

createTab("Admin", "🛠", function()
	-- mostrar conteúdo da aba admin
end)

createTab("Música", "🎵", function()
	-- mostrar conteúdo da aba música
end)

createTab("Config", "⚙️", function()
	-- mostrar conteúdo da aba config
end)-- Parte 4 - Funções das Abas: Visual, Admin, Música e Config

-- Visual: Highlight Players
local function highlightPlayers()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Character and not player.Character:FindFirstChild("Highlight") then
            local highlight = Instance.new("Highlight")
            highlight.Name = "Highlight"
            highlight.FillColor = Color3.fromRGB(255, 0, 0)
            highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
            highlight.FillTransparency = 0.5
            highlight.Parent = player.Character
        end
    end
end

highlightPlayers()

-- Admin: Tornar-se Admin (com crachá visível FE)
local isAdmin = false
local function toggleAdmin()
    local char = game.Players.LocalPlayer.Character
    if not char then return end

    if isAdmin then
        local tag = char:FindFirstChild("AdminTag")
        if tag then tag:Destroy() end
        isAdmin = false
    else
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "AdminTag"
        billboard.Size = UDim2.new(0, 200, 0, 50)
        billboard.StudsOffset = Vector3.new(0, 3, 0)
        billboard.Adornee = char:FindFirstChild("Head")
        billboard.AlwaysOnTop = true

        local label = Instance.new("TextLabel", billboard)
        label.Size = UDim2.new(1, 0, 1, 0)
        label.BackgroundTransparency = 1
        label.Text = "Administrador Brookhaven"
        label.TextColor3 = Color3.fromRGB(255, 255, 255)
        label.TextStrokeColor3 = Color3.fromRGB(255, 0, 0)
        label.TextStrokeTransparency = 0
        label.Font = Enum.Font.GothamBold
        label.TextScaled = true

        billboard.Parent = char
        isAdmin = true
    end
end

-- Admin: Get todas as Gamepasses (Fake FE)
local function giveAllGamepasses()
    local char = game.Players.LocalPlayer.Character
    if char then
        local tag = Instance.new("BillboardGui", char:FindFirstChild("Head"))
        tag.Size = UDim2.new(0, 200, 0, 50)
        tag.StudsOffset = Vector3.new(0, 4, 0)
        tag.AlwaysOnTop = true
        local label = Instance.new("TextLabel", tag)
        label.Text = "Todas as Gamepasses Ativadas"
        label.TextColor3 = Color3.fromRGB(0, 255, 0)
        label.BackgroundTransparency = 1
        label.Size = UDim2.new(1, 0, 1, 0)
        label.Font = Enum.Font.GothamBold
        label.TextScaled = true
    end
end

-- Música: Reprodutor de música por ID
local Sound = Instance.new("Sound", game.Workspace)
Sound.Name = "HubMusic"
Sound.Looped = true

local function playMusic(id)
    Sound.SoundId = "rbxassetid://" .. id
    Sound:Play()
end

local function stopMusic()
    Sound:Stop()
end

-- Config: Botão para salvar configurações (simulação)
local function saveConfig()
    print("Configurações salvas (simulação)")
end-- Parte 3 - Funções da Aba Movimentação

-- Fly GUI (FE)
local UIS = game:GetService("UserInputService")
local flying = false
local speed = 50

local function fly()
    local player = game.Players.LocalPlayer
    local char = player.Character
    local hrp = char:WaitForChild("HumanoidRootPart")

    local bv = Instance.new("BodyVelocity")
    bv.Velocity = Vector3.new()
    bv.MaxForce = Vector3.new(1e9, 1e9, 1e9)
    bv.Parent = hrp

    local direction = Vector3.new()

    UIS.InputBegan:Connect(function(input)
        if input.KeyCode == Enum.KeyCode.W then
            direction = Vector3.new(0, 0, -1)
        elseif input.KeyCode == Enum.KeyCode.S then
            direction = Vector3.new(0, 0, 1)
        elseif input.KeyCode == Enum.KeyCode.A then
            direction = Vector3.new(-1, 0, 0)
        elseif input.KeyCode == Enum.KeyCode.D then
            direction = Vector3.new(1, 0, 0)
        end
    end)

    UIS.InputEnded:Connect(function(input)
        direction = Vector3.new()
    end)

    flying = true
    while flying do
        bv.Velocity = hrp.CFrame:VectorToWorldSpace(direction) * speed
        wait()
    end
end

local function stopFly()
    flying = false
    local hrp = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
    for _, obj in pairs(hrp:GetChildren()) do
        if obj:IsA("BodyVelocity") then
            obj:Destroy()
        end
    end
end

-- UI Buttons para Fly (On/Off)
local flyOn = Instance.new("TextButton")
flyOn.Text = "Fly ON"
flyOn.Size = UDim2.new(0, 100, 0, 30)
flyOn.Position = UDim2.new(0.3, 0, 0.2, 0)
flyOn.Parent = game.CoreGui
flyOn.MouseButton1Click:Connect(fly)

local flyOff = Instance.new("TextButton")
flyOff.Text = "Fly OFF"
flyOff.Size = UDim2.new(0, 100, 0, 30)
flyOff.Position = UDim2.new(0.3, 0, 0.25, 0)
flyOff.Parent = game.CoreGui
flyOff.MouseButton1Click:Connect(stopFly)

-- Speed (Controlável)
local speedSlider = Instance.new("TextBox")
speedSlider.Text = "Velocidade: 50"
speedSlider.Size = UDim2.new(0, 200, 0, 30)
speedSlider.Position = UDim2.new(0.3, 0, 0.3, 0)
speedSlider.ClearTextOnFocus = false
speedSlider.Parent = game.CoreGui

speedSlider.FocusLost:Connect(function()
    local val = tonumber(speedSlider.Text)
    if val then
        speed = val
    else
        speedSlider.Text = "Velocidade: 50"
        speed = 50
    end
end)-- Parte 2 do script - Funções na Aba Troll

-- Função para matar o jogador selecionado
local function killPlayer(playerName)
    local player = game.Players:FindFirstChild(playerName)
    if player then
        player:LoadCharacter() -- Mata o jogador
    end
end

-- Função para teleportar o jogador para o jogador selecionado
local function tpPlayer(playerName)
    local player = game.Players:FindFirstChild(playerName)
    if player then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame -- Teleporta para o player
    end
end

-- Função para ver o jogador selecionado (View Player)
local function viewPlayer(playerName, viewMode)
    local player = game.Players:FindFirstChild(playerName)
    if player then
        if viewMode == "On" then
            -- Exibe o jogador selecionado
            player.Character:FindFirstChild("Head").Transparency = 0
        elseif viewMode == "Off" then
            -- Esconde o jogador
            player.Character:FindFirstChild("Head").Transparency = 1
        end
    end
end

-- Adicionando a interface para as funções com barra de digitação para nome do jogador
local function addTrollFunctions()
    -- UI para Kill Player
    local killInput = Instance.new("TextBox")
    killInput.Position = UDim2.new(0.5, 0, 0.3, 0)
    killInput.Size = UDim2.new(0, 200, 0, 30)
    killInput.PlaceholderText = "Digite o nome do jogador"
    killInput.Parent = game.CoreGui

    local killButton = Instance.new("TextButton")
    killButton.Position = UDim2.new(0.5, 0, 0.35, 0)
    killButton.Size = UDim2.new(0, 200, 0, 30)
    killButton.Text = "Matar Jogador"
    killButton.Parent = game.CoreGui
    killButton.MouseButton1Click:Connect(function()
        killPlayer(killInput.Text)
    end)

    -- UI para TP Player
    local tpInput = Instance.new("TextBox")
    tpInput.Position = UDim2.new(0.5, 0, 0.45, 0)
    tpInput.Size = UDim2.new(0, 200, 0, 30)
    tpInput.PlaceholderText = "Digite o nome do jogador"
    tpInput.Parent = game.CoreGui

    local tpButton = Instance.new("TextButton")
    tpButton.Position = UDim2.new(0.5, 0, 0.5, 0)
    tpButton.Size = UDim2.new(0, 200, 0, 30)
    tpButton.Text = "Teletransportar Jogador"
    tpButton.Parent = game.CoreGui
    tpButton.MouseButton1Click:Connect(function()
        tpPlayer(tpInput.Text)
    end)

    -- UI para View Player (On/Off)
    local viewInput = Instance.new("TextBox")
    viewInput.Position = UDim2.new(0.5, 0, 0.6, 0)
    viewInput.Size = UDim2.new(0, 200, 0, 30)
    viewInput.PlaceholderText = "Digite o nome do jogador"
    viewInput.Parent = game.CoreGui

    local viewButtonOn = Instance.new("TextButton")
    viewButtonOn.Position = UDim2.new(0.5, 0, 0.65, 0)
    viewButtonOn.Size = UDim2.new(0, 100, 0, 30)
    viewButtonOn.Text = "Ver Jogador (On)"
    viewButtonOn.Parent = game.CoreGui
    viewButtonOn.MouseButton1Click:Connect(function()
        viewPlayer(viewInput.Text, "On")
    end)

    local viewButtonOff = Instance.new("TextButton")
    viewButtonOff.Position = UDim2.new(0.5, 0, 0.7, 0)
    viewButtonOff.Size = UDim2.new(0, 100, 0, 30)
    viewButtonOff.Text = "Ver Jogador (Off)"
    viewButtonOff.Parent = game.CoreGui
    viewButtonOff.MouseButton1Click:Connect(function()
        viewPlayer(viewInput.Text, "Off")
    end)
end

addTrollFunctions()
