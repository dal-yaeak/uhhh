-- Tamamen boş bir ScreenGui oluşturur
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "EmptyGui"
ScreenGui.ResetOnSpawn = true
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- 500x500 boyutunda bir Frame ekle
local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 500, 0, 500)
Frame.Position = UDim2.new(0.5, -250, 0.5, -250) -- Ortalamak için
Frame.AnchorPoint = Vector2.new(0.5, 0.5)
Frame.Parent = ScreenGui
-- Frame'e bir Gizle butonu ekle (sağ üst köşe)
 local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 40, 0, 40)
CloseButton.Position = UDim2.new(0, 0)
CloseButton.Text = "✕"
CloseButton.BackgroundColor3 = Color3.fromRGB(220, 60, 60)
CloseButton.TextColor3 = Color3.new(1,1,1)
CloseButton.Font = Enum.Font.SourceSansBold
CloseButton.TextSize = 28
Close.Parent = Frame



















































































































































































