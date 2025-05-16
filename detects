local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer

-- List of target usernames to detect (replace with actual usernames)
local TARGET_USERS = {
	"AlphaByteDev",
	"ArtemisSnipe",
	"leporus",
	"Black_ink10",
	"HoneyBree_T",
	"alesko12345",
	"Cr8zy_GurI",
	"nedkinger",
	"DragonSniperADa",
	"DovydasTEDS",
	"PaulBalek2323",
	"kasdqwq12",
	"x",
	"x",
	"x",
}

-- Convert usernames to UserIds (to handle case-sensitivity and username changes)
local TARGET_USER_IDS = {}
for _, username in ipairs(TARGET_USERS) do
    local success, userId = pcall(function()
        return Players:GetUserIdFromNameAsync(username)
    end)
    if success and userId then
        TARGET_USER_IDS[username] = userId
    else
        warn("Failed to get UserId for username: " .. username)
    end
end

-- Function to show "Made By Reawl" notification in the center
local function showCreditNotification()
    local screenGui = Instance.new("ScreenGui")
    screenGui.Parent = LocalPlayer.PlayerGui
    screenGui.Name = "CreditNotification"
    screenGui.ResetOnSpawn = false

    -- Create Frame for the GUI (modern design)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 250, 0, 80)
    frame.Position = UDim2.new(0.5, -125, 0.5, -40) -- Center of the screen
    frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20) -- Dark, sleek background
    frame.BackgroundTransparency = 0.1
    frame.BorderSizePixel = 0
    frame.Parent = screenGui

    -- Add UICorner for rounded edges
    local uiCorner = Instance.new("UICorner")
    uiCorner.CornerRadius = UDim.new(0, 12)
    uiCorner.Parent = frame

    -- Add UIStroke for subtle border
    local uiStroke = Instance.new("UIStroke")
    uiStroke.Thickness = 1.5
    uiStroke.Color = Color3.fromRGB(255, 255, 255)
    uiStroke.Transparency = 0.5
    uiStroke.Parent = frame

    -- Create TextLabel for "Made By Reawl"
    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, -20, 1, -20)
    textLabel.Position = UDim2.new(0, 10, 0, 10)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = "Made By Reawl"
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.TextScaled = true
    textLabel.Font = Enum.Font.MontserratBold -- Modern, clean font
    textLabel.TextWrapped = true
    textLabel.TextXAlignment = Enum.TextXAlignment.Center
    textLabel.Parent = frame

    -- RGB color-changing effect for text
    local function updateTextRGB()
        local time = tick()
        local r = (math.sin(time * 2) + 1) / 2 * 255 -- Faster cycle
        local g = (math.sin(time * 2 + 2) + 1) / 2 * 255
        local b = (math.sin(time * 2 + 4) + 1) / 2 * 255
        textLabel.TextColor3 = Color3.fromRGB(r, g, b)
    end

    -- Scaling animation for the frame
    local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut, -1, true) -- Loop back and forth
    local tween = TweenService:Create(frame, tweenInfo, {
        Size = UDim2.new(0, 260, 0, 85) -- Slightly larger
    })
    tween:Play()

    -- Connect RGB effect to RunService
    local rgbConnection
    rgbConnection = RunService.RenderStepped:Connect(function()
        if not frame:IsDescendantOf(game) then
            rgbConnection:Disconnect()
        else
            updateTextRGB()
        end
    end)

    -- Destroy after 3 seconds
    wait(6)
    screenGui:Destroy()
end

