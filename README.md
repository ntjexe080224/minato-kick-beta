local sourceCode = [[
local Admins = {
    ["eo_minatoqteama"] = true -- Substitua por seu nome de usuário
}

local BannedPlayers = {}

game.Players.PlayerAdded:Connect(function(player)
    if BannedPlayers[player.UserId] then
        player:Kick("Você está banido.")
    end
end)

game.Players.PlayerAdded:Connect(function(player)
    player.Chatted:Connect(function(msg)
        if not Admins[player.Name] then return end

        local args = string.split(msg, " ")
        local cmd = string.lower(args[1])

        if cmd == "!kick" and args[2] then
            local target = game.Players:FindFirstChild(args[2])
            if target then
                target:Kick("Você foi expulso.")
            end

        elseif cmd == "!kickall" then
            for _, p in pairs(game.Players:GetPlayers()) do
                if not Admins[p.Name] then
                    p:Kick("Todos foram expulsos.")
                end
            end

        elseif cmd == "!ban" and args[2] then
            local target = game.Players:FindFirstChild(args[2])
            if target then
                BannedPlayers[target.UserId] = true
                target:Kick("Você foi banido.")
            end
        end
    end)
end)
]]

loadstring(sourceCode)()
