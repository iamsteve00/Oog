-- Criação da Tela Principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "EmilliHub"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Mensagem de Boas-vindas Centralizada
local WelcomeFrame = Instance.new("Frame")
WelcomeFrame.Size = UDim2.new(0.5, 0, 0.2, 0)
WelcomeFrame.Position = UDim2.new(0.25, 0, 0.4, 0)
WelcomeFrame.BackgroundTransparency = 0.5
WelcomeFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
WelcomeFrame.BorderSizePixel = 0
WelcomeFrame.Parent = ScreenGui

local WelcomeText = Instance.new("TextLabel")
WelcomeText.Size = UDim2.new(1, 0, 1, 0)
WelcomeText.BackgroundTransparency = 1
WelcomeText.Text = "Bem-vindo ao Emilli Hub!"
WelcomeText.Font = Enum.Font.GothamBold
WelcomeText.TextSize = 30
WelcomeText.TextColor3 = Color3.fromRGB(255, 0, 0)
WelcomeText.Parent = WelcomeFrame

-- Animação de Fade In e Fade Out
WelcomeFrame.Visible = true
WelcomeFrame.BackgroundTransparency = 1
WelcomeText.TextTransparency = 1

task.spawn(function()
    for i = 1, 0, -0.05 do
        WelcomeFrame.BackgroundTransparency = i
        WelcomeText.TextTransparency = i
        task.wait(0.05)
    end
    task.wait(2)
    for i = 0, 1, 0.05 do
        WelcomeFrame.BackgroundTransparency = i
        WelcomeText.TextTransparency = i
        task.wait(0.05)
    end
    WelcomeFrame:Destroy()
end)

-- Interface Principal do Hub
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 600, 0, 400)
MainFrame.Position = UDim2.new(0.5, -300, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.BorderColor3 = Color3.fromRGB(255, 0, 0)
MainFrame.BorderSizePixel = 2
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui
MainFrame.Visible = false -- Só aparece depois da mensagem

-- Delay para aparecer
task.delay(5, function()
    MainFrame.Visible = true
end)

-- Layout lateral com Ícones
local SideBar = Instance.new("Frame")
SideBar.Size = UDim2.new(0, 60, 1, 0)
SideBar.Position = UDim2.new(0, 0, 0, 0)
SideBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
SideBar.Parent = MainFrame

local SideLayout = Instance.new("UIListLayout")
SideLayout.Parent = SideBar
SideLayout.SortOrder = Enum.SortOrder.LayoutOrder
SideLayout.Padding = UDim.new(0, 10)

-- Botões de Minimize e Fechar
local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Size = UDim2.new(0, 25, 0, 25)
MinimizeButton.Position = UDim2.new(1, -60, 0, 10)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MinimizeButton.Text = "-"
MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeButton.Parent = MainFrame

local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 25, 0, 25)
CloseButton.Position = UDim2.new(1, -30, 0, 10)
CloseButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.Parent = MainFrame

-- Ações dos botões
MinimizeButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Título no Topo
local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(1, 0, 0, 40)
TitleLabel.Position = UDim2.new(0, 0, 0, 0)
TitleLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
TitleLabel.BorderSizePixel = 0
TitleLabel.Text = "Brookhaven RP | Português"
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextSize = 18
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.Parent = MainFrame

-- Área de Páginas
local PageContainer = Instance.new("Frame")
PageContainer.Size = UDim2.new(1, -70, 1, -50)
PageContainer.Position = UDim2.new(0, 70, 0, 50)
PageContainer.BackgroundTransparency = 1
PageContainer.Parent = MainFrame

local Pages = {}

-- Função para Criar Páginas
local function CreatePage(name)
    local page = Instance.new("ScrollingFrame")
    page.Size = UDim2.new(1, 0, 1, 0)
    page.CanvasSize = UDim2.new(0, 0, 5, 0)
    page.BackgroundTransparency = 1
    page.Visible = false
    page.Parent = PageContainer
    Pages[name] = page
end

-- Lista de Abas
local TabNames = {"Troll", "Movimentação", "Visual", "Admin", "Música", "Config"}

for _, name in ipairs(TabNames) do
    CreatePage(name)

    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, 0, 0, 40)
    button.Text = name
    button.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.Gotham
    button.TextSize = 14
    button.Parent = SideBar

    button.MouseButton1Click:Connect(function()
        for _, page in pairs(Pages) do
            page.Visible = false
        end
        Pages[name].Visible = true
    end)
