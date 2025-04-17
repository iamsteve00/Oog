local Players = game:GetService("Players")
local player = Players.LocalPlayer
local TweenService = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")

-- Cria a tela
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "EmilliHub"
screenGui.ResetOnSpawn = false

-- Container principal com cantos arredondados
local main = Instance.new("Frame", screenGui)
main.Name = "Main"
main.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
main.BorderSizePixel = 0
main.Position = UDim2.new(0.25, 0, 0.2, 0)
main.Size = UDim2.new(0, 500, 0, 350)
main.Visible = false

local UICorner = Instance.new("UICorner", main)
UICorner.CornerRadius = UDim.new(0, 8)

-- Aba lateral com ícones
local sidebar = Instance.new("Frame", main)
sidebar.Size = UDim2.new(0, 50, 1, 0)
sidebar.Position = UDim2.new(0, 0, 0, 0)
sidebar.BackgroundColor3 = Color3.fromRGB(10, 10, 10)

local UIListLayout = Instance.new("UIListLayout", sidebar)
UIListLayout.Padding = UDim.new(0, 5)
UIListLayout.FillDirection = Enum.FillDirection.Vertical

-- Definição das abas e ícones
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

-- Área de conteúdo com cantos arredondados
local content = Instance.new("Frame", main)
content.Size = UDim2.new(1, -50, 1, 0)
content.Position = UDim2.new(0, 50, 0, 0)
content.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

local UICornerContent = Instance.new("UICorner", content)
UICornerContent.CornerRadius = UDim.new(0, 8)

-- Criar botões de navegação
for i, tab in ipairs(Tabs) do
	local Button = Instance.new("ImageButton", sidebar)
	Button.Name = tab.Name .. "Tab"
	Button.Size = UDim2.new(1, 0, 0, 40)
	Button.BackgroundTransparency = 1
	Button.Image = tab.Icon
	Button.ImageColor3 = Color3.fromRGB(200, 200, 200)

	-- Animação ao passar o mouse
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

-- Mostrar a primeira aba por padrão
TabButtons[1].MouseButton1Click:Fire()

-- Animação de Fade-In para a interface
TweenService:Create(main, TweenInfo.new(1), {Visible = true}):Play()
