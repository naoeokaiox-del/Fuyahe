-- FUYAHE NYA 😼 ULTRA LEVE UI – by 😼Nekomata mana😼
local Player = game.Players.LocalPlayer
local GUI = Instance.new("ScreenGui", Player:WaitForChild("PlayerGui"))
GUI.ResetOnSpawn = false

-- GUI PRINCIPAL
local Main = Instance.new("Frame", GUI)
Main.Size = UDim2.new(0, 300, 0, 520)
Main.Position = UDim2.new(0.5, -150, 0.3, 0)
Main.BackgroundColor3 = Color3.fromRGB(20,20,20)
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
local UICorner = Instance.new("UICorner", Main)
UICorner.CornerRadius = UDim.new(0,16)
local UIStroke = Instance.new("UIStroke", Main)
UIStroke.Color = Color3.fromRGB(170,0,255)
UIStroke.Thickness = 2

-- FOTO TOPO
local TopImage = Instance.new("ImageLabel", Main)
TopImage.Size = UDim2.new(1, -20, 0, 80)
TopImage.Position = UDim2.new(0, 10, 0, 10)
TopImage.Image = "rbxassetid://132904741245694"
TopImage.BackgroundTransparency = 1
local TopCorner = Instance.new("UICorner", TopImage)
TopCorner.CornerRadius = UDim.new(0,12)
local TopStroke = Instance.new("UIStroke", TopImage)
TopStroke.Color = Color3.fromRGB(170,0,255)
TopStroke.Thickness = 2

-- TÍTULO RGB
local Title = Instance.new("TextLabel", Main)
Title.Size = UDim2.new(1,0,0,25)
Title.Position = UDim2.new(0,0,0,95)
Title.BackgroundTransparency = 1
Title.Text = "Fuyahe Nya 😼"
Title.TextScaled = true
Title.Font = Enum.Font.GothamBold
task.spawn(function()
while true do
Title.TextColor3 = Color3.fromHSV(tick()%5/5,1,1)
task.wait(0.05)
end
end)

-- SCROLL
local Scroll = Instance.new("ScrollingFrame", Main)
Scroll.Size = UDim2.new(1, -20, 0, 380)
Scroll.Position = UDim2.new(0,10,0,130)
Scroll.BackgroundTransparency = 1
Scroll.ScrollBarThickness = 6
local UIList = Instance.new("UIListLayout", Scroll)
UIList.Padding = UDim.new(0,8)

-- FUNÇÃO PARA BOTÕES
local function MakeButton(name)
local B = Instance.new("TextButton", Scroll)
B.Size = UDim2.new(1,-10,0,40)
B.BackgroundColor3 = Color3.fromRGB(40,0,55)
B.TextColor3 = Color3.fromRGB(255,255,255)
B.TextScaled = true
B.Font = Enum.Font.GothamBold
B.Text = name
local corner = Instance.new("UICorner", B)
corner.CornerRadius = UDim.new(0,12)
local stroke = Instance.new("UIStroke", B)
stroke.Color = Color3.fromRGB(170,0,255)
stroke.Thickness = 2
return B
end

-- FUNÇÕES DE OTIMIZAÇÃO
local function RemoveDecoratives()
for _,v in ipairs(workspace:GetDescendants()) do
if v:IsA("Model") then
local nameLower = string.lower(v.Name)
if string.find(nameLower,"tree") or string.find(nameLower,"plant") or string.find(nameLower,"bush")
or string.find(nameLower,"lata") or string.find(nameLower,"trash") or string.find(nameLower,"bench")
or string.find(nameLower,"stone") or string.find(nameLower,"rock") then
v:Destroy()
end
end
end
end

local function RemoveTextures()
for _,v in ipairs(workspace:GetDescendants()) do
if v:IsA("Decal") or v:IsA("Texture") then
v:Destroy()
elseif v:IsA("MeshPart") then
v.TextureID = ""
v.Material = Enum.Material.Plastic
v.Color = Color3.fromRGB(200,200,200)
elseif v:IsA("Part") then
v.Material = Enum.Material.Plastic
v.Color = Color3.fromRGB(200,200,200)
v.Reflectance = 0
v.CastShadow = false
end
end
end

local function AntiLag()
for _,v in ipairs(workspace:GetDescendants()) do
if v:IsA("ParticleEmitter") or v:IsA("Smoke") or v:IsA("Fire")
or v:IsA("Beam") or v:IsA("PointLight") or v:IsA("SpotLight")
or v:IsA("SurfaceLight") then
v:Destroy()
end
if v:IsA("Part") or v:IsA("MeshPart") then
v.CastShadow = false
end
end
end

