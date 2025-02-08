local itemIdsToUse, useRange, moveRange = {8997}, 1, 7
local caminhoEvento = "clickup" -- Nome do perfil do CaveBot
local macroAtivo = false -- Controle do estado do macro

-- Definição dos horários de ativação e desativação
local horarios = {
    {ativacaoHora = 13, ativacaoMinuto = 0, ativacaoSegundo = 0, desativacaoHora = 13, desativacaoMinuto = 27, desativacaoSegundo = 0},
    {ativacaoHora = 18, ativacaoMinuto = 0, ativacaoSegundo = 0, desativacaoHora = 18, desativacaoMinuto = 27, desativacaoSegundo = 0},
    {ativacaoHora = 22, ativacaoMinuto = 0, ativacaoSegundo = 0, desativacaoHora = 22, desativacaoMinuto = 27, desativacaoSegundo = 0}
}

-- Função para verificar se estamos dentro dos horários permitidos
local function isInAllowedTime()
    local horaAtual = tonumber(os.date("%H"))
    local minutoAtual = tonumber(os.date("%M"))
    local segundoAtual = tonumber(os.date("%S"))
    for _, horario in ipairs(horarios) do
        local ativacao = horario.ativacaoHora * 3600 + horario.ativacaoMinuto * 60 + horario.ativacaoSegundo
        local desativacao = horario.desativacaoHora * 3600 + horario.desativacaoMinuto * 60 + horario.desativacaoSegundo
        local agora = horaAtual * 3600 + minutoAtual * 60 + segundoAtual

        if agora >= ativacao and agora <= desativacao then
            return true
        end
    end
    return false
end

-- Função para carregar o perfil do CaveBot
local function carregarCavebotEvento()
    local status, err = pcall(function()
        CaveBot.setCurrentProfile(caminhoEvento)
    end)
    if not status then return end
    CaveBot.setOn() -- Ativa o CaveBot
end

-- Função principal para procurar caixas
local function findItemsInLayer(layerIndex)
    local searchLayers = {
        {from = {x = posx() - 1, y = posy() - 1, z = posz()}, to = {x = posx() + 1, y = posy() + 1, z = posz()}},
        {from = {x = posx() - 2, y = posy() - 2, z = posz()}, to = {x = posx() + 2, y = posy() + 2, z = posz()}},
        {from = {x = posx() - 3, y = posy() - 3, z = posz()}, to = {x = posx() + 3, y = posy() + 3, z = posz()}},
        {from = {x = posx() - 4, y = posy() - 4, z = posz()}, to = {x = posx() + 4, y = posy() + 4, z = posz()}},
        {from = {x = posx() - 5, y = posy() - 5, z = posz()}, to = {x = posx() + 5, y = posy() + 5, z = posz()}},
        {from = {x = posx() - 6, y = posy() - 6, z = posz()}, to = {x = posx() + 6, y = posy() + 6, z = posz()}},
        {from = {x = posx() - 7, y = posy() - 7, z = posz()}, to = {x = posx() + 7, y = posy() + 7, z = posz()}}
    }
    if layerIndex > #searchLayers then return false end
    local currentLayer = searchLayers[layerIndex]
    for x = currentLayer.from.x, currentLayer.to.x do
        for y = currentLayer.from.y, currentLayer.to.y do
            local tile = g_map.getTile({x = x, y = y, z = posz()})
            if tile then
                for _, item in ipairs(tile:getItems()) do
                    if item and table.contains(itemIdsToUse, item:getId()) then
                        local distance = getDistanceBetween(pos(), tile:getPosition())
                        if distance <= useRange then
                            g_game.use(item)
                            CaveBot.setOff() -- Desativa o CaveBot ao encontrar a caixa
                            return true
                        end
                        if distance > useRange and distance <= moveRange then
                            if autoWalk(tile:getPosition(), moveRange, {ignoreNonPathable = true, precision = 1}) then
                                delay(200)
                                return true
                            end
                        end
                    end
                end
            end
        end
    end
    return findItemsInLayer(layerIndex + 1)
end

-- Macro principal
caixinhaaaaaa = macro(150, function()
    -- Verificar se estamos dentro dos horários permitidos
    if not isInAllowedTime() then
        if macroAtivo then
            macroAtivo = false
            CaveBot.setOff() -- Garante que o CaveBot está desativado fora do horário
        end
        return
    end

    -- Se dentro do horário, ativar macro
    macroAtivo = true
    local foundBox = findItemsInLayer(1)
    if not foundBox then
        carregarCavebotEvento() -- Ativa o CaveBot se não encontrar caixas
    end
end)
addIcon("AUTOo", {item=8997, text="AUTOo"},caixinhaaaaaa)
