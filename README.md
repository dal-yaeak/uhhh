--crate a screenGui
local screenGui = Instance . new ["screenGui"]
screenGui . Parent =
game .Players .LocalPlayer:WaitForChild("PlayerGui")

-- Create a Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0.8, 0, 0.8, 0) -- 80% width and height of the screen
frame.Position = UDim2.new(0.1, 0, 0.1, 0) -- Center the frame
frame.BackgroundTransparency = 0.5 -- Transparent background
frame.BackgroundColor3 = Color3.new(0, 0, 0) -- Black background
frame.Parent = screenGui

-- Create 24 TextLabels inside the Frame
for i = 1, 24 do
    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, 0, 1 / 24, 0) -- Divide the frame height into 24 rows
    textLabel.Position = UDim2.new(0, 0, (i - 1) / 24, 0) -- Position each label row by row
    textLabel.BackgroundTransparency = 1 -- Fully transparent background for the label
    textLabel.Text = "Satır " .. i -- Display "Satır" followed by the row number
    textLabel.TextColor3 = Color3.new(1, 1, 1) -- White text color
    textLabel.TextScaled = true -- Automatically scale the text to fit
    textLabel.Parent = frame
end
 local gui = Instance.new("ScreenGui", game.Players.LocalPlayer.PlayerGui)
local btn = Instance.new("TextButton", gui)
btn.Size = UDim2.new(0,120,0,40)
btn.Position = UDim2.new(0.5,-60,0.5,-20)
btn.Text = "Gizle"
btn.BackgroundColor3 = Color3.fromRGB(200,60,60)
btn.TextColor3 = Color3.new(1,1,1)
btn.MouseButton1Click:Connect(function()
    gui.Enabled = false
end)







































































