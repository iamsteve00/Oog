-- Emilli Hub | Parte 1: Interface, Boas-Vindas, Abas

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local TweenService = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")

-- Cria a tela
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "EmilliHub"
screenGui.ResetOnSpawn = false

-- Mensagem de boas-vindas
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

-- Fade in
TweenService:Create(welcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 0.2}):Play()
TweenService:Create(welcomeText, TweenInfo.new(1), {TextTransparency = 0}):Play()
task.wait(2)

-- Fade out
TweenService:Create(welcomeFrame, TweenInfo.new(1), {BackgroundTransparency = 1}):Play()
TweenService:Create(welcomeText, TweenInfo.new(1), {TextTransparency = 1}):Play()
task.wait(1)

welcomeFrame:Destroy()

-- Container principal
local main = Instance.new("Frame", screenGui)
main.Name = "Main"
main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
main.BorderSizePixel = 0
main.Position = UDim2.new(0.25, 0, 0.2, 0)
main.Size = UDim2.new(0, 500, 0, 350)
main.Visible = false

-- Fade in da interface principal
TweenService:Create(main, TweenInfo.new(1), {Visible = true}):Play()

-- Aba lateral (ícones)
local sidebar = Instance.new("Frame", main)
sidebar.Size = UDim2.new(0, 50, 1, 0)
sidebar.Position = UDim2.new(0, 0, 0, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(15, 15, 15)

local iconNames = {"Troll", "Move", "Visual", "Admin", "Music", "Config"}
local iconRefs = {}

for i, name in ipairs(iconNames) do
	local button = Instance.new("TextButton", sidebar)
	button.Name = name.."Tab"
	button.Size = UDim2.new(1, 0, 0, 50)
	button.Position = UDim2.new(0, 0, 0, (i - 1) * 50)
	button.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
	button.Text = name
	button.TextColor3 = Color3.new(1,1,1)
	button.TextScaled = true
	iconRefs[name] = button
end

-- Conteúdo das abas
local pages = {}

for _, name in pairs(iconNames) do
	local page = Instance.new("ScrollingFrame", main)
	page.Name = name.."Page"
	page.Size = UDim2.new(1, -50, 1, 0)
	page.Position = UDim2.new(0, 50, 0, 0)
	page.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	page.Visible = false
	page.BorderSizePixel = 0
	page.CanvasSize = UDim2.new(0, 0, 2, 0)
	pages[name] = page
end

-- Alternância de abas
for name, button in pairs(iconRefs) do
	button.MouseButton1Click:Connect(function()
		for _, page in pairs(pages) do page.Visible = false end
		pages[name].Visible = true
	end)
end

-- Mostra a primeira aba por padrão
pages["Troll"].Visible = true-- ABA LATERAL COM ÍCONES E NAVEGAÇÃO ENTRE AS ABAS

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

for i, tab in ipairs(Tabs) do
	local Button = Instance.new("ImageButton")
	Button.Name = tab.Name .. "Tab"
	Button.Size = UDim2.new(1, 0, 0, 40)
	Button.BackgroundTransparency = 1
	Button.Image = tab.Icon
	Button.ImageColor3 = Color3.fromRGB(255, 255, 255)
	Button.Parent = Sidebar
	Button.Position = UDim2.new(0, 0, 0, (i - 1) * 45)
	Button.MouseEnter:Connect(function()
		Button.ImageColor3 = Color3.fromRGB(255, 0, 0)
	end)
	Button.MouseLeave:Connect(function()
		if SelectedTab ~= Button then
			Button.ImageColor3 = Color3.fromRGB(255, 255, 255)
		end
	end)
	Button.MouseButton1Click:Connect(function()
		for _, content in ipairs(Content:GetChildren()) do
			if content:IsA("Frame") then
				content.Visible = false
			end
		end
		for _, otherButton in ipairs(TabButtons) do
			otherButton.ImageColor3 = Color3.fromRGB(255, 255, 255)
		end
		local TargetTab = Content:FindFirstChild(tab.Name)
		if TargetTab then
			TargetTab.Visible = true
		end
		Button.ImageColor3 = Color3.fromRGB(255, 0, 0)
		SelectedTab = Button
	end)
	table.insert(TabButtons, Button)
end

-- CRIAR AS ABA CONTAINERS NO CONTENT
for _, tab in ipairs(Tabs) do
	local TabFrame = Instance.new("Frame")
	TabFrame.Name = tab.Name
	TabFrame.Size = UDim2.new(1, 0, 1, 0)
	TabFrame.BackgroundTransparency = 1
	TabFrame.Visible = false
	TabFrame.Parent = Content

	local UIListLayout = Instance.new("UIListLayout", TabFrame)
	UIListLayout.Padding = UDim.new(0, 5)
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
end

-- SELECIONA A PRIMEIRA ABA COMO PADRÃO
TabButtons[1].MouseButton1Click:Fire()
