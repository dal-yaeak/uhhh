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
local frame = script.ParentCloseButton.MouseButton1Click:Connect(function()
    Frame.Visible = false
end)

local dragging = false
local dragInput, dragStart, startPos

local function update(input)
    local delta = input.Position - dragStart
    frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
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

-- Başlık (Label) ekle
local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(1, 0, 0, 50) -- Genişlik: frame kadar, yükseklik: 50px
TitleLabel.Position = UDim2.new(0, 0, 0, 0) -- Frame'in üstüne hizala
TitleLabel.BackgroundColor3 = Color3.fromRGB(200, 200, 255)
TitleLabel.Text = "wandarana hub"
TitleLabel.TextColor3 = Color3.fromRGB(40, 40, 80)
TitleLabel.Font = Enum.Font.SourceSansBold
TitleLabel.TextSize = 32
TitleLabel.Parent = Frame
TitleLabel.BorderSizePixel = 0
-- Frame ve varsa içeriği oluşturulmuş olmalı!
-- Aşağıdaki kodu, Frame ve içeriğini oluşturduktan sonra ekle

-- İçerik (örnek olarak bir TextLabel, kaydırılacak)
local Content = Instance.new("TextLabel")
Content.Size = UDim2.new(1, -50, 0, 1000) -- İçerik Frame'den daha uzun, kaydırma için
Content.Position = UDim2.new(0, 0, 0, 0)
Content.BackgroundColor3 = Color3.fromRGB(245, 245, 255)
Content.Text = "Kaydırılabilir içerik\n" .. string.rep("Daha fazla içerik!\n", 20)
Content.TextSize = 18
Content.TextXAlignment = Enum.TextXAlignment.Left
Content.TextYAlignment = Enum.TextYAlignment.Top
Content.TextWrapped = true
Content.Parent = Frame

-- Yukarı butonu
local UpButton = Instance.new("TextButton")
UpButton.Size = UDim2.new(0, 40, 0, 40)
UpButton.Position = UDim2.new(1, -45, 0, 55) -- Sağ üstten biraz aşağı
UpButton.Text = "▲"
UpButton.BackgroundColor3 = Color3.fromRGB(180, 180, 200)
UpButton.TextColor3 = Color3.new(0,0,0)
UpButton.Font = Enum.Font.ArialBold
UpButton.TextSize = 28
UpButton.Parent = Frame

-- Aşağı butonu
local DownButton = Instance.new("TextButton")
DownButton.Size = UDim2.new(0, 40, 0, 40)
DownButton.Position = UDim2.new(1, -45, 1, -45) -- Sağ alt köşe
DownButton.Text = "▼"
DownButton.BackgroundColor3 = Color3.fromRGB(180, 180, 200)
DownButton.TextColor3 = Color3.new(0,0,0)
DownButton.Font = Enum.Font.ArialBold
DownButton.TextSize = 28
DownButton.AnchorPoint = Vector2.new(0, 1)
DownButton.Parent = Frame

-- Kaydırma ayarları
local scrollStep = 40 -- Her tıklamada kaç piksel kayacak
local minY = 0
local maxY = math.max(0, Content.AbsoluteSize.Y - Frame.AbsoluteSize.Y)

-- Frame yeniden boyutlanınca maxY güncelle
Frame:GetPropertyChangedSignal("AbsoluteSize"):Connect(function()
    maxY = math.max(0, Content.AbsoluteSize.Y - Frame.AbsoluteSize.Y)
end)
Content:GetPropertyChangedSignal("AbsoluteSize"):Connect(function()
    maxY = math.max(0, Content.AbsoluteSize.Y - Frame.AbsoluteSize.Y)
end)

-- Yukarı kaydır
UpButton.MouseButton1Click:Connect(function()
    local y = Content.Position.Y.Offset + scrollStep
    if y > minY then y = minY end
    Content.Position = UDim2.new(0, 0, 0, y)
end)

-- Aşağı kaydır
DownButton.MouseButton1Click:Connect(function()
    local y = Content.Position.Y.Offset - scrollStep
    if math.abs(y) > maxY then y = -maxY end
    Content.Position = UDim2.new(0, 0, 0, y)
end)

-- Uzun yazı için kaydırılabilir TextBox ekle
local LongText = Instance.new("TextBox")
LongText.Size = UDim2.new(1, -60, 1, -110) -- Sağdan ve alttan butonlar için boşluk bırak
LongText.Position = UDim2.new(0, 10, 0, 60) -- Üstte başlık ve butonlar için boşluk bırak
LongText.BackgroundColor3 = Color3.fromRGB(245, 245, 255)
LongText.TextColor3 = Color3.fromRGB(30,30,60)
LongText.Font = Enum.Font.SourceSans
LongText.TextSize = 22
LongText.TextWrapped = true
LongText.TextXAlignment = Enum.TextXAlignment.Left
LongText.TextYAlignment = Enum.TextYAlignment.Top
LongText.TextEditable = false
LongText.ClearTextOnFocus = false
LongText.MultiLine = true
LongText.Text = [[
Merhaba bunu okuyorsan suan ana sayfadasın
senin icin sıkılmadiye buton ekledim
bu buttonla para kasa bilir sin
suan guim v0 0.5 süründe
neyse ben guiyi yapayım v2 görüsürüz
onda guim daha güzel olur belki
iyi günler.
]]
LongText.Parent = Frame

-- ... (önceki kodlar, Frame ve LongText eklenmiş olmalı)

-- Auto Bonds butonu ekle (uzun yazının hemen altına)
local AutoBondsButton = Instance.new("TextButton")
AutoBondsButton.Size = UDim2.new(0, 180, 0, 45)
AutoBondsButton.Position = UDim2.new(0.5, -90, 0, LongText.Position.Y.Offset + LongText.Size.Y.Offset + 10)
AutoBondsButton.BackgroundColor3 = Color3.fromRGB(120, 230, 120)
AutoBondsButton.Text = "Auto Bonds"
AutoBondsButton.TextColor3 = Color3.fromRGB(0,0,0)
AutoBondsButton.Font = Enum.Font.SourceSansBold
AutoBondsButton.TextSize = 22
AutoBondsButton.Parent = Frame

local autoCollecting = false
local autoThread = nil

-- Oyununa özel: "turda mıyız?" kontrolü ve para toplama fonksiyonu
local function IsRoundActive()
    -- Bunu oyununun round sistemine göre düzenle
    return workspace:FindFirstChild("CurrentRound") and workspace.CurrentRound.Value == true
end

local function CollectAllBonds()
    -- Oyununda Bond nesnesine göre uyarlamalısın!
    for _, bond in ipairs(workspace:GetChildren()) do
        if bond.Name == "Bond" and bond:IsA("Part") then
            firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, bond, 0)
            wait()
            firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart, bond, 1)
        end
    end
end

local function StartAutoCollect()
    autoCollecting = true
    AutoBondsButton.Text = "Auto Bonds (Açık)"
    autoThread = task.spawn(function()
        while autoCollecting do
            if IsRoundActive() then
                CollectAllBonds()
            end
            task.wait(1)
        end
    end)
end

local function StopAutoCollect()
    autoCollecting = false
    AutoBondsButton.Text = "Auto Bonds"
end

AutoBondsButton.MouseButton1Click:Connect(function()
    if not autoCollecting then
        StartAutoCollect()
    else
        StopAutoCollect()
    end
end)












































































































































































