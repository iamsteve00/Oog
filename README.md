- Tela de Boas-Vindas

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "EmilliWelcome"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local WelcomeFrame = Instance.new("Frame")
WelcomeFrame.Size = UDim2.new(0, 400, 0, 100)
WelcomeFrame.Position = UDim2.new(0.5, -200, 0.5, -50)
WelcomeFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
WelcomeFrame.BackgroundTransparency = 0.5
WelcomeFrame.BorderSizePixel = 0
WelcomeFrame.Visible = true
WelcomeFrame.Parent = ScreenGui

local WelcomeText = Instance.new("TextLabel")
WelcomeText.Size = UDim2.new(1, 0, 1, 0)
WelcomeText.BackgroundTransparency = 1
WelcomeText.Text = "Bem-vindo ao Emilli Hub"
WelcomeText.TextColor3 = Color3.fromRGB(255, 0, 0)
WelcomeText.TextStrokeTransparency = 0
WelcomeText.Font = Enum.Font.GothamBold
WelcomeText.TextScaled = true
WelcomeText.Parent = WelcomeFrame

-- Fade In
for i = 1, 0, -0.1 do
	task.wait(0.05)
	WelcomeFrame.BackgroundTransparency = i
	WelcomeText.TextTransparency = i
end

task.wait(2)

-- Fade Out
for i = 0, 1, 0.1 do
	task.wait(0.05)
	WelcomeFrame.BackgroundTransparency = i
	WelcomeText.TextTransparency = i
end

WelcomeFrame:Destroy()-- Emilli Hub 

--Interface Principal e Sistema de Abas

local Players = game:GetService("Players") local LocalPlayer = Players.LocalPlayer local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- Interface Principal local ScreenGui = Instance.new("ScreenGui") ScreenGui.Name = "EmilliHubGUI" ScreenGui.ResetOnSpawn = false ScreenGui.Parent = PlayerGui

-- Fundo Principal local MainFrame = Instance.new("Frame") MainFrame.Name = "MainFrame" MainFrame.Size = UDim2.new(0, 600, 0, 400) MainFrame.Position = UDim2.new(0.5, -300, 0.5, -200) MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20) MainFrame.BorderSizePixel = 0 MainFrame.Visible = false MainFrame.Parent = ScreenGui

-- Cantos arredondados local UICorner = Instance.new("UICorner") UICorner.CornerRadius = UDim.new(0, 12) UICorner.Parent = MainFrame

-- Título local Title = Instance.new("TextLabel") Title.Text = "Brookhaven RP | Português" Title.Font = Enum.Font.GothamBold Title.TextColor3 = Color3.fromRGB(255, 255, 255) Title.TextSize = 22 Title.BackgroundTransparency = 1 Title.Position = UDim2.new(0, 60, 0, 10) Title.Size = UDim2.new(1, -70, 0, 30) Title.TextXAlignment = Enum.TextXAlignment.Left Title.Parent = MainFrame

-- Botão Fechar local CloseButton = Instance.new("TextButton") CloseButton.Text = "X" CloseButton.Font = Enum.Font.GothamBold CloseButton.TextColor3 = Color3.fromRGB(255, 0, 0) CloseButton.TextSize = 18 CloseButton.Size = UDim2.new(0, 30, 0, 30) CloseButton.Position = UDim2.new(1, -35, 0, 5) CloseButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30) CloseButton.BorderSizePixel = 0 CloseButton.Parent = MainFrame CloseButton.MouseButton1Click:Connect(function() MainFrame.Visible = false end)

-- Botão Minimizar local MinimizeButton = Instance.new("TextButton") MinimizeButton.Text = "_" MinimizeButton.Font = Enum.Font.GothamBold MinimizeButton.TextColor3 = Color3.fromRGB(200, 200, 200) MinimizeButton.TextSize = 18 MinimizeButton.Size = UDim2.new(0, 30, 0, 30) MinimizeButton.Position = UDim2.new(1, -70, 0, 5) MinimizeButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30) MinimizeButton.BorderSizePixel = 0 MinimizeButton.Parent = MainFrame

-- Sistema de Minimizar local ContentVisible = true MinimizeButton.MouseButton1Click:Connect(function() ContentVisible = not ContentVisible for _, child in ipairs(MainFrame:GetChildren()) do if child:IsA("Frame") or child:IsA("ScrollingFrame") then child.Visible = ContentVisible end end end)

-- Painel de abas local SideBar = Instance.new("Frame") SideBar.Name = "SideBar" SideBar.Size = UDim2.new(0, 50, 1, -50) SideBar.Position = UDim2.new(0, 0, 0, 50) SideBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25) SideBar.BorderSizePixel = 0 SideBar.Parent = MainFrame

local Tabs = { {"Troll", "rbxassetid://1234561"}, {"Movimentação", "rbxassetid://1234562"}, {"Visual", "rbxassetid://1234563"}, {"Admin", "rbxassetid://1234564"}, {"Música", "rbxassetid://1234565"}, {"Config", "rbxassetid://1234566"}, }

