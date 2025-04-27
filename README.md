-- Emilli Hub | Sistema Principal
local ScreenGui = Instance.new("ScreenGui")
local WelcomeFrame = Instance.new("Frame")
local WelcomeLabel = Instance.new("TextLabel")
local MainFrame = Instance.new("Frame")
local CloseButton = Instance.new("TextButton")
local MinimizeButton = Instance.new("TextButton")
local TabsFrame = Instance.new("Frame")
local ContentFrame = Instance.new("Frame")

-- Propriedades principais
ScreenGui.Name = "EmilliHub"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- Tela de Boas-Vindas
WelcomeFrame.Name = "WelcomeFrame"
WelcomeFrame.Parent = ScreenGui
WelcomeFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
WelcomeFrame.BorderSizePixel = 0
WelcomeFrame.Size = UDim2.new(0, 400, 0, 150)
WelcomeFrame.Position = UDim2.new(0.5, -200, 0.5, -75)
WelcomeFrame.AnchorPoint = Vector2.new(0.5, 0.5)

WelcomeLabel.Name = "WelcomeLabel"
WelcomeLabel.Parent = WelcomeFrame
WelcomeLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
WelcomeLabel.BorderSizePixel = 0
WelcomeLabel.Size = UDim2.new(1, 0, 1, 0)
WelcomeLabel.Font = Enum.Font.GothamBold
WelcomeLabel.Text = "Bem-vindo ao Emilli Hub"
WelcomeLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
WelcomeLabel.TextSize = 24

-- Interface Principal (MainFrame)
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.BorderSizePixel = 0
MainFrame.Position = UDim2.new(0.5, -250, 0.5, -200)
MainFrame.Size = UDim2.new(0, 500, 0, 400)
MainFrame.Visible = false
MainFrame.ClipsDescendants = true

-- Botões de Fechar e Minimizar
CloseButton.Name = "CloseButton"
CloseButton.Parent = MainFrame
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 0, 5)
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.TextSize = 20

MinimizeButton.Name = "MinimizeButton"
MinimizeButton.Parent = MainFrame
MinimizeButton.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -70, 0, 5)
MinimizeButton.Text = "_"
MinimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeButton.TextSize = 20

-- Frame de Abas (Lateral)
TabsFrame.Name = "TabsFrame"
TabsFrame.Parent = MainFrame
TabsFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
TabsFrame.BorderSizePixel = 0
TabsFrame.Position = UDim2.new(0, 0, 0, 40)
TabsFrame.Size = UDim2.new(0, 60, 1, -40)

-- Frame de Conteúdo
ContentFrame.Name = "ContentFrame"
ContentFrame.Parent = MainFrame
ContentFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
ContentFrame.BorderSizePixel = 0
ContentFrame.Position = UDim2.new(0, 60, 0, 40)
ContentFrame.Size = UDim2.new(1, -60, 1, -40)

-- Função de Boas-vindas (Fade In / Fade Out)
WelcomeFrame.BackgroundTransparency = 1
WelcomeLabel.TextTransparency = 1

game:GetService("TweenService"):Create(WelcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 0}):Play()
game:GetService("TweenService"):Create(WelcomeLabel, TweenInfo.new(1), {TextTransparency = 0}):Play()

wait(2)

game:GetService("TweenService"):Create(WelcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 1}):Play()
game:GetService("TweenService"):Create(WelcomeLabel, TweenInfo.new(1), {TextTransparency = 1}):Play()

wait(1)

WelcomeFrame.Visible = false
MainFrame.Visible = true

-- Botões
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

local minimized = false
MinimizeButton.MouseButton1Click:Connect(function()
    minimized = not minimized
    if minimized then
        ContentFrame.Visible = false
    else
        ContentFrame.Visible = true
    end
end)-- Criando as abas laterais
local tabs = {
    {Name = "Troll", Icon = "rbxassetid://12345678"},
    {Name = "Movimentação", Icon = "rbxassetid://12345679"},
    {Name = "Visual", Icon = "rbxassetid://12345680"},
    {Name = "Admin", Icon = "rbxassetid://12345681"},
    {Name = "Música", Icon = "rbxassetid://12345682"},
    {Name = "Config", Icon = "rbxassetid://12345683"},
}

local TabsButtons = {}
local SelectedTab

for i, tabData in ipairs(tabs) do
    local button = Instance.new("TextButton")
    button.Name = tabData.Name.."Tab"
    button.Parent = TabsFrame
    button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    button.BorderSizePixel = 0
    button.Position = UDim2.new(0, 0, 0, (i-1) * 60)
    button.Size = UDim2.new(1, 0, 0, 60)
    button.Text = tabData.Name
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 14
    button.Font = Enum.Font.GothamBold
    button.MouseButton1Click:Connect(function()
        if SelectedTab then
            SelectedTab.Visible = false
        end
        if ContentFrame:FindFirstChild(tabData.Name.."Page") then
            ContentFrame:FindFirstChild(tabData.Name.."Page").Visible = true
            SelectedTab = ContentFrame:FindFirstChild(tabData.Name.."Page")
        end
    end)
    TabsButtons[tabData.Name] = button
end

-- Criar as páginas de conteúdo para cada aba
local Pages = {}

for _, tabData in ipairs(tabs) do
    local page = Instance.new("Frame")
    page.Name = tabData.Name.."Page"
    page.Parent = ContentFrame
    page.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    page.BorderSizePixel = 0
    page.Size = UDim2.new(1, 0, 1, 0)
    page.Visible = false

    Pages[tabData.Name] = page

    local label = Instance.new("TextLabel")
    label.Parent = page
    label.Size = UDim2.new(1, 0, 0, 30)
    label.BackgroundTransparency = 1
    label.Font = Enum.Font.GothamBold
    label.TextSize = 18
    label.Text = tabData.Name
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
end

-- Abrir primeira aba por padrão
Pages["Troll"].Visible = true
SelectedTab = Pages["Troll"]
