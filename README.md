-- Espera o jogo carregar
if not game:IsLoaded() then
    game.Loaded:Wait()
end

-- Referências
local CoreGui = game:GetService("CoreGui")

-- Remove GUI anterior se já existir
if CoreGui:FindFirstChild("EmilliHub") then
    CoreGui.EmilliHub:Destroy()
end

-- Cria GUI principal
local gui = Instance.new("ScreenGui")
gui.Name = "EmilliHub"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = CoreGui  -- USANDO CoreGui PARA DRIBLAR BLOQUEIO

-- Frame principal
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 400)
frame.Position = UDim2.new(0.5, -150, 0.5, -200)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
frame.BorderSizePixel = 0
frame.Parent = gui

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
title.Text = "Emilli Hub"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.GothamBold
title.TextSize = 20
title.Parent = frame

-- Função para criar botões
local function createButton(text, yPos, callback)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(1, -20, 0, 40)
	button.Position = UDim2.new(0, 10, 0, yPos)
	button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Font = Enum.Font.Gotham
	button.TextSize = 16
	button.Text = text
	button.Parent = frame
	button.MouseButton1Click:Connect(callback)
end

-- Botões de exemplo (testes)
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
