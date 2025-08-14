local userKey = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui"):FindFirstChild("InputBox").Text

if userKey ~= "MINHA_CHAVE123" then
    return warn("Chave inválida! Você não pode usar este script.")
end

-- Pega o script ofuscado do GitHub
loadstring(game:HttpGet('https://raw.githubusercontent.com/seu_usuario/seu_repositorio/main/SCRIPT_READ.lua?time='..tick()))()

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Stats = game:GetService("Stats")
local UserInputService = game:GetService("UserInputService")
local VirtualUser = game:GetService("VirtualUser")
local LocalPlayer = Players.LocalPlayer
local CoreGui = game:GetService("CoreGui") -- Adicionado

-- === PAINEL PRINCIPAL ===
local screenGuiMain = Instance.new("ScreenGui")
screenGuiMain.Name = "MainGui"
screenGuiMain.ResetOnSpawn = false -- Adicionado
screenGuiMain.IgnoreGuiInset = true -- Adicionado
screenGuiMain.Parent = CoreGui -- Alterado para CoreGui

local painel = Instance.new("Frame")
painel.Size = UDim2.new(0, 480, 0, 340)
painel.Position = UDim2.new(0.3, 0, 0.3, 0)
painel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
painel.BorderSizePixel = 0
painel.Parent = screenGuiMain
painel.Active = true
painel.Draggable = true

local titulo = Instance.new("TextLabel")
titulo.Size = UDim2.new(1, 0, 0, 30)
titulo.BackgroundTransparency = 1
titulo.Text = "🔥DRAGON BLOX ULTIMATE"
titulo.Font = Enum.Font.GothamBold
titulo.TextSize = 29
titulo.TextColor3 = Color3.fromRGB(0, 255, 0)
titulo.Parent = painel

local linha = Instance.new("Frame")
linha.Size = UDim2.new(1, 0, 0, 2)
linha.Position = UDim2.new(0, 0, 0, 28)
linha.BackgroundColor3 = Color3.fromRGB(0, 85, 255)
linha.BorderSizePixel = 0
linha.Parent = painel

local botaoFechar = Instance.new("TextButton")
botaoFechar.Size = UDim2.new(0, 25, 0, 25)
botaoFechar.Position = UDim2.new(1, -30, 0, 2)
botaoFechar.Text = "-"
botaoFechar.Font = Enum.Font.SourceSansBold
botaoFechar.TextSize = 20
botaoFechar.TextColor3 = Color3.fromRGB(255, 255, 255)
botaoFechar.BackgroundTransparency = 1
botaoFechar.Parent = painel

local barraFechada = Instance.new("TextButton")
barraFechada.Size = UDim2.new(0, 380, 0, 30)
barraFechada.Position = painel.Position
barraFechada.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
barraFechada.BorderSizePixel = 0
barraFechada.Text = "🔥 DBU DRAGON BLOX ULTIMATE"
barraFechada.Font = Enum.Font.GothamBold
barraFechada.TextSize = 25
barraFechada.TextColor3 = Color3.fromRGB(0, 255, 0)
barraFechada.Visible = false
barraFechada.Active = true
barraFechada.Draggable = true
barraFechada.Parent = screenGuiMain

botaoFechar.MouseButton1Click:Connect(function()
    painel.Visible = false
    barraFechada.Visible = true
    barraFechada.Position = painel.Position
end)

barraFechada.MouseButton1Click:Connect(function()
    painel.Visible = true
    barraFechada.Visible = false
    painel.Position = barraFechada.Position
end)

-- Label info: FPS e Ping
local infoLabel = Instance.new("TextLabel")
infoLabel.Size = UDim2.new(0, 100, 0, 62)
infoLabel.Position = UDim2.new(1, -205, 0, 5)
infoLabel.BackgroundTransparency = 1
infoLabel.Font = Enum.Font.GothamBold
infoLabel.TextSize = 16
infoLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
infoLabel.TextXAlignment = Enum.TextXAlignment.Right
infoLabel.Text = "FPS: 0 | Ping: 0 ms"
infoLabel.Parent = painel

