
-- Creating the Main Interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193) -- Theme color
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)

-- Function to display a global message
local function broadcastMessage(messageText, duration)
    for _, player in ipairs(game.Players:GetPlayers()) do
        local playerGui = player:FindFirstChildOfClass("PlayerGui")
        if playerGui then
            local messageLabel = Instance.new("TextLabel")
            messageLabel.Parent = playerGui
            messageLabel.Text = messageText
            messageLabel.Size = UDim2.new(0, 400, 0, 50)
            messageLabel.Position = UDim2.new(0.5, -200, 0.05, 0)
            messageLabel.BackgroundTransparency = 0.5
            messageLabel.TextScaled = true
            messageLabel.TextColor3 = Color3.fromRGB(255, 0, 0)

            task.delay(duration, function()
                messageLabel:Destroy()
            end)
        end
    end
end

broadcastMessage("🚀 Slime X Emili", 5)

-- Creating Tabs
local function createTabButton(name, text, position)
    local tabButton = Instance.new("TextButton")
    tabButton.Name = name
    tabButton.Parent = Frame
    tabButton.Text = text
    tabButton.Size = UDim2.new(0, 80, 0, 30)
    tabButton.Position = position
    return tabButton
end

local TrollTab = createTabButton("TrollTab", "Troll", UDim2.new(0, 10, 0, 10))
local PlayerTab = createTabButton("PlayerTab", "Player", UDim2.new(0, 100, 0, 10))
local OthersTab = createTabButton("OthersTab", "Others", UDim2.new(0, 190, 0, 10))

-- Creating Tab Frames
local function createTabFrame()
    local tabFrame = Instance.new("Frame")
    tabFrame.Parent = ScreenGui
    tabFrame.Size = UDim2.new(0, 300, 0, 250)
    tabFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
    tabFrame.Visible = false
    return tabFrame
end

local TrollFrame = createTabFrame()
local OthersFrame = createTabFrame()
local PlayerFrame = createTabFrame()

-- Showing Tabs when clicked
TrollTab.MouseButton1Click:Connect(function()
    Frame.Visible = false
    TrollFrame.Visible = true
end)

OthersTab.MouseButton1Click:Connect(function()
    Frame.Visible = false
    OthersFrame.Visible = true
end)

PlayerTab.MouseButton1Click:Connect(function()
    Frame.Visible = false
    PlayerFrame.Visible = true
end)

-- Fly Option in Others Tab
local FlyButton = Instance.new("TextButton")
FlyButton.Parent = OthersFrame
FlyButton.Text = "Fly (Toggle)"
FlyButton.Size = UDim2.new(0, 150, 0, 40)
FlyButton.Position = UDim2.new(0.5, -75, 0.7, 0)

local isFlying = false
local flySpeed = 50

local function toggleFly(player)
    if not player or not player.Character or not player.Character:FindFirstChild("HumanoidRootPart") then return end
    local humanoidRootPart = player.Character.HumanoidRootPart

    if isFlying then
        isFlying = false
    else
        isFlying = true
        game:GetService("RunService").Heartbeat:Connect(function()
            humanoidRootPart.Velocity = Vector3.new(0, flySpeed, 0)
        end)
    end
end

FlyButton.MouseButton1Click:Connect(function()
    toggleFly(game.Players.LocalPlayer)
end)

-- Teleport Option in Player Tab
local TeleportButton = Instance.new("TextButton")
TeleportButton.Parent = PlayerFrame
TeleportButton.Text = "Teleport"
TeleportButton.Size = UDim2.new(0, 150, 0, 40)
TeleportButton.Position = UDim2.new(0.5, -75, 0.2, 0)

TeleportButton.MouseButton1Click:Connect(function()
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        character.HumanoidRootPart.CFrame = CFrame.new(0, 10, 0)
    end
end)

-- Change Speed in Player Tab
local SpeedButton = Instance.new("TextButton")
SpeedButton.Parent = PlayerFrame
SpeedButton.Text = "Change Speed"
SpeedButton.Size = UDim2.new(0, 150, 0, 40)
SpeedButton.Position = UDim2.new(0.5, -75, 0.35, 0)

SpeedButton.MouseButton1Click:Connect(function()
    local humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
    if humanoid then
        humanoid.WalkSpeed = math.clamp(humanoid.WalkSpeed + 10, 10, 100) -- Limits between 10 and 100
    end
end)

-- Change Jump Power in Player Tab
local JumpButton = Instance.new("TextButton")
JumpButton.Parent = PlayerFrame
JumpButton.Text = "Change Jump"
JumpButton.Size = UDim2.new(0, 150, 0, 40)
JumpButton.Position = UDim2.new(0.5, -75, 0.5, 0)

JumpButton.MouseButton1Click:Connect(function()
    local humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
    if humanoid then
        humanoid.JumpPower = math.clamp(humanoid.JumpPower + 10, 10, 200) -- Limits between 10 and 200
    end
end)# Oog
