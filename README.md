local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "MATRIX HUB v1.4🎩", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

--[[
Name = <MATRIX HUB v1.4🎩> - The name of the UI.
HidePremium = <bool> - Whether or not the user details shows Premium status or not.
SaveConfig = <bool> - Toggles the config saving in the UI.
ConfigFolder = <PBhubconfigs> - The name of the folder where the configs are saved.
IntroEnabled = <true> - Whether or not to show the intro animation.
IntroText = <TEAM CARTOLA CENTER> - Text to show in the intro animation.
IntroIcon = <string> - URL to the image you want to use in the intro animation.
Icon = <rbxassetid://17802167990> - URL to the image you want displayed on the window.
CloseCallback = <function> - Function to execute when the window is closed.
]]


-- By Conta Teste local textura = "" -- Exemplo: rbxassetid://asset_id local nomeBotao = "BotaoArrastavel" local playerGui = game.Players.LocalPlayer:WaitForChild("PlayerGui") if playerGui:FindFirstChild("BotaoMovel") and playerGui.BotaoMovel:FindFirstChild(nomeBotao) then 	return end local ScreenGui = Instance.new("ScreenGui") ScreenGui.ResetOnSpawn = false ScreenGui.Name = "BotaoMovel" ScreenGui.Parent = playerGui local Botao = Instance.new("ImageButton") Botao.Size = UDim2.new(0, 50, 0, 50) Botao.Position = UDim2.new(0, 0, 0.454706937, 0) Botao.AutoButtonColor = true Botao.BorderSizePixel = 0 Botao.Name = nomeBotao Botao.Parent = ScreenGui local UICorner = Instance.new("UICorner", Botao) UICorner.CornerRadius = UDim.new(0, 12) if textura == "" then 	Botao.BackgroundColor3 = Color3.fromRGB(255, 255, 255) 	Botao.BackgroundTransparency = 0 	Botao.Image = "" else 	Botao.BackgroundTransparency = 0 	Botao.Image = textura 	Botao.ScaleType = Enum.ScaleType.Stretch end local UserInputService = game:GetService("UserInputService") local dragging = false local dragInput, dragStart, startPos Botao.InputBegan:Connect(function(input) 	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then 		dragging = true 		dragStart = input.Position 		startPos = Botao.Position 		input.Changed:Connect(function() 			if input.UserInputState == Enum.UserInputState.End then 				dragging = false 			end 		end) 	end end) Botao.InputChanged:Connect(function(input) 	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then 		dragInput = input 	end end) UserInputService.InputChanged:Connect(function(input) 	if input == dragInput and dragging then 		local delta = input.Position - dragStart 		Botao.Position = UDim2.new( 			startPos.X.Scale, 			startPos.X.Offset + delta.X, 			startPos.Y.Scale, 			startPos.Y.Offset + delta.Y 		) 	end end) local VirtualInputManager = game:GetService("VirtualInputManager") Botao.MouseButton1Click:Connect(function() 	VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.LeftControl, false, game) end)

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
    Default = "11",
    TextDisappear = true,
    Callback = function(Value)
        a = tonumber(Value) or 0  -- Converte o valor para nÃƒÂºmero ou define como 0 se nÃƒÂ£o for um nÃƒÂºmero vÃƒÂ¡lido
    end      
})

