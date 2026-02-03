local Player = game:GetService("Players").LocalPlayer
local Mouse = Player:GetMouse()
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("StarterGui")

local TargetLocation = nil
local NoclipEnabled = false

-- Eski menüyü temizle
if Player.PlayerGui:FindFirstChild("OwneradminReallOp") then
    Player.PlayerGui.OwneradminReallOp:Destroy()
end

local sg = Instance.new("ScreenGui", Player.PlayerGui)
sg.Name = "OwneradminReallOp"
sg.ResetOnSpawn = false

local Frame = Instance.new("Frame", sg)
Frame.Size = UDim2.new(0, 200, 0, 220) -- Noclip butonu için biraz daha büyütüldü
Frame.Position = UDim2.new(0.5, -100, 0.4, 0)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Frame.BorderSizePixel = 2
Frame.Active = true
Frame.Draggable = true

-- Header
local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 25)
Title.Text = "OwneradminReall-Op"
Title.TextColor3 = Color3.fromRGB(255, 215, 0)
Title.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Title.Font = Enum.Font.SourceSansBold

-- 1. NOCLIP BUTTON
local NoclipBtn = Instance.new("TextButton", Frame)
NoclipBtn.Size = UDim2.new(1, -20, 0, 30)
NoclipBtn.Position = UDim2.new(0, 10, 0, 35)
NoclipBtn.Text = "NOCLIP: OFF"
NoclipBtn.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
NoclipBtn.TextColor3 = Color3.new(1, 1, 1)
NoclipBtn.Font = Enum.Font.SourceSansBold

NoclipBtn.MouseButton1Click:Connect(function()
    NoclipEnabled = not NoclipEnabled
    if NoclipEnabled then
        NoclipBtn.Text = "NOCLIP: ON"
        NoclipBtn.BackgroundColor3 = Color3.fromRGB(0, 150, 150)
    else
        NoclipBtn.Text = "NOCLIP: OFF"
        NoclipBtn.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
    end
end)

-- Noclip Döngüsü
RunService.Stepped:Connect(function()
    if NoclipEnabled and Player.Character then
        for _, part in pairs(Player.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = false
            end
        end
    end
end)

-- 2. SET TARGET
local SetBtn = Instance.new("TextButton", Frame)
SetBtn.Size = UDim2.new(1, -20, 0, 30)
SetBtn.Position = UDim2.new(0, 10, 0, 70)
SetBtn.Text = "SET TARGET"
SetBtn.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
SetBtn.TextColor3 = Color3.new(1, 1, 1)
SetBtn.Font = Enum.Font.SourceSansBold

SetBtn.MouseButton1Click:Connect(function()
    TargetLocation = Mouse.Hit.p
    CoreGui:SetCore("SendNotification", {Title = "OwneradminReall", Text = "Target Set!"})
end)

-- 3. TELEPORT
local TPBtn = Instance.new("TextButton", Frame)
TPBtn.Size = UDim2.new(1, -20, 0, 30)
TPBtn.Position = UDim2.new(0, 10, 0, 105)
TPBtn.Text = "TELEPORT"
TPBtn.BackgroundColor3 = Color3.fromRGB(0, 150, 0)
TPBtn.TextColor3 = Color3.new(1, 1, 1)
TPBtn.Font = Enum.Font.SourceSansBold

TPBtn.MouseButton1Click:Connect(function()
    if TargetLocation and Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
        Player.Character.HumanoidRootPart.CFrame = CFrame.new(TargetLocation + Vector3.new(0, 3, 0))
    end
end)

-- 4. GO FORWARD 10
local ForwardBtn = Instance.new("TextButton", Frame)
ForwardBtn.Size = UDim2.new(1, -20, 0, 30)
ForwardBtn.Position = UDim2.new(0, 10, 0, 140)
ForwardBtn.Text = "GO FORWARD 10"
ForwardBtn.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
ForwardBtn.TextColor3 = Color3.new(1, 1, 1)
ForwardBtn.Font = Enum.Font.SourceSansBold

ForwardBtn.MouseButton1Click:Connect(function()
    if Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
        Player.Character.HumanoidRootPart.CFrame = Player.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -10)
    end
end)

-- 5. OwneradminReall (YT)
local YTBtn = Instance.new("TextButton", Frame)
YTBtn.Size = UDim2.new(1, -20, 0, 30)
YTBtn.Position = UDim2.new(0, 10, 0, 175)
YTBtn.Text = "OwneradminReall"
YTBtn.BackgroundColor3 = Color3.fromRGB(0, 80, 200)
YTBtn.TextColor3 = Color3.new(1, 1, 1)
YTBtn.Font = Enum.Font.SourceSansBold

YTBtn.MouseButton1Click:Connect(function()
    if setclipboard then
        setclipboard("https://www.youtube.com/@OwneradminReall")
        CoreGui:SetCore("SendNotification", {Title = "OwneradminReall", Text = "Link copied!"})
    end
end)
