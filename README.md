-- Emilli Hub | Script Completo | Parte 1

-- Serviços
local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local StarterGui = game:GetService("StarterGui")

-- Variáveis
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Função para criar GUI
local function createUI()
    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "EmilliHub"
    screenGui.Parent = playerGui

    -- Tela de Boas-Vindas
    local welcomeFrame = Instance.new("Frame")
    welcomeFrame.Size = UDim2.new(0, 300, 0, 100)
    welcomeFrame.Position = UDim2.new(0.5, -150, 0.5, -50)
    welcomeFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    welcomeFrame.BackgroundTransparency = 1
    welcomeFrame.Parent = screenGui

    local welcomeText = Instance.new("TextLabel")
    welcomeText.Size = UDim2.new(1, 0, 1, 0)
    welcomeText.BackgroundTransparency = 1
    welcomeText.Text = "Bem-vindo ao Emilli Hub"
    welcomeText.TextColor3 = Color3.fromRGB(255, 0, 0)
    welcomeText.TextScaled = true
    welcomeText.Parent = welcomeFrame

    -- Animação Fade In
    TweenService:Create(welcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 0.3}):Play()
    TweenService:Create(welcomeText, TweenInfo.new(1), {TextTransparency = 0}):Play()

    wait(2)

    -- Animação Fade Out
    TweenService:Create(welcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 1}):Play()
    TweenService:Create(welcomeText, TweenInfo.new(1), {TextTransparency = 1}):Play()

    wait(1)

    welcomeFrame:Destroy()

    -- Interface Principal
    local mainFrame = Instance.new("Frame")
    mainFrame.Size = UDim2.new(0, 600, 0, 400)
    mainFrame.Position = UDim2.new(0.5, -300, 0.5, -200)
    mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    mainFrame.Visible = false
    mainFrame.Parent = screenGui

    -- Fade In da Interface
    TweenService:Create(mainFrame, TweenInfo.new(1), {BackgroundTransparency = 0}):Play()
    mainFrame.Visible = true

    -- Botão Minimizar
    local minimizeButton = Instance.new("TextButton")
    minimizeButton.Size = UDim2.new(0, 30, 0, 30)
    minimizeButton.Position = UDim2.new(1, -70, 0, 10)
    minimizeButton.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
    minimizeButton.Text = "-"
    minimizeButton.Parent = mainFrame

    -- Botão Fechar
    local closeButton = Instance.new("TextButton")
    closeButton.Size = UDim2.new(0, 30, 0, 30)
    closeButton.Position = UDim2.new(1, -35, 0, 10)
    closeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    closeButton.Text = "X"
    closeButton.Parent = mainFrame

    -- Minimizar e Fechar Funcionalidade
    minimizeButton.MouseButton1Click:Connect(function()
        mainFrame.Visible = false
    end)

    closeButton.MouseButton1Click:Connect(function()
        screenGui:Destroy()
    end)

    return mainFrame
end

-- Criar UI
local mainFrame = createUI()

-- Função para criar Abas Laterais
local function createSidebar(frame)
    local sidebar = Instance.new("Frame")
    sidebar.Size = UDim2.new(0, 60, 1, 0)
    sidebar.Position = UDim2.new(0, 0, 0, 0)
    sidebar.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    sidebar.Parent = frame

    local tabNames = {"Troll", "Movimentação", "Visual", "Admin", "Música", "Config"}
    local tabIcons = {"🙂", "🏃", "👁️", "⚙️", "🎵", "🔧"}
    local tabs = {}

    for i, name in ipairs(tabNames) do
        local button = Instance.new("TextButton")
        button.Size = UDim2.new(1, 0, 0, 50)
        button.Position = UDim2.new(0, 0, 0, (i-1) * 60)
        button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
        button.Text = tabIcons[i]
        button.Font = Enum.Font.SourceSansBold
        button.TextColor3 = Color3.fromRGB(255, 255, 255)
        button.TextScaled = true
        button.Parent = sidebar

        tabs[name] = button
    end

    return tabs
end

-- Função para criar o Container das Abas
local function createTabContainer(frame)
    local container = Instance.new("Frame")
    container.Size = UDim2.new(1, -60, 1, 0)
    container.Position = UDim2.new(0, 60, 0, 0)
    container.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    container.Parent = frame

    return container
end

-- Criando Sidebar e Container
local tabs = createSidebar(mainFrame)
local tabContainer = createTabContainer(mainFrame)

-- Sistema para alternar as abas
local pages = {}

