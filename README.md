-- OwneradminReall OP Panel
local ScreenGui = Instance.new("ScreenGui")
local Main = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local SpeedBox = Instance.new("TextBox")
local SetButton = Instance.new("TextButton")

ScreenGui.Parent = game:GetService("CoreGui")
Main.Parent = ScreenGui
Main.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Main.Size = UDim2.new(0, 200, 0, 150)
Main.Position = UDim2.new(0.5, -100, 0.5, -75)
Main.Active = true
Main.Draggable = true

Title.Parent = Main
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "OP PANEL - Hız"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1

SpeedBox.Parent = Main
SpeedBox.Position = UDim2.new(0.1, 0, 0.4, 0)
SpeedBox.Size = UDim2.new(0.8, 0, 0, 30)
SpeedBox.PlaceholderText = "Hız Yaz..."
SpeedBox.Text = ""

SetButton.Parent = Main
SetButton.Position = UDim2.new(0.1, 0, 0.7, 0)
SetButton.Size = UDim2.new(0.8, 0, 0, 30)
SetButton.Text = "UYGULA"
SetButton.BackgroundColor3 = Color3.fromRGB(0, 200, 100)

SetButton.MouseButton1Click:Connect(function()
    local s = tonumber(SpeedBox.Text)
    if s then
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = s
    end
end)