local function CleanNonEssential()
for _,v in ipairs(workspace:GetDescendants()) do
if v:IsA("Model") or v:IsA("Part") or v:IsA("MeshPart") then
local nameLower = string.lower(v.Name)
if string.find(nameLower,"tree") or string.find(nameLower,"plant") or string.find(nameLower,"bush")
or string.find(nameLower,"lata") or string.find(nameLower,"trash") or string.find(nameLower,"bench")
or string.find(nameLower,"stone") or string.find(nameLower,"rock") then
v:Destroy()
end
end
end
end

local function CleanPlayers()
for _, plr in ipairs(game.Players:GetPlayers()) do
if plr.Character then
local char = plr.Character
for _, item in ipairs(char:GetDescendants()) do
if item:IsA("Shirt") or item:IsA("Pants") or item:IsA("Accessory")
or item:IsA("Decal") or item:IsA("Texture") then
item:Destroy()
end
if item:IsA("MeshPart") or item:IsA("Part") then
item.Material = Enum.Material.Plastic
item.Color = Color3.fromRGB(200,200,200)
item.Reflectance = 0
item.CastShadow = false
end
end
local head = char:FindFirstChild("Head")
if head and head:IsA("MeshPart") then
head.Size = Vector3.new(2,2,2)
head.Shape = Enum.PartType.Block
head.Material = Enum.Material.Plastic
head.Color = Color3.fromRGB(200,200,200)
end
end
end
end

local function OptimizeTexturesAndSky()
RemoveTextures()
for _,v in ipairs(game.Lighting:GetChildren()) do
if v:IsA("Sky") then
v:Destroy()
end
end
end

local function RemoveSpecificObjects()
local paths = {
{"Map","Floor","Roads","Stadium","Stadium"},
{"Map","Floor","Roads","Railing","Railing"}
}
for _, path in ipairs(paths) do
local current = workspace
for _, seg in ipairs(path) do
current = current:FindFirstChild(seg)
if not current then break end
end
if current then
current:Destroy()
end
end
end

local function TeleportToDummy()
local live = workspace:FindFirstChild("Live")
if live then
local dummy = live:FindFirstChild("Weakest Dummy")
if dummy and dummy:FindFirstChild("HumanoidRootPart") and Player.Character and Player.Character:FindFirstChild("HumanoidRootPart") then
Player.Character.HumanoidRootPart.CFrame = dummy.HumanoidRootPart.CFrame + Vector3.new(0,3,0)
end
end
end

-- BOTÕES
local btn1 = MakeButton("1 • Remover Objetos Decorativos")
btn1.MouseButton1Click:Connect(RemoveDecoratives)

local btn2 = MakeButton("2 • Limpar Texturas / Simplificar")
btn2.MouseButton1Click:Connect(RemoveTextures)

local btn3 = MakeButton("3 • Otimizar Tudo")
btn3.MouseButton1Click:Connect(AntiLag)

local btn4 = MakeButton("4 • Limpar Objetos Não Essenciais")
btn4.MouseButton1Click:Connect(CleanNonEssential)

local btn5 = MakeButton("5 • Otimizar Players")
btn5.MouseButton1Click:Connect(CleanPlayers)

local btn6 = MakeButton("6 • Remover Texturas e Céu")
btn6.MouseButton1Click:Connect(OptimizeTexturesAndSky)

local btn7 = MakeButton("7 • Teleportar ao Dummy")
btn7.MouseButton1Click:Connect(TeleportToDummy)

local btn8 = MakeButton("8 • Remover Objetos Específicos")
btn8.MouseButton1Click:Connect(RemoveSpecificObjects)

-- RODAPÉ
local credit = Instance.new("TextLabel", Main)
credit.Size = UDim2.new(1,-10,0,15)
credit.Position = UDim2.new(0,5,1,-20)
credit.Text = "Add.Tiktok/Fuyahe – by 😼Nekomata mana😼"
credit.BackgroundTransparency = 1
credit.TextColor3 = Color3.fromRGB(180,0,255)
credit.TextScaled = true
credit.Font = Enum.Font.GothamBold

-- BOTÃO FLUTUANTE ABRIR/FECHAR DESLIZÁVEL
local Toggle = Instance.new("ImageButton", GUI)
Toggle.Size = UDim2.new(0,50,0,50)
Toggle.Position = UDim2.new(0,10,0.5,-25)
Toggle.Image = "rbxassetid://132904741245694"
Toggle.BackgroundTransparency = 0.3
Toggle.BorderSizePixel = 0
local corner = Instance.new("UICorner", Toggle)
corner.CornerRadius = UDim.new(1,0)
Toggle.Active = true
Toggle.Draggable = true

local isOpen = true
Toggle.MouseButton1Click:Connect(function()
isOpen = not isOpen
Main.Visible = isOpen
end)

-- Atualizar players constantemente
game:GetService("RunService").Stepped:Connect(CleanPlayers)