local function createPage(name)
    local page = Instance.new("Frame")
    page.Size = UDim2.new(1, 0, 1, 0)
    page.BackgroundTransparency = 1
    page.Visible = false
    page.Parent = tabContainer

    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, 0, 0, 50)
    label.Position = UDim2.new(0, 0, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = name .. " - Emilli Hub"
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.Font = Enum.Font.SourceSansBold
    label.TextScaled = true
    label.Parent = page

    pages[name] = page
end

for name, _ in pairs(tabs) do
    createPage(name)
end

local function hideAllPages()
    for _, page in pairs(pages) do
        page.Visible = false
    end
end

for name, button in pairs(tabs) do
    button.MouseButton1Click:Connect(function()
        hideAllPages()
        pages[name].Visible = true
    end)
end

-- Mostrar a primeira aba por padrão
pages["Troll"].Visible = true

-- Funções para a Aba Troll
local trollPage = pages["Troll"]

local function createButton(parent, text, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 200, 0, 40)
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextScaled = true
    button.Parent = parent

    button.MouseButton1Click:Connect(callback)

    return button
end

-- Layout para organizar botões
local trollLayout = Instance.new("UIListLayout")
trollLayout.Padding = UDim.new(0, 10)
trollLayout.Parent = trollPage
trollLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
trollLayout.VerticalAlignment = Enum.VerticalAlignment.Top
trollLayout.SortOrder = Enum.SortOrder.LayoutOrder

-- Botões Troll
createButton(trollPage, "Fling Player", function()
    local playerName = game.Players.LocalPlayer.Name
    local character = game.Players.LocalPlayer.Character
    if character then
        local bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.Velocity = Vector3.new(10000, 10000, 10000)
        bodyVelocity.MaxForce = Vector3.new(100000, 100000, 100000)
        bodyVelocity.Parent = character.HumanoidRootPart
        wait(0.1)
        bodyVelocity:Destroy()
    end
end)

createButton(trollPage, "Loop Fling", function()
    local character = game.Players.LocalPlayer.Character
    if character then
        while true do
            local bodyVelocity = Instance.new("BodyVelocity")
            bodyVelocity.Velocity = Vector3.new(10000, 0, 10000)
            bodyVelocity.MaxForce = Vector3.new(100000, 100000, 100000)
            bodyVelocity.Parent = character.HumanoidRootPart
            wait(0.2)
            if bodyVelocity then
                bodyVelocity:Destroy()
            end
        end
    end
end)

createButton(trollPage, "Crash Server (Lag)", function()
    for i = 1, 1000 do
        Instance.new("Part", workspace)
    end
end)

-- Funções para a Aba Movimentação
local movementPage = pages["Movimentação"]

local function createMovementButton(parent, text, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 200, 0, 40)
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextScaled = true
    button.Parent = parent

    button.MouseButton1Click:Connect(callback)

    return button
end

-- Layout para a movimentação
local movementLayout = Instance.new("UIListLayout")
movementLayout.Padding = UDim.new(0, 10)
movementLayout.Parent = movementPage
movementLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
movementLayout.VerticalAlignment = Enum.VerticalAlignment.Top
movementLayout.SortOrder = Enum.SortOrder.LayoutOrder

-- Fly Button
createMovementButton(movementPage, "Fly", function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
    
    local flying = true
    local speed = 50

    local bodyGyro = Instance.new("BodyGyro", humanoidRootPart)
    bodyGyro.P = 9e4
    bodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
    bodyGyro.CFrame = humanoidRootPart.CFrame

    local bodyVelocity = Instance.new("BodyVelocity", humanoidRootPart)
    bodyVelocity.Velocity = Vector3.new(0,0,0)
    bodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)

    game:GetService("UserInputService").InputBegan:Connect(function(input)
        if flying then
            if input.KeyCode == Enum.KeyCode.W then
                bodyVelocity.Velocity = workspace.CurrentCamera.CFrame.LookVector * speed
            elseif input.KeyCode == Enum.KeyCode.S then
                bodyVelocity.Velocity = -workspace.CurrentCamera.CFrame.LookVector * speed
            elseif input.KeyCode == Enum.KeyCode.A then
                bodyVelocity.Velocity = -workspace.CurrentCamera.CFrame.RightVector * speed
            elseif input.KeyCode == Enum.KeyCode.D then
                bodyVelocity.Velocity = workspace.CurrentCamera.CFrame.RightVector * speed
            end
        end
    end)
end)

