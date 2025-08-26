--[!] Coloque este script em StarterGui como LocalScript

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- Configurações
local IMAGE_ID = "rbxassetid://88617760765364" -- Troque pelo seu ID de imagem
local SOUND_ID = "rbxassetid://1848354536" -- Troque pelo ID da música desejada
local LOADING_BAR_COLOR = Color3.fromRGB(255, 0, 0) -- Neon Vermelho
local LOADING_TIME = 17 -- Tempo de carregamento em segundos

-- Criar Blur
local blur = Instance.new("BlurEffect")
blur.Size = 24
blur.Parent = game:GetService("Lighting")

-- Criar Gui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "CustomLoadingScreen"
screenGui.Parent = player:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false
screenGui.IgnoreGuiInset = true -- Para ocupar toda tela

-- Música de fundo
local sound = Instance.new("Sound")
sound.SoundId = SOUND_ID
sound.Looped = true
sound.Volume = 0.5
sound.Parent = screenGui
sound:Play()

-- Container Centralizado (proporção adaptável)
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0.45, 0, 0.45, 0) -- 45% da tela, responsivo
mainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
mainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
mainFrame.BackgroundTransparency = 1
mainFrame.Parent = screenGui

local aspect = Instance.new("UIAspectRatioConstraint")
aspect.AspectRatio = 1
aspect.Parent = mainFrame

-- Imagem centralizada com fade in
local imageLabel = Instance.new("ImageLabel")
imageLabel.Size = UDim2.new(0.55, 0, 0.55, 0)
imageLabel.Position = UDim2.new(0.5, 0, 0.35, 0)
imageLabel.AnchorPoint = Vector2.new(0.5, 0.5)
imageLabel.Image = IMAGE_ID
imageLabel.BackgroundTransparency = 1
imageLabel.ImageTransparency = 1
imageLabel.Parent = mainFrame

-- Barra de carregamento neon centralizada
local barBg = Instance.new("Frame")
barBg.Size = UDim2.new(0.8, 0, 0.13, 0)
barBg.Position = UDim2.new(0.5, 0, 0.80, 0)
barBg.AnchorPoint = Vector2.new(0.5, 0.5)
barBg.BackgroundTransparency = 0.6
barBg.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
barBg.BorderSizePixel = 0
barBg.Parent = mainFrame

local uicorner = Instance.new("UICorner")
uicorner.CornerRadius = UDim.new(0, 12)
uicorner.Parent = barBg

local bar = Instance.new("Frame")
bar.Size = UDim2.new(0, 0, 1, 0)
bar.Position = UDim2.new(0, 0, 0, 0)
bar.BackgroundColor3 = LOADING_BAR_COLOR
bar.BorderSizePixel = 0
bar.Parent = barBg

local barCorner = Instance.new("UICorner")
barCorner.CornerRadius = UDim.new(0, 12)
barCorner.Parent = bar

local neon = Instance.new("UIStroke")
neon.Thickness = 4
neon.Color = LOADING_BAR_COLOR
neon.Transparency = 0.35
neon.Parent = bar

local percentLabel = Instance.new("TextLabel")
percentLabel.Size = UDim2.new(0.25, 0, 1, 0)
percentLabel.Position = UDim2.new(0.5, -0.125, 0, 0)
percentLabel.AnchorPoint = Vector2.new(0.5, 0.5)
percentLabel.BackgroundTransparency = 1
percentLabel.Text = "0%"
percentLabel.Font = Enum.Font.GothamBold
percentLabel.TextSize = 22
percentLabel.TextColor3 = LOADING_BAR_COLOR
percentLabel.Parent = barBg

-- Fade In da Imagem
TweenService:Create(imageLabel, TweenInfo.new(1, Enum.EasingStyle.Quad), {ImageTransparency = 0}):Play()

-- Animação da Barra de Carregamento
local function animateLoading()
    for i = 0, 100 do
        local percent = i / 100
        bar.Size = UDim2.new(percent, 0, 1, 0)
        percentLabel.Text = tostring(i) .. "%"
        neon.Transparency = 0.35 + 0.15 * math.abs(math.sin(i/10))
        bar.BackgroundColor3 = LOADING_BAR_COLOR:lerp(Color3.fromRGB(255,64,64), math.abs(math.sin(i/20)))
        wait(LOADING_TIME / 100)
    end
end

-- Fade Out animação
local function fadeOut()
    local fadeTween = TweenService:Create(mainFrame, TweenInfo.new(1, Enum.EasingStyle.Quad), {BackgroundTransparency = 1})
    local imageTween = TweenService:Create(imageLabel, TweenInfo.new(1, Enum.EasingStyle.Quad), {ImageTransparency = 1})
    local barTween = TweenService:Create(barBg, TweenInfo.new(1, Enum.EasingStyle.Quad), {BackgroundTransparency = 1})
    local barTween2 = TweenService:Create(bar, TweenInfo.new(1, Enum.EasingStyle.Quad), {BackgroundTransparency = 1})
    percentLabel.TextTransparency = 1

    fadeTween:Play()
    imageTween:Play()
    barTween:Play()
    barTween2:Play()

    imageTween.Completed:Wait()
    mainFrame.Visible = false
    blur:Destroy()
    sound:Destroy()
    screenGui:Destroy()
end

-- Executar animações
animateLoading()
fadeOut()

-- Executar Infinite Yield (pós-carregamento)
loadstring(game:HttpGet("https://raw.githubusercontent.com/Lucasgbw/Script-pixel-hub-brookhaven-/refs/heads/main/README.md"))()
