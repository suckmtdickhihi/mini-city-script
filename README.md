-- Script Simples de Auto-Coleta e Auto-Revista (para testes)
-- Aviso: uso indevido pode violar os termos de uso do Roblox. Use apenas com permissão no ambiente de testes.

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Loop para coletar itens automaticamente
spawn(function()
    while true do
        wait(1) -- Intervalo de verificação

        for _, item in pairs(workspace:GetChildren()) do
            if item:IsA("Model") and item:FindFirstChild("TouchTrigger") and item.Name == "Coletavel" then
                -- Move até o item
                humanoidRootPart.CFrame = item.TouchTrigger.CFrame + Vector3.new(0, 3, 0)
                wait(0.5) -- Tempo para "coletar"
            end
        end
    end
end)

-- Loop para revistar jogadores próximos automaticamente
spawn(function()
    while true do
        wait(2) -- Intervalo de verificação

        for _, otherPlayer in pairs(game.Players:GetPlayers()) do
            if otherPlayer ~= player and otherPlayer.Character and otherPlayer.Character:FindFirstChild("HumanoidRootPart") then
                local distance = (otherPlayer.Character.HumanoidRootPart.Position - humanoidRootPart.Position).magnitude
                if distance < 10 then -- Distância para "revistar"
                    print("Revistando:", otherPlayer.Name)
                    -- Aqui você pode simular a revista, como abrir um inventário, por exemplo
                end
            end
        end
    end
end)
