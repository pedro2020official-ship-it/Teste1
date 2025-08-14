-- 📜 PEDRO SCRIPTS - Mod Menu com Key System
-- Chave obrigatória: Pedroscripts

-- Serviços
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:FindFirstChild("PlayerGui") or Instance.new("PlayerGui", LocalPlayer)

-- Criar GUI principal
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "PedroScriptsMenu"
screenGui.Parent = PlayerGui
screenGui.ResetOnSpawn = false

-- 🔐 Tela de chave
local keyFrame = Instance.new("Frame")
keyFrame.Size = UDim2.new(0, 300, 0, 150)
keyFrame.Position = UDim2.new(0.5, -150, 0.5, -75)
keyFrame.BackgroundColor3 = Color3.fromRGB(0, 102, 204)
keyFrame.BorderSizePixel = 2
keyFrame.Active = true
keyFrame.Draggable = true
keyFrame.Parent = screenGui

local keyTitle = Instance.new("TextLabel")
keyTitle.Size = UDim2.new(1, 0, 0, 30)
keyTitle.Text = "🔑 Digite a chave"
keyTitle.TextSize = 18
keyTitle.Font = Enum.Font.SourceSansBold
keyTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
keyTitle.BackgroundTransparency = 1
keyTitle.Parent = keyFrame

local keyBox = Instance.new("TextBox")
keyBox.Size = UDim2.new(1, -20, 0, 35)
keyBox.Position = UDim2.new(0, 10, 0, 50)
keyBox.PlaceholderText = "Digite aqui..."
keyBox.Text = ""
keyBox.TextSize = 16
keyBox.Font = Enum.Font.SourceSans
keyBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
keyBox.TextColor3 = Color3.fromRGB(0, 0, 0)
keyBox.Parent = keyFrame

local submitKey = Instance.new("TextButton")
submitKey.Size = UDim2.new(1, -20, 0, 35)
submitKey.Position = UDim2.new(0, 10, 0, 100)
submitKey.Text = "Verificar"
submitKey.TextSize = 16
submitKey.Font = Enum.Font.SourceSansBold
submitKey.BackgroundColor3 = Color3.fromRGB(0, 153, 255)
submitKey.TextColor3 = Color3.fromRGB(255, 255, 255)
submitKey.Parent = keyFrame

-- 📦 Função para criar menu após chave correta
local function createMenu()
    -- Frame principal
    local mainFrame = Instance.new("Frame")
    mainFrame.Size = UDim2.new(0, 250, 0, 200)
    mainFrame.Position = UDim2.new(0.3, 0, 0.3, 0)
    mainFrame.BackgroundColor3 = Color3.fromRGB(0, 102, 204)
    mainFrame.BorderSizePixel = 2
    mainFrame.Visible = true
    mainFrame.Active = true
    mainFrame.Draggable = true
    mainFrame.Parent = screenGui

    -- Título
    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, -40, 0, 25)
    title.Position = UDim2.new(0, 5, 0, 0)
    title.Text = "Pedro Scripts"
    title.TextColor3 = Color3.fromRGB(255, 255, 255)
    title.BackgroundTransparency = 1
    title.TextSize = 18
    title.Font = Enum.Font.SourceSansBold
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.Parent = mainFrame

    -- Botão Abrir/Fechar
    local toggleButton = Instance.new("TextButton")
    toggleButton.Size = UDim2.new(0, 35, 0, 25)
    toggleButton.Position = UDim2.new(1, -40, 0, 0)
    toggleButton.Text = "-"
    toggleButton.TextSize = 18
    toggleButton.Font = Enum.Font.SourceSansBold
    toggleButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
    toggleButton.Parent = mainFrame

    -- Área de rolagem
    local scrollingFrame = Instance.new("ScrollingFrame")
    scrollingFrame.Size = UDim2.new(1, -10, 1, -35)
    scrollingFrame.Position = UDim2.new(0, 5, 0, 30)
    scrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
    scrollingFrame.ScrollBarThickness = 6
    scrollingFrame.BackgroundTransparency = 1
    scrollingFrame.Parent = mainFrame

    -- Função para criar botões
    local function createButton(name, callback)
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(1, -10, 0, 35)
        btn.BackgroundColor3 = Color3.fromRGB(0, 153, 255)
        btn.TextColor3 = Color3.fromRGB(255, 255, 255)
        btn.Font = Enum.Font.SourceSansBold
        btn.TextSize = 16
        btn.Text = name
        btn.Parent = scrollingFrame
        btn.MouseButton1Click:Connect(callback)
        return btn
    end

    -- Botões de scripts
    local script1 = createButton("Lennon v1", function()
        loadstring(game:HttpGet("https://pastefy.app/3R6JfM1r/raw"))()
    end)

    local script2 = createButton("Lennon v2", function()
        loadstring(game:HttpGet("https://pastefy.app/1FPEhJmq/raw"))()
    end)

    local script3 = createButton("Chilli", function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/tienkhanh1/spicy/main/Chilli.lua"))()
    end)

    -- Posicionar botões
    local buttons = {script1, script2, script3}
    for i, btn in ipairs(buttons) do
        btn.Position = UDim2.new(0, 5, 0, (i - 1) * 40)
    end
    scrollingFrame.CanvasSize = UDim2.new(0, 0, 0, #buttons * 40)

    -- Abrir/Fechar menu
    local isOpen = true
    toggleButton.MouseButton1Click:Connect(function()
        isOpen = not isOpen
        scrollingFrame.Visible = isOpen
        toggleButton.Text = isOpen and "-" or "+"
    end)
end

-- 🔐 Verificação de chave
submitKey.MouseButton1Click:Connect(function()
    if keyBox.Text == "Pedroscripts" then
        keyFrame:Destroy()
        createMenu()
    else
        keyBox.Text = ""
        keyBox.PlaceholderText = "Chave incorreta!"
    end
end)
