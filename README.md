
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()
local Window = OrionLib:MakeWindow({
    Name = "♧BITCH8711♧ HUB (by bitch/by anthony) {brookhaven rp}", 
    HidePremium = false, 
    SaveConfig = true, 
    ConfigFolder = "OrionTest"
})
local Tab = Window:MakeTab({
    Name = "boat fling",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})
local Players = game:GetService("Players")
local playerNames = {}
for _, player in pairs(Players:GetPlayers()) do
    table.insert(playerNames, player.Name)
end

local selectedPlayerName = nil

Tab:AddDropdown({
    Name = "jogadores!",
    Options = playerNames,
    Callback = function(selected)
        selectedPlayerName = selected
    end
})

Tab:AddButton({
    Name = " fling boat",
    Callback = function()
        if selectedPlayerName then
            local selectedPlayer = game.Players:FindFirstChild(selectedPlayerName)
            if selectedPlayer then
                local Player = game.Players.LocalPlayer
                local Character = Player.Character
                local Humanoid = Character and Character:FindFirstChildOfClass("Humanoid")
                local RootPart = Character and Character:FindFirstChild("HumanoidRootPart")
                local Vehicles = game.Workspace:FindFirstChild("Vehicles")
                local OldPos = RootPart and RootPart.CFrame

                if RootPart and Vehicles then
                    local PCar = Vehicles:FindFirstChild(Player.Name.."Car")
                    if not PCar then
                        RootPart.CFrame = CFrame.new(-3, -4, 2105)
                        task.wait(0.5)
                        game:GetService("ReplicatedStorage").RE["1Ca1r"]:FireServer("PickingBoat", "MilitaryBoatFree")
                        task.wait(0.5)
                        PCar = Vehicles:FindFirstChild(Player.Name.."Car")

                        if PCar then
                            local Seat = PCar:FindFirstChild("Body") and PCar.Body:FindFirstChild("VehicleSeat")
                            if Seat then
                                repeat
                                    task.wait()
                                    RootPart.CFrame = Seat.CFrame * CFrame.new(0, 2, 0)
                                until Humanoid and Humanoid.Sit
                            end
                        end
                    end

                    local TargetC = selectedPlayer.Character
                    local TargetH = TargetC and TargetC:FindFirstChildOfClass("Humanoid")
                    local TargetRP = TargetC and TargetC:FindFirstChild("HumanoidRootPart")

                    if PCar and TargetC and TargetH and TargetRP then
                        if not TargetH.Sit then
                            while not TargetH.Sit do
                                task.wait()
                                PCar:SetPrimaryPartCFrame(TargetRP.CFrame * CFrame.new(0, -2, 0))
                            end
                            task.wait(0.1)

                            local AngularVelocity = Instance.new("BodyAngularVelocity")
                            AngularVelocity.AngularVelocity = Vector3.new(70, 0, 0)
                            AngularVelocity.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
                            AngularVelocity.Parent = PCar.PrimaryPart

                            task.wait(1)

                            local launchDirection = Vector3.new(math.random(-1, 1), 1, math.random(-1, 1)).unit * 50
                            local BodyVelocity = Instance.new("BodyVelocity")
                            BodyVelocity.Velocity = launchDirection
                            BodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                            BodyVelocity.Parent = PCar.PrimaryPart

                            task.wait(0.5)
                            BodyVelocity:Destroy()
                            AngularVelocity:Destroy()

                            if Humanoid then Humanoid.Sit = false end
                            task.wait(0.1)
                            if RootPart then RootPart.CFrame = OldPos end
                        end
                    end
                end
            else
                print("tu tento pega um jogador que kitou ou que ta bugado")
            end
        else
            print("seleciona um jogador filho da puta animal")
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
	Name = "sofa",
	Callback = function()
	local args = {
    [1] = "PickingTools",
    [2] = "Couch"
}
 
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
      		print("button pressed")
  	end    
})

local Tab = Window:MakeTab({
    Name = "Casas",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local a = 0

Tab:AddTextbox({
    Name = "Numero",
    Default = "0 ",
    TextDisappear = true,
    Callback = function(Value)
        a = tonumber(Value) or 0  -- Converte o valor para nÃƒÂºmero ou define como 0 se nÃƒÂ£o for um nÃƒÂºmero vÃƒÂ¡lido
    end      
})

Tab:AddButton({
    Name = "pegar permissao!",
    Callback = function()
        local args = {
            "GivePermissionLoopToServer",
            game.Players.LocalPlayer,
            a
        }

        game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))
    end    
})