-- Speed Button
createMovementButton(movementPage, "Speed", function()
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChild("Humanoid") then
        character.Humanoid.WalkSpeed = 120
    end
end)

-- NoClip Button
createMovementButton(movementPage, "NoClip", function()
    local noclip = true
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    game:GetService("RunService").Stepped:Connect(function()
        if noclip and character and character:FindFirstChild("HumanoidRootPart") then
            character.HumanoidRootPart.CanCollide = false
        end
    end)
end)

-- Funções para a Aba Visual
local visualPage = pages["Visual"]

local function createVisualButton(parent, text, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 200, 0, 40)
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextScaled = true
    button.Parent = parent

    button.MouseButton1Click:Connect(callback)

    return button
end

-- Layout para a aba Visual
local visualLayout = Instance.new("UIListLayout")
visualLayout.Padding = UDim.new(0, 10)
visualLayout.Parent = visualPage
visualLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
visualLayout.VerticalAlignment = Enum.VerticalAlignment.Top
visualLayout.SortOrder = Enum.SortOrder.LayoutOrder

-- ESP (Highlight todos jogadores)
createVisualButton(visualPage, "ESP (Destacar Jogadores)", function()
    for _,player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            local character = player.Character
            if character then
                local highlight = Instance.new("Highlight")
                highlight.FillColor = Color3.fromRGB(255, 0, 0)
                highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
                highlight.Parent = character
            end
        end
    end
end)

-- Remover ESP
createVisualButton(visualPage, "Remover ESP", function()
    for _,player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            local character = player.Character
            if character then
                for _,obj in pairs(character:GetChildren()) do
                    if obj:IsA("Highlight") then
                        obj:Destroy()
                    end
                end
            end
        end
    end
end)

-- Ver Todos (Remove Fog e ilumina o mapa)
createVisualButton(visualPage, "Ver Todos (Sem Nevoeiro)", function()
    if workspace:FindFirstChildOfClass("Terrain") then
        workspace.Terrain.FogEnd = 100000
    end
    game.Lighting.FogEnd = 100000
    game.Lighting.Brightness = 5
    game.Lighting.GlobalShadows = false
end)

-- Resetar Visual
createVisualButton(visualPage, "Resetar Visual", function()
    if workspace:FindFirstChildOfClass("Terrain") then
        workspace.Terrain.FogEnd = 500
    end
    game.Lighting.FogEnd = 500
    game.Lighting.Brightness = 2
    game.Lighting.GlobalShadows = true
end)

-- Funções para a Aba Admin
local adminPage = pages["Admin"]

local function createAdminButton(parent, text, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 200, 0, 40)
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.SourceSansBold
    button.TextScaled = true
    button.Parent = parent

    button.MouseButton1Click:Connect(callback)

    return button
end

local adminLayout = Instance.new("UIListLayout")
adminLayout.Padding = UDim.new(0, 10)
adminLayout.Parent = adminPage
adminLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
adminLayout.VerticalAlignment = Enum.VerticalAlignment.Top
adminLayout.SortOrder = Enum.SortOrder.LayoutOrder

-- Tornar-se Admin (Fake Admin Power)
createAdminButton(adminPage, "Tornar-se Admin", function()
    local player = game.Players.LocalPlayer
    local adminTag = Instance.new("BillboardGui")
    adminTag.Size = UDim2.new(0, 100, 0, 50)
    adminTag.Adornee = player.Character:WaitForChild("Head")
    adminTag.AlwaysOnTop = true

    local textLabel = Instance.new("TextLabel")
    textLabel.Text = "ADMIN"
    textLabel.BackgroundTransparency = 1
    textLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
    textLabel.TextScaled = true
    textLabel.Font = Enum.Font.SourceSansBold
    textLabel.Size = UDim2.new(1, 0, 1, 0)
    textLabel.Parent = adminTag

    adminTag.Parent = player.Character
end)

-- Banir jogador
createAdminButton(adminPage, "Banir Player", function()
    local banName = InputPlayerName.Text
    local target = game.Players:FindFirstChild(banName)
    if target then
        target:Kick("Você foi banido pelo slime!")
    else
        warn("Jogador não encontrado.")
    end
end)

-- Kickar jogador
createAdminButton(adminPage, "Kickar Player", function()
    local kickName = InputPlayerName.Text
    local target = game.Players:FindFirstChild(kickName)
    if target then
        target:Kick("Você foi expulso pelo slime!")
    else
        warn("Jogador não encontrado.")
    end
end)
