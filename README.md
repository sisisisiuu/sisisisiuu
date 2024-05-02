- 👋 Hi, I’m @sisisisiuu
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
sisisisiuu/sisisisiuu is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
-- Definir a distância máxima para coleta de frutas
local maxDistanceFruits = 15

-- Função para encontrar frutas próximas
local function findNearestFruit()
    local fruits = game.Workspace.Fruits:GetChildren()
    local nearestFruit = nil
    local minDistance = maxDistanceFruits + 1

    for _, fruit in ipairs(fruits) do
        local distance = (fruit.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude
        if distance < minDistance then
            minDistance = distance
            nearestFruit = fruit
        end
    end

    return nearestFruit
end

-- Função para coletar frutas
local function collectFruits()
    while true do
        wait(1) -- Intervalo de verificação
        
        local fruit = findNearestFruit()
        if fruit and fruit.Parent then
            local distance = (fruit.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude
            if distance <= maxDistanceFruits then
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(fruit.Position)
                wait(0.5) -- Tempo para chegar até a fruta
                game:GetService("ReplicatedStorage").Remotes.Events.Hit:FireServer(fruit)
            end
        end
    end
end

-- Função para auto farmar
local function autoFarm()
    while true do
        wait(5) -- Intervalo entre cada nivel up

        -- Aqui você pode adicionar o código para interagir com o sistema de nivelamento do jogo
        -- Exemplo: game:GetService("ReplicatedStorage").Remotes.Events.Level:FireServer()
    end
end

-- Função para eventos no mar
local function eventSeas()
    while true do
        wait(60) -- Intervalo para verificar eventos

        -- Aqui você pode adicionar o código para lidar com eventos no mar, como matar sea beast, terror shark, piranha, shark, raid barco, e barco assombrado
    end
end

-- Função para auto chip raid
local function autoChipRaid(raidType)
    -- Aqui você pode adicionar o código para comprar um chip de raid automaticamente
    -- Exemplo: game:GetService("ReplicatedStorage").Remotes.Events.Buy:FireServer("RaidChip", raidType)
end

-- Função para auto start raid
local function autoStartRaid()
    -- Aqui você pode adicionar o código para iniciar uma raid automaticamente
    -- Exemplo: game:GetService("ReplicatedStorage").Remotes.Events.Raid:FireServer()
end

-- Função para auto next island
local function autoNextIsland()
    -- Aqui você pode adicionar o código para ir para a próxima ilha da raid automaticamente
    -- Exemplo: game:GetService("ReplicatedStorage").Remotes.Events.Raid:FireServer("NextIsland")
end

-- Função para kill aura na raid
local function killAuraRaid()
    -- Aqui você pode adicionar o código para matar os NPCs da raid automaticamente
    -- Exemplo: Adicionar um loop para detectar NPCs e atacá-los automaticamente
end

-- Iniciar as funções em threads separadas
spawn(collectFruits)
spawn(autoFarm)
spawn(eventSeas)

-- Funções específicas para a aba Raid
local raid = {}

-- Função para comprar um chip de raid
function raid.autoChip(raidType)
    autoChipRaid(raidType)
end

-- Função para iniciar uma raid
function raid.autoStart()
    autoStartRaid()
end

-- Função para ir para a próxima ilha da raid
function raid.autoNextIsland()
    autoNextIsland()
end

-- Função para ativar o Kill Aura na raid
function raid.killAura()
    killAuraRaid()
end

-- Adicionar a aba Raid
_G.Raid = raid
