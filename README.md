-- Função para carregar o perfil do CaveBot
local function carregarCavebotPerfil(perfil)
    local status, err = pcall(function()
        CaveBot.setCurrentProfile(perfil)
        print("CaveBot ativado com o perfil '" .. perfil .. "'.")
		messageSent = true
    end)
    if not status then
        print("Erro ao carregar o perfil: " .. err)
		messageSent = true
    else
        CaveBot.setOn() -- Ativa o CaveBot
    end
end

-- Função para parar o CaveBot e o Target
local function pararCavebotETarget()
    if CaveBot.isOn() then
        CaveBot.setOff()
        print("CaveBot pausado.")
		messageSent = true
    end
    if TargetBot.isOn() then
        TargetBot.setOff()
        print("Target pausado.")
		messageSent = true
    end
end

-- Função para ativar o Target
local function ativarTarget()
    if not TargetBot.isOn() then
        TargetBot.setOn()
        print("Target ativado.")
		messageSent = true
    end
end

-- Macro para executar ações baseadas em horários
macro(100, "CLICK UuuuuuuuP", function() -- Macro rodando a cada 100 ms
    local currentHour = tonumber(os.date("%H"))
    local currentMinute = tonumber(os.date("%M"))
    local currentSecond = tonumber(os.date("%S"))

    if currentHour == 12 and currentMinute == 55 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 12 and currentMinute == 55 and currentSecond == 1 then
        carregarCavebotPerfil("saida")
    elseif currentHour == 12 and currentMinute == 58 and currentSecond == 1 then
        pararCavebotETarget()
    elseif currentHour == 12 and currentMinute == 58 and currentSecond == 2 then
        carregarCavebotPerfil("cccc")
        ativarTarget()
    elseif currentHour == 12 and currentMinute == 59 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 13 and currentMinute == 00 and currentSecond == 6 then
        carregarCavebotPerfil("clickup")
    elseif currentHour == 13 and currentMinute == 27 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 13 and currentMinute == 27 and currentSecond == 5 then
        carregarCavebotPerfil("cccc")
	elseif currentHour == 13 and currentMinute == 27 and currentSecond == 10 then
        pararCavebotETarget()
    elseif currentHour == 13 and currentMinute == 27 and currentSecond == 15 then
	   carregarCavebotPerfil("bbbb")
	elseif currentHour == 17 and currentMinute == 55 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 17 and currentMinute == 55 and currentSecond == 1 then
        carregarCavebotPerfil("saida")
    elseif currentHour == 17 and currentMinute == 58 and currentSecond == 1 then
        pararCavebotETarget()
    elseif currentHour == 17 and currentMinute == 58 and currentSecond == 2 then
        carregarCavebotPerfil("cccc")
        ativarTarget()
    elseif currentHour == 17 and currentMinute == 59 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 18 and currentMinute == 00 and currentSecond == 6 then
        carregarCavebotPerfil("clickup")
    elseif currentHour == 18 and currentMinute == 27 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 18 and currentMinute == 27 and currentSecond == 5 then
        carregarCavebotPerfil("cccc")
    elseif currentHour == 18 and currentMinute == 27 and currentSecond == 10 then
        pararCavebotETarget()
    elseif currentHour == 18 and currentMinute == 27 and currentSecond == 15 then
        carregarCavebotPerfil("bbbb")
	elseif currentHour == 21 and currentMinute == 55 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 21 and currentMinute == 55 and currentSecond == 1 then
        carregarCavebotPerfil("saida")
    elseif currentHour == 21 and currentMinute == 58 and currentSecond == 1 then
        pararCavebotETarget()
    elseif currentHour == 21 and currentMinute == 58 and currentSecond == 2 then
        carregarCavebotPerfil("cccc")
        ativarTarget()
    elseif currentHour == 21 and currentMinute == 59 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 22 and currentMinute == 00 and currentSecond == 6 then
        carregarCavebotPerfil("clickup")
    elseif currentHour == 22 and currentMinute == 27 and currentSecond == 0 then
        pararCavebotETarget()
    elseif currentHour == 22 and currentMinute == 27 and currentSecond == 5 then
        carregarCavebotPerfil("cccc")
	elseif currentHour == 22 and currentMinute == 27 and currentSecond == 10 then
        pararCavebotETarget()
	elseif currentHour == 22 and currentMinute == 27 and currentSecond == 15 then
        carregarCavebotPerfil("bbbb")
		end
end)