Tab:AddButton({
    Name = "pegar permissao",
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
	Name = "infinite yield",
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


local Tab = Window:MakeTab({ Name = "audio FE", Icon = "rbxassetid://4483345998", PremiumOnly = false })Tab:AddButton({ Name = "BOOMBOX", Callback = function() -- Criando a GUI principal local ScreenGui = Instance.new("ScreenGui") ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui") ScreenGui.Enabled = false -- Inicialmente o Frame estarÃƒÂ¡ invisÃƒÂ­vel

-- Criando o frame local Frame = Instance.new("Frame") Frame.Parent = ScreenGui Frame.Size = UDim2.new(0, 400, 0, 200) Frame.Position = UDim2.new(0.5, -200, 0.5, -100) Frame.AnchorPoint = Vector2.new(0.5, 0.5) Frame.BackgroundColor3 = Color3.new(0, 0, 0) Frame.BackgroundTransparency = 0.3 Frame.BorderSizePixel = 0

-- Adicionando cantos arredondados ao Frame local UICornerFrame = Instance.new("UICorner") UICornerFrame.Parent = Frame UICornerFrame.CornerRadius = UDim.new(0, 15)

-- Criando o texto explicativo local Label = Instance.new("TextLabel") Label.Parent = Frame Label.Size = UDim2.new(1, 0, 0.4, 0) Label.Position = UDim2.new(0, 0, 0, 0) Label.Text = "Put in the ID of a sound to play" Label.TextScaled = true Label.TextColor3 = Color3.new(1, 1, 1) Label.BackgroundTransparency = 1 Label.Font = Enum.Font.SciFi

-- Criando a TextBox local TextBox = Instance.new("TextBox") TextBox.Parent = Frame TextBox.Size = UDim2.new(0.8, 0, 0.2, 0) TextBox.Position = UDim2.new(0.1, 0, 0.5, 0) TextBox.PlaceholderText = "Enter ID" TextBox.Text = "" TextBox.TextScaled = true TextBox.TextColor3 = Color3.new(1, 1, 1) TextBox.BackgroundColor3 = Color3.new(0, 0, 0) TextBox.Font = Enum.Font.SciFi TextBox.BorderSizePixel = 0

-- Adicionando cantos arredondados Ãƒ TextBox local UICornerTextBox = Instance.new("UICorner") UICornerTextBox.Parent = TextBox UICornerTextBox.CornerRadius = UDim.new(0, 8)

-- Criando o botÃƒÂ£o local Button = Instance.new("TextButton") Button.Parent = Frame Button.Size = UDim2.new(0.4, 0, 0.2, 0) Button.Position = UDim2.new(0.3, 0, 0.75, 0) Button.Text = "Play" Button.TextScaled = true Button.TextColor3 = Color3.new(1, 1, 1) Button.BackgroundColor3 = Color3.new(0, 0, 0) Button.Font = Enum.Font.SciFi Button.BorderSizePixel = 0

-- Adicionando cantos arredondados ao botÃƒÂ£o local UICornerButton = Instance.new("UICorner") UICornerButton.Parent = Button UICornerButton.CornerRadius = UDim.new(0, 8)

-- VariÃƒÂ¡vel para armazenar o som em reproduÃƒÂ§ÃƒÂ£o local currentSound

-- FunÃƒÂ§ÃƒÂ£o para tocar o som localmente local function playSoundLocally(audioID) local character = game.Players.LocalPlayer.Character if character and character:FindFirstChild("Head") then -- Verifica se jÃƒÂ¡ hÃƒÂ¡ um som sendo tocado e o interrompe if currentSound then currentSound:Stop() currentSound:Destroy() currentSound = nil end

-- Cria e toca um novo som currentSound = Instance.new("Sound") currentSound.Parent = character.Head currentSound.SoundId = "rbxassetid://" .. audioID currentSound.Volume = 1 currentSound:Play() -- Parar o som apÃƒÂ³s 3 segundos task.delay(3, function() if currentSound then currentSound:Stop() currentSound:Destroy() currentSound = nil end end) currentSound.Ended:Connect(function() if currentSound then currentSound:Destroy() currentSound = nil end end) else warn("NÃƒÂ£o foi possÃƒÂ­vel encontrar a cabeÃƒÂ§a do personagem para tocar o som!") end 

end

-- FunÃƒÂ§ÃƒÂ£o para enviar o ÃƒÂ¡udio com o ID Button.MouseButton1Click:Connect(function() local audioID = tonumber(TextBox.Text) if audioID then -- Envia o som para o servidor local args = { [1] = game:GetService("Players").LocalPlayer.Character.Taser.Handle, [2] = audioID, [3] = 0.95 } game:GetService("ReplicatedStorage").RE:FindFirstChild("1Gu1nSound1s"):FireServer(unpack(args))

-- Toca o som localmente playSoundLocally(audioID) else warn("Por favor, insira um ID vÃƒÂ¡lido!") end 

end)

-- FunÃƒÂ§ÃƒÂ£o para verificar o item "Taser" e controlar o Frame local function checkForTaser() local taserDetected = false

while true do local character = game.Players.LocalPlayer.Character local taser = character and character:FindFirstChild("Taser") if taser then if not taserDetected then taserDetected = true ScreenGui.Enabled = true -- Modificar a "GripPos" do "Taser" taser.GripPos = Vector3.new(0, 0, -2) -- Executa o cÃƒÂ³digo de "wear" ao equipar o Taser local args = { [1] = "wear", [2] = 18756289999 } game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args)) end elseif taserDetected then taserDetected = false ScreenGui.Enabled = false -- Executa o cÃƒÂ³digo de "wear" novamente quando o Taser for desequipado local args = { [1] = "wear", [2] = 18756289999 } game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args)) -- Interrompe o som se o Taser for retirado if currentSound then currentSound:Stop() currentSound:Destroy() currentSound = nil end end wait(0.1) -- Verifica a cada 0.1 segundos end 

end

-- Inicia a verificaÃƒÂ§ÃƒÂ£o do item em paralelo spawn(checkForTaser)

-- Ativando a GUI automaticamente ScreenGui.Enabled = true print("button pressed") end
})