end-- Funções Troll dentro da página Troll
local TrollPage = Pages["Troll"]

-- Função: Crashar Jogadores (Fake Kick)
local CrashButton = Instance.new("TextButton")
CrashButton.Size = UDim2.new(0, 200, 0, 40)
CrashButton.Position = UDim2.new(0, 10, 0, 10)
CrashButton.Text = "Crashar Jogadores"
CrashButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
CrashButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CrashButton.Font = Enum.Font.Gotham
CrashButton.TextSize = 14
CrashButton.Parent = TrollPage

CrashButton.MouseButton1Click:Connect(function()
    for _, player in ipairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            player:Kick("Você foi desconectado pelo Emilli Hub!")
        end
    end
end)

-- Função: Buggar Animações
local BugAnimationButton = Instance.new("TextButton")
BugAnimationButton.Size = UDim2.new(0, 200, 0, 40)
BugAnimationButton.Position = UDim2.new(0, 10, 0, 60)
BugAnimationButton.Text = "Buggar Animações"
BugAnimationButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
BugAnimationButton.TextColor3 = Color3.fromRGB(255, 255, 255)
BugAnimationButton.Font = Enum.Font.Gotham
BugAnimationButton.TextSize = 14
BugAnimationButton.Parent = TrollPage

BugAnimationButton.MouseButton1Click:Connect(function()
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChildOfClass("Humanoid") then
        character:FindFirstChildOfClass("Humanoid"):ChangeState(Enum.HumanoidStateType.StrafingNoPhysics)
    end
end)

-- Função: Fazer Player girar sem parar
local SpinButton = Instance.new("TextButton")
SpinButton.Size = UDim2.new(0, 200, 0, 40)
SpinButton.Position = UDim2.new(0, 10, 0, 110)
SpinButton.Text = "Girar Sem Parar"
SpinButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
SpinButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SpinButton.Font = Enum.Font.Gotham
SpinButton.TextSize = 14
SpinButton.Parent = TrollPage

local spinning = false
SpinButton.MouseButton1Click:Connect(function()
    spinning = not spinning
    if spinning then
        task.spawn(function()
            while spinning do
                local character = game.Players.LocalPlayer.Character
                if character and character:FindFirstChild("HumanoidRootPart") then
                    character.HumanoidRootPart.CFrame = character.HumanoidRootPart.CFrame * CFrame.Angles(0, math.rad(30), 0)
                end
                task.wait(0.1)
            end
        end)
    end
end)-- Funções de Movimentação dentro da página Movimentação
local MovPage = Pages["Movimentação"]

-- Fly
local FlyButton = Instance.new("TextButton")
FlyButton.Size = UDim2.new(0, 200, 0, 40)
FlyButton.Position = UDim2.new(0, 10, 0, 10)
FlyButton.Text = "Ativar Fly (E para voar)"
FlyButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
FlyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
FlyButton.Font = Enum.Font.Gotham
FlyButton.TextSize = 14
FlyButton.Parent = MovPage

local flying = false
local UIS = game:GetService("UserInputService")
local runService = game:GetService("RunService")

FlyButton.MouseButton1Click:Connect(function()
    flying = not flying
    local player = game.Players.LocalPlayer
    local char = player.Character or player.CharacterAdded:Wait()
    local humanoidRoot = char:WaitForChild("HumanoidRootPart")
    local bodyGyro = Instance.new("BodyGyro")
    local bodyVelocity = Instance.new("BodyVelocity")
    
    if flying then
        bodyGyro.P = 9e4
        bodyGyro.Parent = humanoidRoot
        bodyVelocity.Velocity = Vector3.zero
        bodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)
        bodyVelocity.Parent = humanoidRoot

        runService.RenderStepped:Connect(function()
            if flying then
                bodyGyro.CFrame = workspace.CurrentCamera.CFrame
                local moveVector = Vector3.zero
                if UIS:IsKeyDown(Enum.KeyCode.W) then
                    moveVector = moveVector + workspace.CurrentCamera.CFrame.LookVector
                end
                if UIS:IsKeyDown(Enum.KeyCode.S) then
                    moveVector = moveVector - workspace.CurrentCamera.CFrame.LookVector
                end
                if UIS:IsKeyDown(Enum.KeyCode.A) then
                    moveVector = moveVector - workspace.CurrentCamera.CFrame.RightVector
                end
                if UIS:IsKeyDown(Enum.KeyCode.D) then
                    moveVector = moveVector + workspace.CurrentCamera.CFrame.RightVector
                end
                bodyVelocity.Velocity = moveVector * 50
            else
                bodyGyro:Destroy()
                bodyVelocity:Destroy()
            end
        end)
    end
