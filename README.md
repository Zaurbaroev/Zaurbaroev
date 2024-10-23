local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")

local player = Players.LocalPlayer

-- Создаем ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "MyGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Создаем огромный текст
local titleText = Instance.new("TextLabel")
titleText.Size = UDim2.new(1, 0, 1, 0)
titleText.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
titleText.TextColor3 = Color3.fromRGB(255, 215, 0)
titleText.Text = "RT[z⚜️m]NEO"
titleText.Font = Enum.Font.SourceSansBold
titleText.TextSize = 100
titleText.TextScaled = true
titleText.AnchorPoint = Vector2.new(0.5, 0.5)
titleText.Position = UDim2.new(0.5, 0, 0.5, 0)
titleText.Parent = screenGui

-- Анимация появления текста
local appearTweenInfo = TweenInfo.new(2, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out)
local appearTween = TweenService:Create(titleText, appearTweenInfo, {TextTransparency = 0})
titleText.TextTransparency = 1
appearTween:Play()

appearTween.Completed:Wait()

-- Анимация исчезновения текста
local disappearTweenInfo = TweenInfo.new(2, Enum.EasingStyle.Bounce, Enum.EasingDirection.In)
local disappearTween = TweenService:Create(titleText, disappearTweenInfo, {TextTransparency = 1})
disappearTween:Play()

disappearTween.Completed:Wait()

-- Удаляем текст
titleText:Destroy()

-- Создаем основное окно (Frame) через 3 секунды
wait(3)

-- Создаем основное окно (Frame)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 200)
mainFrame.Position = UDim2.new(0.5, -130, 0.5, -160)
mainFrame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
mainFrame.BorderSizePixel = 0
mainFrame.ClipsDescendants = true
mainFrame.Parent = screenGui

-- Анимация появления окна
local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local tween = TweenService:Create(mainFrame, tweenInfo, {Position = UDim2.new(0.5, -130, 0.5, -160)})
tween:Play()

-- Заголовок окна
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0, 40)
titleLabel.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
titleLabel.BorderSizePixel = 0
titleLabel.Text = "RT[z⚜️m]NEO🔥"
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.Font = Enum.Font.SourceSansBold
titleLabel.TextSize = 18
titleLabel.Parent = mainFrame

-- Кнопка сворачивания
local minimizeButton = Instance.new("TextButton")
minimizeButton.Size = UDim2.new(0, 40, 0, 40)
minimizeButton.Position = UDim2.new(1, -80, 0, 0)
minimizeButton.Text = "─"
minimizeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
minimizeButton.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
minimizeButton.Font = Enum.Font.SourceSansBold
minimizeButton.TextSize = 18
minimizeButton.BorderSizePixel = 0
minimizeButton.Parent = mainFrame

local isMinimized = false
minimizeButton.MouseButton1Click:Connect(function()
    if isMinimized then
        mainFrame:TweenSize(UDim2.new(0, 300, 0, 200), "Out", "Quad", 0.5, true)
    else
        mainFrame:TweenSize(UDim2.new(0, 300, 0, 40), "Out", "Quad", 0.5, true)
    end
    isMinimized = not isMinimized
end)

-- Кнопка закрытия с анимацией
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 40, 0, 40)
closeButton.Position = UDim2.new(1, -40, 0, 0)
closeButton.Text = "✖"
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
closeButton.Font = Enum.Font.SourceSansBold
closeButton.TextSize = 18
closeButton.BorderSizePixel = 0
closeButton.Parent = mainFrame

closeButton.MouseButton1Click:Connect(function()
    local closeTween = TweenService:Create(mainFrame, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {Position = UDim2.new(0.5, -130, 1, 0)})
    closeTween:Play()
    closeTween.Completed:Connect(function()
        screenGui:Destroy()
    end)
end)

-- Перемещение окна
local dragging = false
local dragInput, mousePos, framePos

titleLabel.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        mousePos = input.Position
        framePos = mainFrame.Position
    end
end)

titleLabel.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

titleLabel.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - mousePos
        mainFrame.Position = UDim2.new(
            framePos.X.Scale,
            framePos.X.Offset + delta.X,
            framePos.Y.Scale,
            framePos.Y.Offset + delta.Y
        )
    end
end)

-- Автофарм
local positions = { 
    Vector3.new(-57.61, 104.29, 1369.45), 
    Vector3.new(-55.94, 103.61, 2134.76), 
    Vector3.new(-64.68, 103.50, 2908.48), 
    Vector3.new(-49.12, 79.44, 3669.15), 
    Vector3.new(-57.28, 99.04, 4445.34), 
    Vector3.new(-57.33, 110.74, 5215.95), 
    Vector3.new(-56.28, 82.33, 5989.16), 
    Vector3.new(-67.14, 85.04, 6749.35), 
    Vector3.new(-33.67, 85.31, 7536.77), 
    Vector3.new(-49.04, 105.27, 8302.19), 
    Vector3.new(-57.71, 59.51, 8669.07), 
    Vector3.new(-53.28, -357.18, 9489.82), 
} 

local isAutoFarmActive = false

local function moveToPosition(position) 
    local character = player.Character 
    if character and character:FindFirstChild("HumanoidRootPart") then 
        local humanoidRootPart = character.HumanoidRootPart 
        local tween = TweenService:Create(humanoidRootPart, TweenInfo.new(2), {CFrame = CFrame.new(position)}) 
        tween:Play() 
        tween.Completed:Wait() 
    end 
end 

local function toggleAutoFarm() 
    if isAutoFarmActive then 
        while isAutoFarmActive do 
            for _, position in ipairs(positions) do 
                moveToPosition(position) 
            end 
            wait(15) 
        end 
    end 
end 

local buttons = {"Auto Farm", "RT[z⚜️m]Neo"}
for i, name in ipairs(buttons) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -10, 0, 30)
    button.Position = UDim2.new(0, 5, 0, 50 + (i - 1) * 40)
    button.Text = name
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
    button.Font = Enum.Font.SourceSans
    button.TextSize = 18
    button.BorderSizePixel = 0
    button.Parent = mainFrame
    
    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(75, 75, 75)}):Play()
    end)
    
    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(55, 55, 55)}):Play()
    end)

    if name == "Auto Farm" then
        button.MouseButton1Click:Connect(function()
            isAutoFarmActive = not isAutoFarmActive
            if isAutoFarmActive then
                toggleAutoFarm()
                button.Text = "Stop Auto Farm"
            else
                button.Text = "Auto Farm"
            end
        end)
    end
end

local function maintainGui() 
    while true do 
        wait(1) 
        if not player.PlayerGui:FindFirstChild("MyGui") then 
            local ScreenGui = Instance.new("ScreenGui") 
            ScreenGui.Name = "MyGui" 
            ScreenGui.ResetOnSpawn = false 
            ScreenGui.Parent = player:WaitForChild("PlayerGui") 
        end 
    end 
end 

maintainGui()
