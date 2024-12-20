-- Define los puntos opuestos de la Region3
local region = Region3.new(Vector3.new(10, 5, -20), Vector3.new(30, 15, 0)) -- Cambia las coordenadas

-- Encuentra el sonido en el mapa
local sound = workspace:FindFirstChild("Sound") -- Asegúrate de que el sonido esté en Workspace

-- Revisa continuamente si los jugadores están dentro de la región
game:GetService("RunService").Stepped:Connect(function()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local position = player.Character.HumanoidRootPart.Position
            -- Si el jugador está dentro de la región, reproduce el sonido
            if region:ContainsPoint(position) then
                if not sound.IsPlaying then
                    sound:Play()
                end
            else
                -- Si el jugador sale de la región, detén el sonido
                if sound.IsPlaying then
                    sound:Stop()
                end
            end
        end
    end
end)