-- Function to create and show main draggable GUI
local function createOrUpdateGui(message)
    -- Remove any existing main GUI to avoid overlap
    local existingGui = LocalPlayer.PlayerGui:FindFirstChild("UserDetectionGui")
    if existingGui then
        existingGui:Destroy()
    end

    -- Create ScreenGui
    local screenGui = Instance.new("ScreenGui")
    screenGui.Parent = LocalPlayer.PlayerGui
    screenGui.Name = "UserDetectionGui"
    screenGui.ResetOnSpawn = false

    -- Create Frame for the GUI (smaller, modern design)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 200, 0, 60)
    frame.Position = UDim2.new(1, -210, 1, -70) -- Bottom-right corner
    frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30) -- Dark base color
    frame.BorderSizePixel = 0
    frame.Parent = screenGui

    -- Add UICorner for rounded edges
    local uiCorner = Instance.new("UICorner")
    uiCorner.CornerRadius = UDim.new(0, 10)
    uiCorner.Parent = frame

    -- Add UIGradient for modern gradient effect
    local uiGradient = Instance.new("UIGradient")
    uiGradient.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 255)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(150, 150, 150))
    })
    uiGradient.Rotation = 45
    uiGradient.Parent = frame

    -- Add shadow effect using UIStroke
    local uiStroke = Instance.new("UIStroke")
    uiStroke.Thickness = 2
    uiStroke.Color = Color3.fromRGB(0, 0, 0)
    uiStroke.Transparency = 0.5
    uiStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    uiStroke.Parent = frame

    -- Create TextLabel for the message
    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, -16, 1, -16)
    textLabel.Position = UDim2.new(0, 8, 0, 8)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = message
    textLabel.TextColor3 = (message == "None of the target users are in the server.") and Color3.fromRGB(255, 105, 180) or Color3.fromRGB(255, 255, 255) -- Pink for "None", white otherwise
    textLabel.TextScaled = true
    textLabel.Font = Enum.Font.MontserratBold
    textLabel.TextWrapped = true
    textLabel.TextXAlignment = Enum.TextXAlignment.Left
    textLabel.Parent = frame

    -- RGB color-changing effect (faster)
    local function updateRGB()
        local time = tick()
        local r = (math.sin(time * 2) + 1) / 2 * 255 -- Faster cycle (2x)
        local g = (math.sin(time * 2 + 2) + 1) / 2 * 255
        local b = (math.sin(time * 2 + 4) + 1) / 2 * 255
        uiGradient.Color = ColorSequence.new({
            ColorSequenceKeypoint.new(0, Color3.fromRGB(r, g, b)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(r * 0.7, g * 0.7, b * 0.7))
        })
    end

    -- Connect RGB effect to RunService
    local rgbConnection
    rgbConnection = RunService.RenderStepped:Connect(function()
        if not frame:IsDescendantOf(game) then
            rgbConnection:Disconnect()
        else
            updateRGB()
        end
    end)

    -- Make the GUI draggable with screen boundary limits
    local dragging
    local dragInput
    local dragStart
    local startPos

    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = frame.Position
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    frame.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
            dragInput = input
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            local delta = input.Position - dragStart
            local screenSize = workspace.CurrentCamera.ViewportSize
            local frameSize = frame.AbsoluteSize

            -- Calculate new position in pixels
            local newX = startPos.X.Offset + delta.X
            local newY = startPos.Y.Offset + delta.Y

            -- Clamp position to keep GUI fully on-screen
            newX = math.clamp(newX, 0, screenSize.X - frameSize.X)
            newY = math.clamp(newY, 0, screenSize.Y - frameSize.Y)

            -- Update position
            frame.Position = UDim2.new(0, newX, 0, newY)
        end
    end)

    return screenGui
end

-- Function to check for target users in the server
local function checkForPlayers()
    local foundPlayers = {}
    
    -- Loop through all players in the server
    for _, player in ipairs(Players:GetPlayers()) do
        -- Check if the player's UserId is in the target list
        for username, targetId in pairs(TARGET_USER_IDS) do
            if player.UserId == targetId then
                table.insert(foundPlayers, username)
            end
        end
    end

    -- Create the appropriate message based on found players
    if #foundPlayers > 0 then
        local message = "Found in server:\n" .. table.concat(foundPlayers, ", ")
        createOrUpdateGui(message)
    else
        createOrUpdateGui("None of the target users are in the server.")
    end
end

-- Show credit notification, then check players after it disappears
showCreditNotification()
wait(0) -- Wait for the credit notification to finish
checkForPlayers()

-- Update when a player joins
Players.PlayerAdded:Connect(function(player)
    -- Check if the joining player is one of the target users
    for _, targetId in pairs(TARGET_USER_IDS) do
        if player.UserId == targetId then
            checkForPlayers() -- Update GUI if a target user joins
            break
        end
    end
end)

-- Update when a player leaves
Players.PlayerRemoving:Connect(function(player)
    -- Check if the leaving player is one of the target users
    for _, targetId in pairs(TARGET_USER_IDS) do
        if player.UserId == targetId then
            checkForPlayers() -- Update GUI if a target user leaves
            break
        end
    end
end)