local lastTime = tick()
local frames = 0
RunService.RenderStepped:Connect(function()
    frames += 1
    if tick() - lastTime >= 1 then
        local fps = frames
        frames = 0
        lastTime = tick()

        local ping = math.floor(Stats.Network.ServerStatsItem["Data Ping"]:GetValue())
        infoLabel.Text = string.format("FPS: %d | Ping: %d ms", fps, ping)
    end
end)

-- Label AFK Timer
local afkLabel = Instance.new("TextLabel")
afkLabel.Size = UDim2.new(0, 300, 0, 61)
afkLabel.Position = UDim2.new(0.05, 0, 0, 100)
afkLabel.BackgroundTransparency = 1
afkLabel.Font = Enum.Font.GothamBold
afkLabel.TextSize = 18
afkLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
afkLabel.Text = "AFK Timer: 0s"
afkLabel.Parent = painel

local afkTimer = 0
local afkInterval = 30

local function resetAFK()
    VirtualUser:CaptureController()
    VirtualUser:ClickButton2(Vector2.new())
    afkLabel.Text = "AFK Timer: 0s (Clique enviado)"
    afkTimer = 0
end

UserInputService.InputBegan:Connect(function()
    afkTimer = 0
    afkLabel.Text = "AFK Timer: 0s (Ativo)"
end)

RunService.Heartbeat:Connect(function(deltaTime)
    afkTimer += deltaTime
    if afkTimer >= afkInterval then
        resetAFK()
    else
        afkLabel.Text = string.format("AFK Timer: %ds", math.floor(afkTimer))
    end
end)

-- Função para criar toggle Material UI
local function criarMaterialToggle(nome, posX, posY)
    local container = Instance.new("Frame")
    container.Size = UDim2.new(0, 200, 0, 30)
    container.Position = UDim2.new(posX, 0, posY, 0)
    container.BackgroundTransparency = 1
    container.Parent = painel

    local label = Instance.new("TextLabel")
    label.Text = nome
    label.Font = Enum.Font.GothamBold
    label.TextSize = 18
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.BackgroundTransparency = 1
    label.Size = UDim2.new(0.75, 0, 1, 0)
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = container

    local toggleBtn = Instance.new("TextButton")
    toggleBtn.Size = UDim2.new(0, 40, 0, 20)
    toggleBtn.Position = UDim2.new(0.8, 0, 0.1, 0)
    toggleBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
    toggleBtn.AutoButtonColor = false
    toggleBtn.Text = ""
    toggleBtn.Parent = container
    toggleBtn.AnchorPoint = Vector2.new(0.5, 0.5)

    local circle = Instance.new("Frame")
    circle.Size = UDim2.new(0, 18, 0, 18)
    circle.Position = UDim2.new(0, 1, 0, 1)
    circle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    circle.BorderSizePixel = 0
    circle.Parent = toggleBtn

    local ligado = false
    toggleBtn.MouseButton1Click:Connect(function()
        ligado = not ligado
        if ligado then
            toggleBtn.BackgroundColor3 = Color3.fromRGB(0, 170, 255)
            circle:TweenPosition(UDim2.new(0.6, 0, 0, 1), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.2, true)
        else
            toggleBtn.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
            circle:TweenPosition(UDim2.new(0, 1, 0, 1), Enum.EasingDirection.Out, Enum.EasingStyle.Quad, 0.2, true)
        end
    end)

    return function() return ligado end
end

-- Criar toggles
local AutoFarm = criarMaterialToggle("😈Auto-Farm", 0.05, 0.3)
local MultiRebirth = criarMaterialToggle("💺REB|STATUS", 0.05, 0.5)
local RebStats = criarMaterialToggle("🎇Auto-Transform", 0.05, 0.7)
local AutoRebirth = criarMaterialToggle("🥇atack 1", 0.55, 0.3)
local AutoCharge = criarMaterialToggle("☠️tp planeta", 0.55, 0.5)
local FarmTeleportToggle = criarMaterialToggle("💫multicast", 0.55, 0.7)

-- Garantir que o painel reapareça após a morte
LocalPlayer.CharacterAdded:Connect(function()
    painel.Visible = true
    barraFechada.Visible = false
end)
