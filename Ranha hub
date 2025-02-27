-- Tenta carregar a biblioteca de forma segura
local success, Library = pcall(function()
    return loadstring(game:HttpGet("https://raw.githubusercontent.com/hacked-prototype/RedzLibV4/main/Source.lua"))()
end)

-- Verifica se houve erro ao carregar a biblioteca
if not success or not Library then
    warn("Falha ao carregar a biblioteca. Verifique a URL ou a disponibilidade do script.")
    return
end

-- Define o tema, se disponÃƒÂ­vel
if Library.SetTheme then
    Library:SetTheme("Dark")  -- Escolha um tema vÃƒÂ¡lido como "Dark" ou "Light"
end

-- Ajusta a transparÃƒÂªncia
if Library.SetTransparency then
    Library:SetTransparency(0.1)
end

-- Criando a janela principal
local Window
if Library.MakeWindow then
    Window = Library:MakeWindow({
        Title = "REDz HUB",
        SubTitle = "by: redz9999",
        LoadText = "Carregando...",
        Flags = "redzHub_Example"
    })
end

-- VariÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â¡veis de controle
local teleporting = false
local flingEnabled = false
local viewEnabled = false
local selectedPlayer = nil
local flingSpeed = 9000  -- Aumentando a velocidade para um Fling mais forte

-- FunÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â§ÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o para teleporte contÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â­nuo
local function startTeleport()
    teleporting = true
    while teleporting do
        task.wait(0.05)

        local targetCharacter = selectedPlayer.Character
        if not targetCharacter then
            teleporting = false
            OrionLib:MakeNotification({
                Name = "Erro",
                Content = "Jogador invÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â¡lido ou nÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o carregado!",
                Time = 3
            })
            return
        end

        local targetHRP = targetCharacter:FindFirstChild("HumanoidRootPart")
        if not targetHRP then
            teleporting = false
            OrionLib:MakeNotification({
                Name = "Erro",
                Content = "HumanoidRootPart nÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o encontrado!",
                Time = 3
            })
            return
        end

        -- Teleporte contÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â­nuo
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetHRP.CFrame

        -- Aplica Fling mais forte se estiver ativado
        if flingEnabled then
            game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(
                math.random(-flingSpeed, flingSpeed), 
                flingSpeed * 2,  -- Dando um impulso mais forte no eixo Y
                math.random(-flingSpeed, flingSpeed)
            )
            game.Players.LocalPlayer.Character.HumanoidRootPart.RotVelocity = Vector3.new(flingSpeed * 1.5, flingSpeed * 1.5, flingSpeed * 1.5)  -- Maior rotaÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â§ÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o
        end
    end
end

-- FunÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â§ÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o para parar o teleporte
local function stopTeleport()
    teleporting = false
end

-- FunÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â§ÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o para atualizar a lista de jogadores
local function updatePlayerList()
    local playerNames = {}
    for _, player in ipairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            table.insert(playerNames, player.Name)
        end
    end
    return playerNames
end

-- FunÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â§ÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o para ativar/desativar o View
local function enableView(targetPlayer)
    if not targetPlayer or not targetPlayer.Character then return end

    local camera = workspace.CurrentCamera
    camera.CameraSubject = targetPlayer.Character:FindFirstChild("Humanoid") or targetPlayer.Character
    camera.CameraType = Enum.CameraType.Custom
end

local function disableView()
    local camera = workspace.CurrentCamera
    camera.CameraSubject = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
    camera.CameraType = Enum.CameraType.Custom
end

-- Reconectar View apÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â³s morte
game.Players.LocalPlayer.CharacterAdded:Connect(function()
    if viewEnabled and selectedPlayer then
        enableView(selectedPlayer)
    end
end)

-- Criar a aba "Fling"
local FlingTab = Window:MakeTab({
    Name = "Flingar ",
    Icon = "rbxassetid://109334249980199",
    PremiumOnly = false
})

-- Dropdown de SeleÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â§ÃƒÆ’Ã†â€™Ãƒâ€ Ã¢â‚¬â„¢ÃƒÆ’Ã¢â‚¬Å¡Ãƒâ€šÃ‚Â£o de Jogador
local dropdown = FlingTab:AddDropdown({
    Name = "Selecionar Jogador",
    Default = "",
    Options = updatePlayerList(),
    Callback = function(value)
        selectedPlayer = game.Players:FindFirstChild(value)
    end
})

-- Atualizar lista de jogadores
FlingTab:AddButton({
    Name = "Atualizar Lista de Jogadores",
    Callback = function()
        dropdown:Refresh(updatePlayerList(), true)
        OrionLib:MakeNotification({
            Name = "Lista Atualizada",
            Content = "Jogadores atualizados com sucesso!",
            Time = 3
        })
    end
})

-- Alternador para Iniciar/Parar o Fling
FlingTab:AddToggle({
    Name = "Iniciar Fling",
    Default = false,
    Callback = function(value)
        flingEnabled = value
        if flingEnabled then
            startTeleport()
        else
            stopTeleport()
        end
    end
})

-- Alternador para Ativar/Desativar o View
FlingTab:AddToggle({
    Name = "View Jogador",
    Default = false,
    Callback = function(value)
        viewEnabled = value
        if viewEnabled then
            enableView(selectedPlayer)
        else
            disableView()
        end
    end
})



local Tab = Window:MakeTab({
	Name = "pegar sofa",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]

Tab:AddButton({
	Name = "sofÃƒÂ¡",
	Callback = function()
	local args = {
    [1] = "PickingTools",
    [2] = "Couch"
}
 
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
