-- Open-source script for Roblox
-- Compatible with Krnl executor

-- Creating the main interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193) -- Theme color
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)

-- Close and Minimize buttons (Now at the bottom right)
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 1, -35) -- Moved to the bottom right
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Parent = Frame
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -70, 1, -35) -- Moved to the bottom right
MinimizeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)

MinimizeButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)

-- Creating tab buttons
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

-- Creating tab frames
local function createTabFrame()
    local tabFrame = Instance.new("Frame")
    tabFrame.Parent = ScreenGui
    tabFrame.Size = UDim2.new(0, 300, 0, 250)
    tabFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
    tabFrame.Visible = false
    return tabFrame
end

local TrollFrame = createTabFrame()
local PlayerFrame = createTabFrame()
local OthersFrame = createTabFrame()

-- Back buttons
local function createBackButton(tabFrame)
    local BackButton = Instance.new("TextButton")
    BackButton.Parent = tabFrame
    BackButton.Text = "Back"
    BackButton.Size = UDim2.new(0, 80, 0, 30)
    BackButton.Position = UDim2.new(0, 10, 0, 10)
    BackButton.BackgroundColor3 = Color3.fromRGB(150, 150, 150)

    BackButton.MouseButton1Click:Connect(function()
        tabFrame.Visible = false
        Frame.Visible = true
    end)
end

createBackButton(TrollFrame)
createBackButton(PlayerFrame)
createBackButton(OthersFrame)

-- Show tabs when clicked
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

-- Adding player selection field and actions in the Troll tab
local PlayerNameBox = Instance.new("TextBox")
PlayerNameBox.Parent = TrollFrame
PlayerNameBox.PlaceholderText = "Enter player's name"
PlayerNameBox.Size = UDim2.new(0, 200, 0, 30)
PlayerNameBox.Position = UDim2.new(0.5, -100, 0.2, 0)
PlayerNameBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
PlayerNameBox.TextColor3 = Color3.fromRGB(0, 0, 0)

-- Void Player button with advanced checking
local VoidButton = Instance.new("TextButton")
VoidButton.Parent = TrollFrame
VoidButton.Text = "Void Player"
VoidButton.Size = UDim2.new(0, 150, 0, 40)
VoidButton.Position = UDim2.new(0.5, -75, 0.35, 0)
VoidButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

VoidButton.MouseButton1Click:Connect(function()
    local playerName = PlayerNameBox.Text
    if playerName == "" then return end -- Prevents execution with empty input

    local targetPlayer = game.Players:FindFirstChild(playerName)

    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        targetPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, -500, 0) -- Teleport to Void
    else
        print("Player not found or missing HumanoidRootPart.")
    end
end)

-- View Player button with advanced checking
local ViewButton = Instance.new("TextButton")
ViewButton.Parent = TrollFrame
ViewButton.Text = "View Player"
ViewButton.Size = UDim2.new(0, 150, 0, 40)
ViewButton.Position = UDim2.new(0.5, -75, 0.5, 0)
ViewButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)

ViewButton.MouseButton1Click:Connect(function()
    local playerName = PlayerNameBox.Text
    if playerName == "" then return end -- Prevents execution with empty input

    local targetPlayer = game.Players:FindFirstChild(playerName)

    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("Humanoid") then
        game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character.Humanoid -- Adjusts camera to follow the player
    else
        print("Player not found or missing Humanoid.")
    end
end)