local Tab = Window:MakeTab({
	Name = "Scripts universais",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]

Tab:AddButton({
	Name = "infinite",
	Callback = function()
	loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
      		print("button pressed")
  	end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]


Tab:AddButton({
	Name = "Nameles Loopfling",
	Callback = function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/FilteringEnabled/NamelessAdmin/main/Source"))()
      		print("button pressed")
  	end  
  
})Tab:AddButton({
	Name = "fly v3",
	Callback = function()
	loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-v3-7412"))()
      		print("button pressed")
  	end 
  })
 
 Tab:AddButton({
	Name = "cleitin hub",
	Callback = function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/CLEITI6966/teste/refs/heads/main/scriptdebosta.lua"))()
      		print("button pressed")
  	end 
  })

-- Iniciar a interface
OrionLib:Init()

-- VariÃƒÂ¡veis de controle
local teleporting = false
local flingEnabled = false
local viewEnabled = false
local selectedPlayer = nil
local flingSpeed = 9000  -- Aumentando a velocidade para um Fling mais forte

-- FunÃƒÂ§ÃƒÂ£o para teleporte contÃƒÂ­nuo
local function startTeleport()
    teleporting = true
    while teleporting do
        task.wait(0.05)

        local targetCharacter = selectedPlayer.Character
        if not targetCharacter then
            teleporting = false
            OrionLib:MakeNotification({
                Name = "Erro",
                Content = "Jogador invÃƒÂ¡lido ou nÃƒÂ£o carregado!",
                Time = 3
            })
            return
        end

        local targetHRP = targetCharacter:FindFirstChild("HumanoidRootPart")
        if not targetHRP then
            teleporting = false
            OrionLib:MakeNotification({
                Name = "Erro",
                Content = "HumanoidRootPart nÃƒÂ£o encontrado!",
                Time = 3
            })
            return
        end

        -- Teleporte contÃƒÂ­nuo
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = targetHRP.CFrame

        -- Aplica Fling mais forte se estiver ativado
        if flingEnabled then
            game.Players.LocalPlayer.Character.HumanoidRootPart.Velocity = Vector3.new(
                math.random(-flingSpeed, flingSpeed), 
                flingSpeed * 2,  -- Dando um impulso mais forte no eixo Y
                math.random(-flingSpeed, flingSpeed)
            )
            game.Players.LocalPlayer.Character.HumanoidRootPart.RotVelocity = Vector3.new(flingSpeed * 1.5, flingSpeed * 1.5, flingSpeed * 1.5)  -- Maior rotaÃƒÂ§ÃƒÂ£o
        end
    end
end

-- FunÃƒÂ§ÃƒÂ£o para parar o teleporte
local function stopTeleport()
    teleporting = false
end

-- FunÃƒÂ§ÃƒÂ£o para atualizar a lista de jogadores
local function updatePlayerList()
    local playerNames = {}
    for _, player in ipairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            table.insert(playerNames, player.Name)
        end
    end
    return playerNames
end

-- FunÃƒÂ§ÃƒÂ£o para ativar/desativar o View
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

-- Reconectar View apÃƒÂ³s morte
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

-- Dropdown de SeleÃƒÂ§ÃƒÂ£o de Jogador
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
    Name = "botao extra!",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Tab = Window:MakeTab({
    Name = "botao extra!",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Tab = Window:MakeTab({
    Name = "botao extra!",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Tab = Window:MakeTab({
    Name = "botao extra!",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local Tab = Window:MakeTab({
    Name = "car fling (test)",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})
local Players = game:GetService("Players")
local playerNames = {}
for _, player in pairs(Players:GetPlayers()) do
    table.insert(playerNames, player.Name)
end

local selectedPlayerName = nil

Tab:AddDropdown({
    Name = "jogadores!",
    Options = playerNames,
    Callback = function(selected)
        selectedPlayerName = selected
    end
})

Tab:AddButton({
    Name = " kill",
    Callback = function()
        if selectedPlayerName then
            local selectedPlayer = game.Players:FindFirstChild(selectedPlayerName)
            if selectedPlayer then
                local Player = game.Players.LocalPlayer
                local Character = Player.Character
                local Humanoid = Character and Character:FindFirstChildOfClass("Humanoid")
                local RootPart = Character and Character:FindFirstChild("HumanoidRootPart")
                local Vehicles = game.Workspace:FindFirstChild("Vehicles")
                local OldPos = RootPart and RootPart.CFrame

                if RootPart and Vehicles then
                    local PCar = Vehicles:FindFirstChild(Player.Name.."Car")
                    if not PCar then
                        RootPart.CFrame = CFrame.new(-3, -4, 2105)
                        task.wait(0.5)
                        game:GetService("ReplicatedStorage").RE["1Ca1r"]:FireServer("Pickingcar", "carpurbleFree")
                        task.wait(0.5)
                        PCar = Vehicles:FindFirstChild(Player.Name.."Car")

                        if PCar then
                            local Seat = PCar:FindFirstChild("Body") and PCar.Body:FindFirstChild("VehicleSeat")
                            if Seat then
                                repeat
                                    task.wait()
                                    RootPart.CFrame = Seat.CFrame * CFrame.new(0, 2, 0)
                                until Humanoid and Humanoid.Sit
                            end
                        end
                    end

                    local TargetC = selectedPlayer.Character
                    local TargetH = TargetC and TargetC:FindFirstChildOfClass("Humanoid")
                    local TargetRP = TargetC and TargetC:FindFirstChild("HumanoidRootPart")

                    if PCar and TargetC and TargetH and TargetRP then
                        if not TargetH.Sit then
                            while not TargetH.Sit do
                                task.wait()
                                PCar:SetPrimaryPartCFrame(TargetRP.CFrame * CFrame.new(0, -2, 0))
                            end
                            task.wait(0.1)

                            local AngularVelocity = Instance.new("BodyAngularVelocity")
                            AngularVelocity.AngularVelocity = Vector3.new(70, 0, 0)
                            AngularVelocity.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
                            AngularVelocity.Parent = PCar.PrimaryPart

                            task.wait(1)

                            local launchDirection = Vector3.new(math.random(-1, 1), 1, math.random(-1, 1)).unit * 50
                            local BodyVelocity = Instance.new("BodyVelocity")
                            BodyVelocity.Velocity = launchDirection
                            BodyVelocity.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
                            BodyVelocity.Parent = PCar.PrimaryPart

                            task.wait(0.5)
                            BodyVelocity:Destroy()
                            AngularVelocity:Destroy()

                            if Humanoid then Humanoid.Sit = false end
                            task.wait(0.1)
                            if RootPart then RootPart.CFrame = OldPos end
                        end
                    end
                end
            else
                print("tu tento pega um jogador que kitou ou que ta bugado")
            end
        else
            print("seleciona um jogador filho da puta animal")
        end
    end
})

-- Criando aba "Lag"
LagTab local = Janela:CriarTab({
    Nome = "Atraso",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Tabela de alternâncias
alternâncias locais = {
    DupeBook = falso,
    DupeStretcher = falso
}

-- Função para clicar em objetos com ClickDetector
função local clickNormalmente(objeto)
    local clickDetector = objeto:FindFirstChildWhichIsA("ClickDetector")
    se clickDetector então
        detector de clique de fogo(clickDetector)
    fim
fim

-- Função para duplicar itens
função local dupeItem(itemPath, maxTeleports)
    se itemPath então
        teletransporte localCount = 0
        enquanto teleportCount < maxTeleports e toggles.DupeBook do
            se game.Players.LocalPlayer e game.Players.LocalPlayer.Character e game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") então
                jogo.Jogadores.JogadorLocal.Personagem.ParteRaizHumanoide.CFrame = caminhodoitem.CFrame
                cliqueNormalmente(itemPath)
                teleportCount = teleportCount + 1
                wait(0.01) -- Tempo de espera para evitar travamentos
            outro
                warning("Personagem do jogador não encontrada.")
                quebrar
            fim
        fim
    outro
        warn("ItemPath inválido.")
    fim
fim

-- Alternar para duplicar o livro
LagTab:AdicionarAlternar({
    Nome = "Livro Dupe",
    Padrão = falso,
    Retorno de chamada = função(estado)
        alterna.DupeBook = estado
        se estado então
            local bookPath = espaço de trabalho:FindFirstChild("WorkspaceCom")
                e espaço de trabalho.WorkspaceCom:FindFirstChild("001_DayCare")
                e espaço de trabalho.WorkspaceCom["001_DayCare"]:FindFirstChild("Ferramentas")
                e espaço de trabalho.WorkspaceCom["001_DayCare"].Tools:FindFirstChild("Livro")

            se bookPath então
                gerar(função()
                    dupeItem(bookPath, 9999999999999999999999999999999999999)
                fim)
            outro
                warning("Livro não encontrado.")
            fim
        outro
            print("Livro Duplicado desligar.")
        fim
    fim
})

-- Função para duplicar a maca
função local dupeStretcher()
    local stretcherPath = espaço de trabalho:FindFirstChild("WorkspaceCom")
        e espaço de trabalho.WorkspaceCom:FindFirstChild("001_GiveTools")
        e espaço de trabalho.WorkspaceCom["001_GiveTools"]:FindFirstChild("Maca")

    se stretcherPath então
        dupeItem(caminhodamaca, 9 ...
    outro
        warning("Item Maca não encontrado.")
    fim
fim

-- Alternar para duplicar uma maca
LagTab:AdicionarAlternar({
    Nome = "Dupe Stretcher",
    Padrão = falso,
    Retorno de chamada = função(estado)
        alterna.DupeStretcher = estado
        se estado então
            spawn(dupeStretcher)
        outro
            print("Dupe Maca desligada.")
        fim
    fim
})

OrionLib:Init()
