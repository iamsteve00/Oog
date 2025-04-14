-- Espera o jogo carregar
if not game:IsLoaded() then game.Loaded:Wait() end

local CoreGui = game:GetService("CoreGui")

-- Remove GUI antiga se já existir
if CoreGui:FindFirstChild("EmilliHub") then
    CoreGui.EmilliHub:Destroy()
end

-- Criação da ScreenGui
local gui = Instance.new("ScreenGui")
gui.Name = "EmilliHub"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = CoreGui

-- Frame principal com estilo Chaos
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 400)
frame.Position = UDim2.new(0.5, -150, 0.5, -200)
frame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
frame.BorderSizePixel = 0
frame.Parent = gui

-- UICorner para bordas arredondadas
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = frame

-- Sombras simuladas (opcional)
local shadow = Instance.new("ImageLabel")
shadow.Size = UDim2.new(1, 30, 1, 30)
shadow.Position = UDim2.new(0, -15, 0, -15)
shadow.BackgroundTransparency = 1
shadow.Image = "rbxassetid://1316045217" -- sombra padrão
shadow.ImageTransparency = 0.6
shadow.ZIndex = 0
shadow.Parent = frame

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
title.Text = "Emilli Hub"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.GothamBlack
title.TextSize = 20
title.Parent = frame

local titleCorner = Instance.new("UICorner")
titleCorner.CornerRadius = UDim.new(0, 12)
titleCorner.Parent = title

-- Função para criar botões com estilo
local function createButton(text, yPos, callback)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(1, -20, 0, 40)
	button.Position = UDim2.new(0, 10, 0, yPos)
	button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Font = Enum.Font.Gotham
	button.TextSize = 16
	button.Text = text
	button.ZIndex = 2
	button.Parent = frame

	local btnCorner = Instance.new("UICorner")
	btnCorner.CornerRadius = UDim.new(0, 8)
	btnCorner.Parent = button

	button.MouseButton1Click:Connect(callback)
end

-- Botões (exemplo)
createButton("Fly GUI", 60, function()
	print("Fly ativado")
end)

createButton("Kill Player", 110, function()
	print("Kill ativado")
end)

createButton("Speed", 160, function()
	print("Speed ativado")
end)

createButton("Teleport", 210, function()
	print("Teleport ativado")
end)

createButton("Fechar", 260, function()
	gui:Destroy()
end)
