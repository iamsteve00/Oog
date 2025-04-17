local Players = game:GetService("Players")
local player = Players.LocalPlayer
local TweenService = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")

-- Criar tela principal
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "EmilliHub"
screenGui.ResetOnSpawn = false

-- Mensagem de boas-vindas aprimorada
local welcomeFrame = Instance.new("Frame", screenGui)
welcomeFrame.Size = UDim2.new(0.3, 0, 0.15, 0)
welcomeFrame.Position = UDim2.new(0.35, 0, 0.4, 0)
welcomeFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
welcomeFrame.BackgroundTransparency = 1

local welcomeText = Instance.new("TextLabel", welcomeFrame)
welcomeText.Size = UDim2.new(1, 0, 1, 0)
welcomeText.Text = "Bem-vindo ao Emilli Hub"
welcomeText.TextColor3 = Color3.new(1, 1, 1)
welcomeText.TextScaled = true
welcomeText.BackgroundTransparency = 1
welcomeText.Font = Enum.Font.GothamBold

TweenService:Create(welcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 0.2}):Play()
TweenService:Create(welcomeText, TweenInfo.new(1), {TextTransparency = 0}):Play()
task.wait(2)

TweenService:Create(welcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 1}):Play()
TweenService:Create(welcomeText, TweenInfo.new(1), {TextTransparency = 1}):Play()
task.wait(1)

welcomeFrame:Destroy()

-- Criar container principal com interface refinada
local main = Instance.new("Frame", screenGui)
main.Name = "Main"
main.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
main.BorderSizePixel = 0
main.Position = UDim2.new(0.25, 0, 0.2, 0)
main.Size = UDim2.new(0, 500, 0, 350)
main.Visible = true

local UICorner = Instance.new("UICorner", main)
UICorner.CornerRadius = UDim.new(0, 8)

-- Aba lateral com ícones ajustados
local sidebar = Instance.new("Frame", main)
sidebar.Size = UDim2.new(0, 50, 1, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(10, 10, 10)

local UIListLayout = Instance.new("UIListLayout", sidebar)
UIListLayout.Padding = UDim.new(0, 5)
UIListLayout.FillDirection = Enum.FillDirection.Vertical

local Tabs = {
    { Name = "Troll", Icon = "rbxassetid://13670805471" },
    { Name = "Movimentação", Icon = "rbxassetid://13670814386" },
    { Name = "Visual", Icon = "rbxassetid://13670816429" },
    { Name = "Admin", Icon = "rbxassetid://13670817756" },
    { Name = "Música", Icon = "rbxassetid://13670818967" },
    { Name = "Config", Icon = "rbxassetid://13670819923" }
}

local SelectedTab = nil
local TabButtons = {}

-- Criar conteúdo das abas com aparência refinada
local content = Instance.new("Frame", main)
content.Size = UDim2.new(1, -50, 1, 0)
content.Position = UDim2.new(0, 50, 0, 0)
content.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

local UICornerContent = Instance.new("UICorner", content)
UICornerContent.CornerRadius = UDim.new(0, 8)

-- Criar botões das abas com animação aprimorada
for i, tab in ipairs(Tabs) do
    local Button = Instance.new("ImageButton", sidebar)
    Button.Name = tab.Name .. "Tab"
    Button.Size = UDim2.new(1, 0, 0, 40)
    Button.BackgroundTransparency = 1
    Button.Image = tab.Icon
    Button.ImageColor3 = Color3.fromRGB(200, 200, 200)

    Button.MouseEnter:Connect(function()
        Button.ImageColor3 = Color3.fromRGB(255, 0, 0)
    end)
    Button.MouseLeave:Connect(function()
        if SelectedTab ~= Button then
            Button.ImageColor3 = Color3.fromRGB(200, 200, 200)
        end
    end)

    -- Criar páginas das abas
    local TabFrame = Instance.new("ScrollingFrame", content)
    TabFrame.Name = tab.Name
    TabFrame.Size = UDim2.new(1, 0, 1, 0)
    TabFrame.BackgroundTransparency = 1
    TabFrame.Visible = false
    TabFrame.BorderSizePixel = 0
    TabFrame.CanvasSize = UDim2.new(0, 0, 2, 0)

    local UIListLayoutTab = Instance.new("UIListLayout", TabFrame)
    UIListLayoutTab.Padding = UDim.new(0, 5)
    UIListLayoutTab.SortOrder = Enum.SortOrder.LayoutOrder

    Button.MouseButton1Click:Connect(function()
        for _, page in ipairs(content:GetChildren()) do
            if page:IsA("ScrollingFrame") then
                page.Visible = false
            end
        end
        for _, otherButton in ipairs(TabButtons) do
            otherButton.ImageColor3 = Color3.fromRGB(200, 200, 200)
        end

        local TargetTab = content:FindFirstChild(tab.Name)
        if TargetTab then
            TargetTab.Visible = true
        end
        Button.ImageColor3 = Color3.fromRGB(255, 0, 0)
        SelectedTab = Button
    end)

    table.insert(TabButtons, Button)
end

-- Exibir a primeira aba por padrão
TabButtons[1].MouseButton1Click:Fire()

-- Adicionar efeito Fade-In à interface
TweenService:Create(main, TweenInfo.new(1), {Visible = true}):Play()
