local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- Função para limpar completamente um personagem
local function stripCharacter(character)
    if not character then return end
    
    -- Remove TODOS os acessórios
    for _, item in pairs(character:GetChildren()) do
        if item:IsA("Accessory") or item:IsA("Hat") then
            item:Destroy()
        end
    end
    
    -- Processa todas as partes do personagem
    for _, part in pairs(character:GetDescendants()) do
        -- Remove TODAS as roupas
        if part:IsA("Shirt") then
            part:Destroy()
        end
        
        if part:IsA("Pants") then
            part:Destroy()
        end
        
        if part:IsA("ShirtGraphic") then
            part:Destroy()
        end
        
        -- Remove pacotes de corpo (body packages)
        if part:IsA("CharacterMesh") then
            part:Destroy()
        end
        
        -- Remove todas as decals e texturas
        if part:IsA("Decal") then
            part:Destroy()
        end
        
        if part:IsA("Texture") then
            part:Destroy()
        end
        
        -- Limpa texturas de meshes especiais
        if part:IsA("SpecialMesh") then
            part.TextureId = ""
            -- Define mesh básico quando possível
            if part.MeshType == Enum.MeshType.FileMesh then
                part.MeshId = ""
            end
        end
        
        -- Limpa texturas de MeshParts
        if part:IsA("MeshPart") then
            part.TextureID = ""
            -- Tenta converter para Part básico se possível
            local size = part.Size
            local position = part.Position
            local parent = part.Parent
            
            -- Define cor cinza padrão
            part.Color = Color3.fromRGB(163, 162, 165)
            part.Material = Enum.Material.Plastic
        end
        
        -- Remove SurfaceAppearance (texturas PBR)
        if part:IsA("SurfaceAppearance") then
            part:Destroy()
        end
        
        -- Reseta TODAS as partes para cinza básico
        if part:IsA("BasePart") then
            -- Remove todas as propriedades visuais
            part.Color = Color3.fromRGB(163, 162, 165)
            part.Material = Enum.Material.Plastic
            part.Transparency = 0
            part.Reflectance = 0
            
            -- Remove BrickColor especial
            pcall(function()
                part.BrickColor = BrickColor.new("Medium stone grey")
            end)
        end
        
        -- Remove partículas e efeitos
        if part:IsA("ParticleEmitter") or 
           part:IsA("Fire") or 
           part:IsA("Smoke") or 
           part:IsA("Sparkles") or
           part:IsA("Light") or
           part:IsA("PointLight") or
           part:IsA("SpotLight") or
           part:IsA("SurfaceLight") then
            part:Destroy()
        end
        
        -- Remove trails e beams
        if part:IsA("Trail") or part:IsA("Beam") then
            part:Destroy()
        end
    end
    
    -- Remove especificamente a face
    local head = character:FindFirstChild("Head")
    if head then
        -- Remove QUALQUER face
        for _, item in pairs(head:GetChildren()) do
            if item:IsA("Decal") or item.Name:lower():find("face") then
                item:Destroy()
            end
        end
        
        -- Garante que a cabeça seja cinza
        head.Color = Color3.fromRGB(163, 162, 165)
        head.Material = Enum.Material.Plastic
    end
    
    -- Remove body colors customizados
    local bodyColors = character:FindFirstChildOfClass("BodyColors")
    if bodyColors then
        bodyColors.HeadColor = BrickColor.new("Medium stone grey")
        bodyColors.TorsoColor = BrickColor.new("Medium stone grey")
        bodyColors.LeftArmColor = BrickColor.new("Medium stone grey")
        bodyColors.RightArmColor = BrickColor.new("Medium stone grey")
        bodyColors.LeftLegColor = BrickColor.new("Medium stone grey")
        bodyColors.RightLegColor = BrickColor.new("Medium stone grey")
    end
    
    -- Remove Humanoid customizations
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    if humanoid then
        -- Remove todas as animações customizadas
        local animator = humanoid:FindFirstChildOfClass("Animator")
        if animator then
            for _, track in pairs(animator:GetPlayingAnimationTracks()) do
                if not track.Animation.AnimationId:find("rbxasset") then
                    track:Stop()
                end
            end
        end
        
        -- Reseta descrição do avatar
        pcall(function()
            local description = humanoid:FindFirstChildOfClass("HumanoidDescription")
            if description then
                description:Destroy()
            end
        end)
    end
end

-- Função para processar jogadores continuamente
local function processPlayer(player)
    if player ~= Players.LocalPlayer then
        if player.Character then
            stripCharacter(player.Character)
        end
        
        -- Conecta para quando personagem spawnar/respawnar
        player.CharacterAdded:Connect(function(character)
            -- Delay para garantir que tudo carregou
            task.wait(0.5)
            stripCharacter(character)
            
            -- Reaplica após um tempo para garantir
            task.wait(1)
            stripCharacter(character)
        end)
        
        -- Monitora mudanças no personagem
        player.CharacterAppearanceLoaded:Connect(function(character)
            stripCharacter(character)
        end)
    end
end

-- Processa todos os jogadores existentes
for _, player in pairs(Players:GetPlayers()) do
    processPlayer(player)
end

-- Processa novos jogadores
Players.PlayerAdded:Connect(processPlayer)

-- Loop agressivo para manter tudo removido
local frameCount = 0
RunService.Heartbeat:Connect(function()
    frameCount = frameCount + 1
    
    -- A cada 30 frames (aproximadamente 0.5 segundos)
    if frameCount >= 30 then
        frameCount = 0
        
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= Players.LocalPlayer and player.Character then
                -- Remove qualquer coisa nova que apareça
                for _, item in pairs(player.Character:GetChildren()) do
                    if item:IsA("Accessory") or 
                       item:IsA("Hat") or 
                       item:IsA("Shirt") or 
                       item:IsA("Pants") or 
                       item:IsA("ShirtGraphic") then
                        item:Destroy()
                    end
                end
                
                -- Reaplica cor cinza
                for _, part in pairs(player.Character:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.Color = Color3.fromRGB(163, 162, 165)
                    end
                end
            end
        end
    end
end)

print("=" .. string.rep("=", 50))
print("✓ SCRIPT ATIVADO - Removedor Total de Skins")
print("→ Todas as roupas foram removidas")
print("→ Todos os acessórios foram removidos")
print("→ Todas as texturas foram limpas")
print("→ Todos os jogadores agora são bonecos cinza básicos")
print("=" .. string.rep("=", 50))