end)

-- Speed
local SpeedButton = Instance.new("TextButton")
SpeedButton.Size = UDim2.new(0, 200, 0, 40)
SpeedButton.Position = UDim2.new(0, 10, 0, 60)
SpeedButton.Text = "Ativar Speed"
SpeedButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
SpeedButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedButton.Font = Enum.Font.Gotham
SpeedButton.TextSize = 14
SpeedButton.Parent = MovPage

local speedOn = false
SpeedButton.MouseButton1Click:Connect(function()
    speedOn = not speedOn
    local humanoid = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid")
    if humanoid then
        if speedOn then
            humanoid.WalkSpeed = 80
        else
            humanoid.WalkSpeed = 16
        end
    end
end)

-- NoClip
local NoclipButton = Instance.new("TextButton")
NoclipButton.Size = UDim2.new(0, 200, 0, 40)
NoclipButton.Position = UDim2.new(0, 10, 0, 110)
NoclipButton.Text = "Ativar NoClip (B para atravessar)"
NoclipButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
NoclipButton.TextColor3 = Color3.fromRGB(255, 255, 255)
NoclipButton.Font = Enum.Font.Gotham
NoclipButton.TextSize = 14
NoclipButton.Parent = MovPage

local noclip = false
local function NoClipLoop()
    if noclip then
        for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
            if v:IsA("BasePart") and v.CanCollide then
                v.CanCollide = false
            end
        end
    end
end

NoclipButton.MouseButton1Click:Connect(function()
    noclip = not noclip
end)

game:GetService("RunService").Stepped:Connect(function()
    if noclip then
        NoClipLoop()
    end
end)-- Funções de Visual dentro da página Visual
local VisualPage = Pages["Visual"]

-- FullBright
local FullBrightButton = Instance.new("TextButton")
FullBrightButton.Size = UDim2.new(0, 200, 0, 40)
FullBrightButton.Position = UDim2.new(0, 10, 0, 10)
FullBrightButton.Text = "Ativar FullBright"
FullBrightButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
FullBrightButton.TextColor3 = Color3.fromRGB(255, 255, 255)
FullBrightButton.Font = Enum.Font.Gotham
FullBrightButton.TextSize = 14
FullBrightButton.Parent = VisualPage

local brightOn = false
FullBrightButton.MouseButton1Click:Connect(function()
    brightOn = not brightOn
    if brightOn then
        game.Lighting.Brightness = 2
        game.Lighting.ClockTime = 14
        game.Lighting.FogEnd = 100000
        game.Lighting.GlobalShadows = false
    else
        game.Lighting.Brightness = 1
        game.Lighting.ClockTime = 12
        game.Lighting.FogEnd = 1000
        game.Lighting.GlobalShadows = true
    end
end)

-- ESP (Player Highlight)
local ESPButton = Instance.new("TextButton")
ESPButton.Size = UDim2.new(0, 200, 0, 40)
ESPButton.Position = UDim2.new(0, 10, 0, 60)
ESPButton.Text = "Ativar ESP (ver jogadores)"
ESPButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
ESPButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ESPButton.Font = Enum.Font.Gotham
ESPButton.TextSize = 14
ESPButton.Parent = VisualPage

local espOn = false
local function CreateESP(plr)
    if plr.Character then
        local highlight = Instance.new("Highlight")
        highlight.FillColor = Color3.fromRGB(255, 0, 0)
        highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
        highlight.Parent = plr.Character
    end
end

ESPButton.MouseButton1Click:Connect(function()
    espOn = not espOn
    if espOn then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer then
                CreateESP(player)
            end
        end
        game.Players.PlayerAdded:Connect(function(player)
            player.CharacterAdded:Connect(function()
                CreateESP(player)
            end)
        end)
    else
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character then
                for _, obj in pairs(player.Character:GetChildren()) do
                    if obj:IsA("Highlight") then
                        obj:Destroy()
                    end
                end
            end
        end
    end
end)

