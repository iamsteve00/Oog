-- Emilli Hub | Estilo Chaos Hub com funcionalidades completas

local EmilliHub = Instance.new("ScreenGui")
local Main = Instance.new("Frame")
local TopBar = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local Minimize = Instance.new("TextButton")
local Close = Instance.new("TextButton")
local Sidebar = Instance.new("Frame")
local Content = Instance.new("Frame")
local TrollTab = Instance.new("Frame")
local KillInput = Instance.new("TextBox")
local KillButton = Instance.new("TextButton")
local MinimizedIcon = Instance.new("TextButton")

-- Propriedades básicas
EmilliHub.Name = "EmilliHub"
EmilliHub.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
EmilliHub.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
EmilliHub.ResetOnSpawn = false

-- Interface principal
Main.Name = "Main"
Main.Parent = EmilliHub
Main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Main.Position = UDim2.new(0.3, 0, 0.2, 0)
Main.Size = UDim2.new(0, 750, 0, 420)
Main.BorderSizePixel = 0

-- Topo
TopBar.Name = "TopBar"
TopBar.Parent = Main
TopBar.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
TopBar.Size = UDim2.new(1, 0, 0, 30)

Title.Name = "Title"
Title.Parent = TopBar
Title.Text = "Brookhaven RP | Português"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0.03, 0, 0, 0)
Title.Size = UDim2.new(0.9, 0, 1, 0)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 16
Title.TextXAlignment = Enum.TextXAlignment.Left

Minimize.Name = "Minimize"
Minimize.Parent = TopBar
Minimize.Size = UDim2.new(0, 30, 0, 30)
Minimize.Position = UDim2.new(1, -60, 0, 0)
Minimize.Text = "_"
Minimize.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Minimize.TextColor3 = Color3.fromRGB(255, 255, 255)

Close.Name = "Close"
Close.Parent = TopBar
Close.Size = UDim2.new(0, 30, 0, 30)
Close.Position = UDim2.new(1, -30, 0, 0)
Close.Text = "X"
Close.BackgroundColor3 = Color3.fromRGB(120, 0, 0)
Close.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Sidebar lateral
Sidebar.Name = "Sidebar"
Sidebar.Parent = Main
Sidebar.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Sidebar.Position = UDim2.new(0, 0, 0, 30)
Sidebar.Size = UDim2.new(0, 60, 1, -30)

-- Conteúdo principal
Content.Name = "Content"
Content.Parent = Main
Content.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Content.Position = UDim2.new(0, 60, 0, 30)
Content.Size = UDim2.new(1, -60, 1, -30)

-- Aba Troll
TrollTab.Name = "TrollTab"
TrollTab.Parent = Content
TrollTab.Size = UDim2.new(1, 0, 1, 0)
TrollTab.BackgroundTransparency = 1

KillInput.Name = "KillInput"
KillInput.Parent = TrollTab
KillInput.PlaceholderText = "Nome do Player"
KillInput.Size = UDim2.new(0, 200, 0, 40)
KillInput.Position = UDim2.new(0, 20, 0, 20)
KillInput.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
KillInput.TextColor3 = Color3.fromRGB(255, 255, 255)
KillInput.Text = ""
KillInput.Font = Enum.Font.Gotham
KillInput.TextSize = 14

KillButton.Name = "KillButton"
KillButton.Parent = TrollTab
KillButton.Size = UDim2.new(0, 200, 0, 40)
KillButton.Position = UDim2.new(0, 20, 0, 70)
KillButton.Text = "Kill Player"
KillButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
KillButton.TextColor3 = Color3.fromRGB(255, 255, 255)
KillButton.Font = Enum.Font.GothamBold
KillButton.TextSize = 14

KillButton.MouseButton1Click:Connect(function()
	local targetName = KillInput.Text
	local event = game.ReplicatedStorage:FindFirstChild("KillPlayerEvent")
	if event and targetName ~= "" then
		event:FireServer(targetName)
	end
end)

-- Minimizado
MinimizedIcon.Name = "MinimizedIcon"
MinimizedIcon.Parent = EmilliHub
MinimizedIcon.Text = "E"
MinimizedIcon.Position = UDim2.new(0.4, 0, 0.05, 0)
MinimizedIcon.Size = UDim2.new(0, 50, 0, 50)
MinimizedIcon.Visible = false
MinimizedIcon.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
MinimizedIcon.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizedIcon.Draggable = true
MinimizedIcon.Active = true

-- Funcionalidade de minimizar
Minimize.MouseButton1Click:Connect(function()
	Main.Visible = false
	MinimizedIcon.Visible = true
end)

MinimizedIcon.MouseButton1Click:Connect(function()
	Main.Visible = true
	MinimizedIcon.Visible = false
end)

-- Fechar
Close.MouseButton1Click:Connect(function()
	EmilliHub:Destroy()
end)
