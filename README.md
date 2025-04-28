-- Emilli Hub VERSÃO FINAL
-- Parte 1 de 7

-- Serviços
local Players = game:GetService("Players")
local StarterGui = game:GetService("StarterGui")
local RunService = game:GetService("RunService")
local LocalPlayer = Players.LocalPlayer

-- Criar a Interface
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "EmilliHub"

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 450, 0, 400)
MainFrame.Position = UDim2.new(0.5, -225, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(30,30,30)
MainFrame.BorderSizePixel = 0
MainFrame.Visible = false

local UICorner = Instance.new("UICorner", MainFrame)
UICorner.CornerRadius = UDim.new(0, 8)

-- Título
local Title = Instance.new("TextLabel", MainFrame)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.BackgroundTransparency = 1
Title.Text = "Brookhaven RP | Português"
Title.Font = Enum.Font.GothamBold
Title.TextColor3 = Color3.fromRGB(255,0,0)
Title.TextSize = 20

-- Minimize e Close
local Minimize = Instance.new("TextButton", MainFrame)
Minimize.Size = UDim2.new(0, 30, 0, 30)
Minimize.Position = UDim2.new(1, -70, 0, 5)
Minimize.BackgroundColor3 = Color3.fromRGB(50,50,50)
Minimize.Text = "-"
Minimize.TextColor3 = Color3.new(1,1,1)
local MinimizeCorner = Instance.new("UICorner", Minimize)
MinimizeCorner.CornerRadius = UDim.new(1,0)

local Close = Instance.new("TextButton", MainFrame)
Close.Size = UDim2.new(0, 30, 0, 30)
Close.Position = UDim2.new(1, -35, 0, 5)
Close.BackgroundColor3 = Color3.fromRGB(255,50,50)
Close.Text = "X"
Close.TextColor3 = Color3.new(1,1,1)
local CloseCorner = Instance.new("UICorner", Close)
CloseCorner.CornerRadius = UDim.new(1,0)

-- Funções de Minimizar e Fechar
Minimize.MouseButton1Click:Connect(function()
	MainFrame.Visible = not MainFrame.Visible
end)

Close.MouseButton1Click:Connect(function()
	ScreenGui:Destroy()
end)

-- Animação de Boas-vindas
local WelcomeFrame = Instance.new("Frame", ScreenGui)
WelcomeFrame.Size = UDim2.new(0, 400, 0, 100)
WelcomeFrame.Position = UDim2.new(0.5, -200, 0.5, -50)
WelcomeFrame.BackgroundTransparency = 0.5
WelcomeFrame.BackgroundColor3 = Color3.fromRGB(20,20,20)
WelcomeFrame.Visible = true

local WelcomeUICorner = Instance.new("UICorner", WelcomeFrame)
WelcomeUICorner.CornerRadius = UDim.new(0, 10)

local WelcomeLabel = Instance.new("TextLabel", WelcomeFrame)
WelcomeLabel.Size = UDim2.new(1, 0, 1, 0)
WelcomeLabel.BackgroundTransparency = 1
WelcomeLabel.Text = "Bem-vindo ao Emilli Hub!"
WelcomeLabel.Font = Enum.Font.GothamBold
WelcomeLabel.TextColor3 = Color3.fromRGB(255,0,0)
WelcomeLabel.TextSize = 30

task.spawn(function()
	for i = 1,0,-0.05 do
		WelcomeFrame.BackgroundTransparency = i
		task.wait(0.05)
	end
	task.wait(2)
	for i = 0,1,0.05 do
		WelcomeFrame.BackgroundTransparency = i
		task.wait(0.05)
	end
	WelcomeFrame:Destroy()
	MainFrame.Visible = true
end)

-- Sidebar (Abas)
local Sidebar = Instance.new("Frame", MainFrame)
Sidebar.Size = UDim2.new(0, 70, 1, -40)
Sidebar.Position = UDim2.new(0, 0, 0, 40)
Sidebar.BackgroundColor3 = Color3.fromRGB(40,40,40)

local SidebarCorner = Instance.new("UICorner", Sidebar)
SidebarCorner.CornerRadius = UDim.new(0,8)

-- Conteúdo principal
local ContentFrame = Instance.new("Frame", MainFrame)
ContentFrame.Size = UDim2.new(1, -70, 1, -40)
ContentFrame.Position = UDim2.new(0, 70, 0, 40)
ContentFrame.BackgroundTransparency = 1

-- Tabelas para controle de abas
local Tabs = {}
local CurrentTab

-- Criar função para adicionar Abas
function CreateTab(name, iconId)
	local Button = Instance.new("ImageButton", Sidebar)
	Button.Size = UDim2.new(1, 0, 0, 50)
	Button.BackgroundTransparency = 1
	Button.Image = "rbxassetid://"..iconId
	
	local TabFrame = Instance.new("ScrollingFrame", ContentFrame)
	TabFrame.Size = UDim2.new(1,0,1,0)
	TabFrame.CanvasSize = UDim2.new(0,0,2,0)
	TabFrame.ScrollBarThickness = 6
	TabFrame.BackgroundTransparency = 1
	TabFrame.Visible = false
	
	Button.MouseButton1Click:Connect(function()
		if CurrentTab then
			CurrentTab.Visible = false
		end
		TabFrame.Visible = true
		CurrentTab = TabFrame
	end)
	
	Tabs[name] = TabFrame
end

-- Criar função para adicionar Botões dentro das Abas
function CreateButton(tabName, text, callback)
	local Button = Instance.new("TextButton", Tabs[tabName])
	Button.Size = UDim2.new(1, -10, 0, 40)
	Button.Position = UDim2.new(0,5,0, #Tabs[tabName]:GetChildren()*45)
	Button.BackgroundColor3 = Color3.fromRGB(60,60,60)
	Button.Text = text
	Button.Font = Enum.Font.GothamBold
	Button.TextColor3 = Color3.new(1,1,1)
	Button.TextSize = 18
	Button.BorderSizePixel = 0
	
	local ButtonCorner = Instance.new("UICorner", Button)
	ButtonCorner.CornerRadius = UDim.new(0,6)
	
	Button.MouseButton1Click:Connect(callback)
end)

-- Criando as Abas
CreateTab("Troll", "4483362458") -- ícone de troll
CreateTab("Movimentação", "4483362269") -- ícone de movimento
CreateTab("Visual", "4483362909") -- ícone de olho
CreateTab("Admin", "4483362535") -- ícone de escudo
CreateTab("Música", "4483363015") -- ícone de música
CreateTab("Config", "4483363095") -- ícone de engrenagem

-- Funções Troll
CreateButton("Troll", "Fling Players", function()
    -- Fling clássico
    local character = LocalPlayer.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        local BodyVelocity = Instance.new("BodyVelocity", character.HumanoidRootPart)
        BodyVelocity.Velocity = Vector3.new(0,9999,0)
        BodyVelocity.MaxForce = Vector3.new(999999,999999,999999)
        task.wait(0.5)
        BodyVelocity:Destroy()
    end
end)

CreateButton("Troll", "Teleport Random Player", function()
    local players = Players:GetPlayers()
    if #players > 1 then
        local randomPlayer = players[math.random(1,#players)]
        if randomPlayer ~= LocalPlayer and randomPlayer.Character and randomPlayer.Character:FindFirstChild("HumanoidRootPart") then
            LocalPlayer.Character:MoveTo(randomPlayer.Character.HumanoidRootPart.Position)
        end
    end
end)

-- Funções Movimentação
CreateButton("Movimentação", "Fly (GUI)", function()
    -- Fly via GUI
    local FlyGui = Instance.new("ScreenGui", LocalPlayer.PlayerGui)
    FlyGui.Name = "FlyGui"

    local FlyButton = Instance.new("TextButton", FlyGui)
    FlyButton.Size = UDim2.new(0,200,0,50)
    FlyButton.Position = UDim2.new(0.5,-100,0.9,-25)
    FlyButton.BackgroundColor3 = Color3.fromRGB(50,50,255)
    FlyButton.Text = "Fly: OFF"
    FlyButton.Font = Enum.Font.GothamBold
    FlyButton.TextColor3 = Color3.new(1,1,1)
    FlyButton.TextSize = 20

    local flying = false
    local speed = 50

    FlyButton.MouseButton1Click:Connect(function()
        flying = not flying
        FlyButton.Text = flying and "Fly: ON" or "Fly: OFF"
        
        if flying then
            local char = LocalPlayer.Character
            local humanoidRootPart = char:WaitForChild("HumanoidRootPart")
            local bodyVelocity = Instance.new("BodyVelocity", humanoidRootPart)
            bodyVelocity.MaxForce = Vector3.new(1e5,1e5,1e5)
            bodyVelocity.Name = "FlyVelocity"

            RunService.RenderStepped:Connect(function()
                if not bodyVelocity.Parent then return end
                local cam = workspace.CurrentCamera
                local moveVec = Vector3.new()
                if UserInputService:IsKeyDown(Enum.KeyCode.W) then moveVec = moveVec + cam.CFrame.LookVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.S) then moveVec = moveVec - cam.CFrame.LookVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.A) then moveVec = moveVec - cam.CFrame.RightVector end
                if UserInputService:IsKeyDown(Enum.KeyCode.D) then moveVec = moveVec + cam.CFrame.RightVector end
                bodyVelocity.Velocity = moveVec * speed
            end)
        else
            if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
                local humrp = LocalPlayer.Character.HumanoidRootPart
                if humrp:FindFirstChild("FlyVelocity") then
                    humrp.FlyVelocity:Destroy()
                end
            end
        end
    end)
end)

CreateButton("Movimentação", "Super Velocidade", function()
    local char = LocalPlayer.Character
    if char and char:FindFirstChildOfClass("Humanoid") then
        char.Humanoid.WalkSpeed = 100
    end
end)

CreateButton("Movimentação", "Super Pulo", function()
    local char = LocalPlayer.Character
    if char and char:FindFirstChildOfClass("Humanoid") then
        char.Humanoid.JumpPower = 200
    end
end)

-- Funções Visual
CreateButton("Visual", "ESP Players", function()
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local billboard = Instance.new("BillboardGui", player.Character.HumanoidRootPart)
            billboard.Size = UDim2.new(0,100,0,40)
            billboard.AlwaysOnTop = true
            billboard.Name = "ESPBillboard"

            local label = Instance.new("TextLabel", billboard)
            label.Size = UDim2.new(1,0,1,0)
            label.BackgroundTransparency = 1
            label.Text = player.Name
            label.TextColor3 = Color3.fromRGB(255,0,0)
            label.TextStrokeTransparency = 0
            label.Font = Enum.Font.GothamBold
            label.TextSize = 14
        end
    end
end)

CreateButton("Visual", "Remover ESP", function()
    for _, player in ipairs(Players:GetPlayers()) do
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            if player.Character.HumanoidRootPart:FindFirstChild("ESPBillboard") then
                player.Character.HumanoidRootPart.ESPBillboard:Destroy()
            end
        end
    end
end)

-- Funções Admin
CreateButton("Admin", "Tornar-se Admin (On/Off)", function()
    -- Sistema de Crachá Administrador
    if LocalPlayer.Character and not LocalPlayer.Character:FindFirstChild("AdminBadge") then
        local badge = Instance.new("BillboardGui", LocalPlayer.Character.Head)
        badge.Name = "AdminBadge"
        badge.Size = UDim2.new(0,150,0,50)
        badge.StudsOffset = Vector3.new(0,2,0)
        badge.AlwaysOnTop = true

        local label = Instance.new("TextLabel", badge)
        label.Size = UDim2.new(1,0,1,0)
        label.BackgroundTransparency = 1
        label.Text = "Administrador Brookhaven"
        label.TextColor3 = Color3.fromRGB(255,215,0)
        label.TextStrokeTransparency = 0
        label.Font = Enum.Font.GothamBold
        label.TextSize = 16
    else
        if LocalPlayer.Character:FindFirstChild("AdminBadge") then
            LocalPlayer.Character.AdminBadge:Destroy()
        end
    end
end)

CreateButton("Admin", "Kick Player", function()
    local playerName = CreateInput("Digite o nome do jogador para kickar")
    if playerName ~= "" then
        local target = Players:FindFirstChild(playerName)
        if target then
            target:Kick("Você foi kickado pelo Administrador.")
        end
    end
end)

CreateButton("Admin", "Ban Player (Simulado)", function()
    local playerName = CreateInput("Digite o nome do jogador para banir")
    if playerName ~= "" then
        local target = Players:FindFirstChild(playerName)
        if target then
            target:Kick("Você foi banido permanentemente.")
        end
    end
end)

-- Funções Música
CreateButton("Música", "Tocar Música", function()
    local musicId = CreateInput("Digite o ID da música")
    if musicId ~= "" then
        local sound = Instance.new("Sound", workspace)
        sound.SoundId = "rbxassetid://" .. musicId
        sound:Play()
    end
end)

CreateButton("Música", "Parar Música", function()
    for _, sound in pairs(workspace:GetChildren()) do
        if sound:IsA("Sound") then
            sound:Stop()
        end
    end
end)

-- Funções Config
CreateButton("Config", "Salvar Configurações", function()
    local settings = {
        ["Fly"] = "Off",
        ["ESP"] = "Off",
        ["SuperVel"] = "Off",
        ["SuperJump"] = "Off"
    }
    local savedSettings = game:GetService("DataStoreService"):GetDataStore("HubSettings")
    local success, errorMessage = pcall(function()
        savedSettings:SetAsync(LocalPlayer.UserId, settings)
    end)
    if success then
        print("Configurações salvas com sucesso!")
    else
        print("Erro ao salvar configurações: " .. errorMessage)
    end
end)

CreateButton("Config", "Carregar Configurações", function()
    local savedSettings = game:GetService("DataStoreService"):GetDataStore("HubSettings")
    local settings
    local success, errorMessage = pcall(function()
        settings = savedSettings:GetAsync(LocalPlayer.UserId)
    end)
    if success and settings then
        print("Configurações carregadas!")
        -- Aplicar configurações
        if settings["Fly"] == "On" then
            -- Ativar Fly
        end
        if settings["ESP"] == "On" then
            -- Ativar ESP
        end
        if settings["SuperVel"] == "On" then
            -- Ativar Super Velocidade
        end
        if settings["SuperJump"] == "On" then
            -- Ativar Super Pulo
        end
    else
        print("Erro ao carregar configurações: " .. errorMessage)
    end
end)