-- Remove Fog (Remover Neblina)
local RemoveFogButton = Instance.new("TextButton")
RemoveFogButton.Size = UDim2.new(0, 200, 0, 40)
RemoveFogButton.Position = UDim2.new(0, 10, 0, 110)
RemoveFogButton.Text = "Remover Neblina"
RemoveFogButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
RemoveFogButton.TextColor3 = Color3.fromRGB(255, 255, 255)
RemoveFogButton.Font = Enum.Font.Gotham
RemoveFogButton.TextSize = 14
RemoveFogButton.Parent = VisualPage

RemoveFogButton.MouseButton1Click:Connect(function()
    game.Lighting.FogEnd = 100000
end)-- Funções de Admin dentro da página Admin
local AdminPage = Pages["Admin"]

-- Input para nome do player alvo
local AdminNameBox = Instance.new("TextBox")
AdminNameBox.Size = UDim2.new(0, 200, 0, 40)
AdminNameBox.Position = UDim2.new(0, 10, 0, 10)
AdminNameBox.PlaceholderText = "Nome do Jogador"
AdminNameBox.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
AdminNameBox.TextColor3 = Color3.fromRGB(255, 255, 255)
AdminNameBox.Font = Enum.Font.Gotham
AdminNameBox.TextSize = 14
AdminNameBox.Parent = AdminPage

-- Botão "Banir Player"
local BanButton = Instance.new("TextButton")
BanButton.Size = UDim2.new(0, 200, 0, 40)
BanButton.Position = UDim2.new(0, 10, 0, 60)
BanButton.Text = "Banir Jogador"
BanButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
BanButton.TextColor3 = Color3.fromRGB(255, 255, 255)
BanButton.Font = Enum.Font.Gotham
BanButton.TextSize = 14
BanButton.Parent = AdminPage

BanButton.MouseButton1Click:Connect(function()
    local targetName = AdminNameBox.Text
    local targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer then
        targetPlayer:Kick("Você foi banido pelo Administrador.")
    end
end)

-- Botão "Kickar Player"
local KickButton = Instance.new("TextButton")
KickButton.Size = UDim2.new(0, 200, 0, 40)
KickButton.Position = UDim2.new(0, 10, 0, 110)
KickButton.Text = "Expulsar Jogador"
KickButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
KickButton.TextColor3 = Color3.fromRGB(255, 255, 255)
KickButton.Font = Enum.Font.Gotham
KickButton.TextSize = 14
KickButton.Parent = AdminPage

KickButton.MouseButton1Click:Connect(function()
    local targetName = AdminNameBox.Text
    local targetPlayer = game.Players:FindFirstChild(targetName)
    if targetPlayer then
        targetPlayer:Kick("Você foi expulso pelo Administrador.")
    end
end)

-- Botão "Tornar-se Admin (ON/OFF)"
local AdminToggleButton = Instance.new("TextButton")
AdminToggleButton.Size = UDim2.new(0, 200, 0, 40)
AdminToggleButton.Position = UDim2.new(0, 10, 0, 160)
AdminToggleButton.Text = "Ativar Admin"
AdminToggleButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
AdminToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
AdminToggleButton.Font = Enum.Font.Gotham
AdminToggleButton.TextSize = 14
AdminToggleButton.Parent = AdminPage

local adminOn = false
local badgeGui = nil

AdminToggleButton.MouseButton1Click:Connect(function()
    adminOn = not adminOn
    if adminOn then
        AdminToggleButton.Text = "Desativar Admin"
        -- Adiciona um crachá no player
        badgeGui = Instance.new("BillboardGui")
        badgeGui.Size = UDim2.new(0, 100, 0, 50)
        badgeGui.Adornee = game.Players.LocalPlayer.Character:WaitForChild("Head")
        badgeGui.AlwaysOnTop = true

        local label = Instance.new("TextLabel")
        label.Size = UDim2.new(1, 0, 1, 0)
        label.BackgroundTransparency = 1
        label.Text = "Administrador Brookhaven"
        label.TextColor3 = Color3.fromRGB(255, 0, 0)
        label.TextStrokeTransparency = 0
        label.Font = Enum.Font.GothamBold
        label.TextSize = 14
        label.Parent = badgeGui

        badgeGui.Parent = game.Players.LocalPlayer.Character
    else
        AdminToggleButton.Text = "Ativar Admin"
        if badgeGui then
            badgeGui:Destroy()
            badgeGui = nil
        end
    end
end)