local TabFrames = {}

for i, tab in ipairs(Tabs) do local tabName, iconId = tab[1], tab[2]

-- Botão da aba
local Button = Instance.new("ImageButton")
Button.Name = tabName .. "Button"
Button.Size = UDim2.new(1, 0, 0, 50)
Button.Position = UDim2.new(0, 0, 0, (i - 1) * 50)
Button.Image = iconId
Button.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Button.BorderSizePixel = 0
Button.Parent = SideBar

-- Frame da aba
local Frame = Instance.new("ScrollingFrame")
Frame.Name = tabName .. "Frame"
Frame.Size = UDim2.new(1, -60, 1, -60)
Frame.Position = UDim2.new(0, 60, 0, 50)
Frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Frame.Visible = false
Frame.BorderSizePixel = 0
Frame.CanvasSize = UDim2.new(0, 0, 0, 1000)
Frame.ScrollBarThickness = 6
Frame.Parent = MainFrame

TabFrames[tabName] = Frame

Button.MouseButton1Click:Connect(function()
	for name, tabFrame in pairs(TabFrames) do
		tabFrame.Visible = (name == tabName)
	end
end)

end

-- Exibir a primeira aba TabFrames["Troll"].Visible = true MainFrame.Visible = true

--- Abas Laterais com Ícones

local TabsFrame = Instance.new("Frame")
TabsFrame.Name = "TabsFrame"
TabsFrame.Size = UDim2.new(0, 60, 1, -30)
TabsFrame.Position = UDim2.new(0, 0, 0, 30)
TabsFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
TabsFrame.BorderSizePixel = 0
TabsFrame.Parent = MainFrame

local TabNames = {
	{ Name = "Troll", Icon = "rbxassetid://6031091002" },
	{ Name = "Movimentação", Icon = "rbxassetid://6031071050" },
	{ Name = "Visual", Icon = "rbxassetid://6031094678" },
	{ Name = "Admin", Icon = "rbxassetid://6031071053" },
	{ Name = "Música", Icon = "rbxassetid://6031077301" },
	{ Name = "Config", Icon = "rbxassetid://6031082533" },
}

local Tabs = {}
local CurrentTab

for i, tab in ipairs(TabNames) do
	local Button = Instance.new("ImageButton")
	Button.Name = tab.Name .. "Tab"
	Button.Size = UDim2.new(1, 0, 0, 50)
	Button.Position = UDim2.new(0, 0, 0, (i - 1) * 52)
	Button.BackgroundTransparency = 1
	Button.Image = tab.Icon
	Button.Parent = TabsFrame

	local Tooltip = Instance.new("TextLabel")
	Tooltip.Name = "Tooltip"
	Tooltip.Size = UDim2.new(0, 100, 0, 20)
	Tooltip.Position = UDim2.new(1, 5, 0.5, -10)
	Tooltip.BackgroundTransparency = 0.3
	Tooltip.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	Tooltip.Text = tab.Name
	Tooltip.TextColor3 = Color3.fromRGB(255, 255, 255)
	Tooltip.TextScaled = true
	Tooltip.Visible = false
	Tooltip.Parent = Button

	Button.MouseEnter:Connect(function()
		Tooltip.Visible = true
	end)

	Button.MouseLeave:Connect(function()
		Tooltip.Visible = false
	end)

	Tabs[tab.Name] = Button
end

--Conteúdo das Abas

local ContentFrame = Instance.new("Frame")
ContentFrame.Name = "ContentFrame"
ContentFrame.Size = UDim2.new(1, -60, 1, -30)
ContentFrame.Position = UDim2.new(0, 60, 0, 30)
ContentFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
ContentFrame.BorderSizePixel = 0
ContentFrame.Parent = MainFrame

local Pages = {}

for _, tab in ipairs(TabNames) do
	local Page = Instance.new("ScrollingFrame")
	Page.Name = tab.Name .. "Page"
	Page.Size = UDim2.new(1, 0, 1, 0)
	Page.CanvasSize = UDim2.new(0, 0, 0, 0)
	Page.ScrollBarThickness = 6
	Page.Visible = false
	Page.BackgroundTransparency = 1
	Page.BorderSizePixel = 0
	Page.Parent = ContentFrame

	local Layout = Instance.new("UIListLayout")
	Layout.Padding = UDim.new(0, 6)
	Layout.SortOrder = Enum.SortOrder.LayoutOrder
	Layout.Parent = Page

	Pages[tab.Name] = Page
end

local function ShowTab(tabName)
	for name, page in pairs(Pages) do
		page.Visible = (name == tabName)
	end
	CurrentTab = tabName
end

for name, button in pairs(Tabs) do
	button.MouseButton1Click:Connect(function()
		ShowTab(name)
	end)
end

-- Exibe a aba Troll por padrão ao iniciar
ShowTab("Troll")
