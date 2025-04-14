
-- Creating the main interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)

-- Close and minimize buttons
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 1, -35)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Parent = Frame
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -70, 1, -35)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)

-- Minimize function and make the frame draggable
local minimized = false

MinimizeButton.MouseButton1Click:Connect(function()
    if minimized then
        Frame.Size = UDim2.new(0, 300, 0, 200)
        Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
    else
        Frame.Size = UDim2.new(0, 50, 0, 50)
        Frame.Position = UDim2.new(0.5, -25, 0.5, -25)
    end
    minimized = not minimized
end)

local UserInputService = game:GetService("UserInputService")

local dragging = false
local dragInput
local dragStart
local startPos

Frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = Frame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

Frame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        Frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

-- Creating tabs
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

-- Adding flight option
local FlyButton = Instance.new("TextButton")
FlyButton.Parent = OthersFrame
FlyButton.Text = "Enable/Disable Flight"
FlyButton.Size = UDim2.new(0, 150, 0, 30)
FlyButton.Position = UDim2.new(0, 10, 0, 50)
FlyButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)

local SpeedBox = Instance.new("TextBox")
SpeedBox.Parent = OthersFrame
SpeedBox.Text = "Speed: 50"
SpeedBox.Size = UDim2.new(0, 150, 0, 30)
SpeedBox.Position = UDim2.new(0, 10, 0, 90)
SpeedBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)

local flying = false
local speed = 50
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")

FlyButton.MouseButton1Click:Connect(function()
    flying = not flying

    if flying then
        local bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.Velocity = Vector3.new(0, speed, 0)
        bodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
        bodyVelocity.Parent = humanoidRootPart
    else
        for _, obj in pairs(humanoidRootPart:GetChildren()) do
            if obj:IsA("BodyVelocity") then
                obj:Destroy()
            end
        end
    end
end)

SpeedBox.FocusLost:Connect(function()
    local newSpeed = tonumber(SpeedBox.Text:match("%d+"))
    if newSpeed then
        speed = newSpeed
    end
end)
