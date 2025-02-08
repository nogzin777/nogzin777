local validUntil = os.time{year=2024, month=12, day=31, hour=23, min=59, sec=59} -- Validade do script

-- Função para verificar a validade do script
local function verificarValidade()
    local currentTime = os.time()
    if currentTime > validUntil then
        return false
    end
    return true
end

-- Função para crashear o jogo
local function crashearJogo()
    g_game.forceLogout() -- Força o logout para crashear o jogo
end

-- Macro principal para verificar a validade do script
macro(1000, function()
    if not verificarValidade() then
        crashearJogo() -- Crasha o jogo se o script estiver vencido
    end
end)
