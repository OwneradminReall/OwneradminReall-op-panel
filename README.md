--[[
    OWNERADMINREALL-HUB UNIVERSAL MOBILE + INF JUMP
    Link: https://raw.githubusercontent.com/c00lkiddhacket-ctrl/OwneradminReall-Hub/main/README.md
]]

local L_1_ = game:GetService("Players").LocalPlayer
local L_2_ = L_1_:GetMouse()
local L_3_ = game:GetService("RunService")
local L_4_ = game:GetService("StarterGui")
local L_5_ = game:GetService("UserInputService")

local TargetLocation = nil
local NoclipEnabled = false
local InfJumpEnabled = false

-- Eski menüyü temizle
if L_1_.PlayerGui:FindFirstChild("OwneradminReall-Hub") then
    L_1_.PlayerGui["OwneradminReall-Hub"]:Destroy()
end

local sg = Instance.new("ScreenGui", L_1_.PlayerGui)
sg.Name = "OwneradminReall-Hub"
sg.ResetOnSpawn = false

local Frame = Instance.new("Frame", sg)
Frame.Size = UDim2.new(0, 200, 0, 290) -- Yeni buton için boyutu büyüttüm
Frame.Position = UDim2.new(0.5, -100, 0.4, 0)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Frame.BorderSizePixel = 2
Frame.Active = true
Frame.Draggable = true

local Corner = Instance.new("UICorner", Frame)
Corner.CornerRadius = UDim.new(0, 8)

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Text = "OwneradminReall-Hub"
Title.TextColor3 = Color3.fromRGB(255, 0, 0)
Title.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 18

-- --- 1. INF JUMP BUTTON (NEW) ---
local InfJumpBtn = Instance.new("TextButton", Frame)
InfJumpBtn.Size = UDim2.new(1, -20, 0, 35)
InfJumpBtn.Position = UDim2.new(0, 10, 0, 40)
InfJumpBtn.Text = "INF JUMP: OFF"
InfJumpBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
InfJumpBtn.TextColor3 = Color3.new(1, 1, 1)
InfJumpBtn.Font = Enum.Font.SourceSansBold

InfJumpBtn.MouseButton1Click:Connect(function()
    InfJumpEnabled = not InfJumpEnabled
    InfJumpBtn.Text = InfJumpEnabled and "INF JUMP: ON" or "INF JUMP: OFF"
    InfJumpBtn.BackgroundColor3 = InfJumpEnabled and Color3.fromRGB(150, 0, 0) or Color3.fromRGB(60, 60, 60)
end)

-- Inf Jump Logic (Safe Version)
L_5_.JumpRequest:Connect(function()
    if InfJumpEnabled then
        L_1_.Character:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping")
    end
end)

-- --- 2. NOCLIP BUTTON ---
local NoclipBtn = Instance.new("TextButton", Frame)
NoclipBtn.Size = UDim2.new(1, -20, 0, 35)
NoclipBtn.Position = UDim2.new(0, 10, 0, 80)
NoclipBtn.Text = "NOCLIP: OFF"
NoclipBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
NoclipBtn.TextColor3 = Color3.new(1, 1, 1)
NoclipBtn.Font = Enum.Font.SourceSansBold

NoclipBtn.MouseButton1Click:Connect(function()
    NoclipEnabled = not NoclipEnabled
    NoclipBtn.Text = NoclipEnabled and "NOCLIP: ON" or "NOCLIP: OFF"
    NoclipBtn.BackgroundColor3 = NoclipEnabled and Color3.fromRGB(150, 0, 0) or Color3.fromRGB(60, 60, 60)
end)

L_3_.Stepped:Connect(function()
    if NoclipEnabled and L_1_.Character then
        for _, v in pairs(L_1_.Character:GetDescendants()) do
            if v:IsA("BasePart") then v.CanCollide = false end
        end
    end
end)

-- --- 3. MARK POSITION ---
local SetBtn = Instance.new("TextButton", Frame)
SetBtn.Size = UDim2.new(1, -20, 0, 35)
SetBtn.Position = UDim2.new(0, 10, 0, 120)
SetBtn.Text = "MARK POSITION"
SetBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
SetBtn.TextColor3 = Color3.new(1, 1, 1)
SetBtn.Font = Enum.Font.SourceSansBold

SetBtn.MouseButton1Click:Connect(function()
    if L_1_.Character and L_1_.Character:FindFirstChild("HumanoidRootPart") then
        TargetLocation = L_1_.Character.HumanoidRootPart.CFrame
        L_4_:SetCore("SendNotification", {Title = "OwneradminReall", Text = "Position Marked!"})
    end
end)

-- --- 4. TP TO MARK ---
local TPBtn = Instance.new("TextButton", Frame)
TPBtn.Size = UDim2.new(1, -20, 0, 35)
TPBtn.Position = UDim2.new(0, 10, 0, 160)
TPBtn.Text = "TP TO MARK"
TPBtn.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
TPBtn.TextColor3 = Color3.new(1, 1, 1)
TPBtn.Font = Enum.Font.SourceSansBold

TPBtn.MouseButton1Click:Connect(function()
    if TargetLocation and L_1_.Character then
        L_1_.Character.HumanoidRootPart.CFrame = TargetLocation
    end
end)

-- --- 5. FORWARD (10) ---
local ForwardBtn = Instance.new("TextButton", Frame)
ForwardBtn.Size = UDim2.new(1, -20, 0, 35)
ForwardBtn.Position = UDim2.new(0, 10, 0, 200)
ForwardBtn.Text = "FORWARD (10)"
ForwardBtn.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
ForwardBtn.TextColor3 = Color3.new(1, 1, 1)
ForwardBtn.Font = Enum.Font.SourceSansBold

ForwardBtn.MouseButton1Click:Connect(function()
    if L_1_.Character and L_1_.Character:FindFirstChild("HumanoidRootPart") then
        L_1_.Character.HumanoidRootPart.CFrame = L_1_.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -10)
    end
end)

-- --- 6. CLOSE HUB ---
local CloseBtn = Instance.new("TextButton", Frame)
CloseBtn.Size = UDim2.new(1, -20, 0, 35)
CloseBtn.Position = UDim2.new(0, 10, 0, 240)
CloseBtn.Text = "DESTROY HUB"
CloseBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
CloseBtn.TextColor3 = Color3.new(1, 1, 1)
CloseBtn.Font = Enum.Font.SourceSansBold

CloseBtn.MouseButton1Click:Connect(function()
    sg:Destroy()
end)

L_4_:SetCore("SendNotification", {Title = "OwneradminReall-Hub", Text = "Inf Jump Added! Enjoy.", Duration = 5})
