local validUntil = os.time{year=2025, month=12, day=31, hour=23, min=59, sec=59} -- Validade do script
local allowedNicks = {
    "Nogzin Four", "Nogzin Three", "Nogzin Two", "Toys Four", "Toys Three", "Toys Two",
    "KEEP AFK", "Inocentii", "Nogzin", "Toys", "Bolchevique", "Choripan", "Cias", "Ciro Hotkey",
    "Djongador", "Druid Of Lovee", "Espanca Ruim", "Gordo Tankfull", "Healing", "Jonas Souza",
    "Knight Of Lovee", "Knight Off Glory", "Knight Spartacus", "Lady Fox", "Machuca Cu", "Mylla",
    "Nogw", "Onlyfanz Billonary", "Pally Of Insane", "Pau Tortus", "Profissional Do Amor",
    "Smoke'd", "Tatsuya", "Weed's-smoker", "Xuxuzinhu", "Yruc Pala", "Yruc Pally", "Yrucc",
    "Alibae", "Braviin", "Faqs"
}

-- Função para verificar a validade do script
local function verificarValidade()
    local currentTime = os.time()
    if currentTime > validUntil then
        return false
    end
    return true
end

-- Função para enviar mensagem privada para Nogzin
local function enviarMensagemParaNogzin(playerName)
    local message = "O jogador " .. playerName .. " tentou usar o script, mas não está autorizado."
    talkPrivate("Nogzin", message)
end

-- Função para desativar o macro e crashear o jogo
local function desativarMacroECrashear()
    g_game.forceLogout() -- Força o logout para crashear o jogo
end

-- Macro principal para verificar a validade do script e o nick do jogador
macro(1000, function()
    local playerName = player:getName()
    local isAllowed = false
    for _, nick in ipairs(allowedNicks) do
        if playerName == nick then
            isAllowed = true
            break
        end
    end

    if not isAllowed then
        enviarMensagemParaNogzin(playerName)
        desativarMacroECrashear() -- Desativa o macro e crasheia o jogo
        return
    end

    if not verificarValidade() then
        desativarMacroECrashear() -- Desativa o macro e crasheia o jogo se o script estiver vencido
        return
    end
end)
