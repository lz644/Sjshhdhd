# Sjshhdhd
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRoot = character:WaitForChild("HumanoidRootPart")
local base = workspace:WaitForChild("Base")

-- Criar um BodyVelocity para simular voo
local bodyVelocity = Instance.new("BodyVelocity")
bodyVelocity.MaxForce = Vector3.new(1e5, 1e5, 1e5)
bodyVelocity.Velocity = Vector3.new(0, 50, 0) -- Sobe primeiro
bodyVelocity.Parent = humanoidRoot

-- Espera 1 segundo e depois começa a ir para a base
task.wait(1)

-- Voa até a base
local function voarAteBase()
	while (humanoidRoot.Position - base.Position).Magnitude > 5 do
		local direcao = (base.Position - humanoidRoot.Position).Unit
		bodyVelocity.Velocity = direcao * 100 -- velocidade
		task.wait(0.1)
	end

	-- Quando chegar, para o voo
	bodyVelocity:Destroy()

	-- Efeito visual (opcional)
	game.StarterGui:SetCore("ChatMakeSystemMessage", {
		Text = "Você chegou com o Brainrot na base!";
		Color = Color3.new(0, 1, 0);
	})

	-- Kick ou vitória, por exemplo
	-- player:Kick("Você venceu com o Brainrot!")
end

voarAteBase()
local player = game.Players.LocalPlayer
local button = script.Parent
local frame = button.Parent
local fugirButton = frame:WaitForChild("escapar")

-- Quando clicar no botão Roubar
button.MouseButton1Click:Connect(function()
    print(player.Name .. " Teste 01") -- Apenas exemplo
    button.Visible = false
    fugirButton.Visible = true

    -- Dá ponto ao jogador (opcional, depende do seu sistema)
    local stats = player:FindFirstChild("leaderstats")
    if stats then
        local pontos = stats:FindFirstChild("Pontos")
        if pontos then
            pontos.Value = pontos.Value + 1
        end
    end
end)
