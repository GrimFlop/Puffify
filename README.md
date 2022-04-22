# Puffify
--Puffify Script E to enable Z to disable (you can always change keys in script)

--////PUFFIFY CREATED BY GRIMFLOP\\\\--

local plr            = game:GetService("Players").LocalPlayer --Gets player
local UIS            = game:GetService("UserInputService") --Gets User Input Service
local mouse          = plr:GetMouse() --Gets mouse
local char           = plr.Character  -- Gets character
local datBoi         = char.HumanoidRootPart:Clone() --Cursor part
local puffVal        = 2.1 --Change to increase how puffed up people will get
local puffColor      = Color3.fromRGB(255,255,0) --puff effect color(yellow by default)
local puffMaterial   = Enum.Material.Neon
local randomizeColor = false--Determines if the puff effect has randomized colors
local enabled        = false --Enabled toggle
local hotkey         = Enum.KeyCode.E --Enable/Disable hotkey
local quitKey        = Enum.KeyCode.Z
local cursorSize     = 2.1-- Change to increase size of hitbox
datBoi.CanCollide    = false -- boring stuff below
datBoi.Name          = "detboi"
datBoi.Size          = Vector3.new(cursorSize,cursorSize,cursorSize)
datBoi.Color         = Color3.fromRGB(255,0,0) --hitbox color (red by default)
datBoi.Massless      = true
datBoi.Transparency  = 1 
datBoi.Parent        = char --dont change

 game.StarterGui:SetCore("SendNotification", {
        Title    = "Puffify",
        Text     = "Script Loaded Succesfully",
        Duration = 4
        })

UIS.InputBegan:Connect(function(input,GPE) --enable/disable script 
    if GPE then return end
    if input.KeyCode == hotkey then
        if not enabled then datBoi.Transparency = 0.7 enabled = true else enabled = false datBoi.Transparency = 1 end
    end
end)

UIS.InputBegan:Connect(function(input,GPE) --Stop script
    if GPE then return end
    if input.KeyCode == quitKey then
            if char:FindFirstChild("detboi") then
        game.StarterGui:SetCore("SendNotification", {
        Title    = "Puffify",
        Text     = "Script stopped.",
        Duration = 4
        })
    end
        datBoi:Destroy()
    
    end
end)




datBoi.Touched:Connect(function(hit) --hitbox stuff
    if not enabled then return end
    if not hit.Parent:FindFirstChild("Humanoid")  then return end
    if hit.Parent == char then return end
    hit.Size            = Vector3.new(puffVal,puffVal,puffVal)
    local effect        = Instance.new("Part", workspace)
    effect.Position     = hit.Position
    effect.Anchored     = true
    if randomizeColor then puffColor = Color3.fromRGB(math.random(0,255),math.random(0,255),math.random(0,255)) end
    effect.Color        = puffColor
 
    effect.Material     = puffMaterial--material of puff effect
    effect.Shape        = "Ball" --shape of puff effect
    effect.Transparency = 0.9 -- transparency of puff effect
    effect.Size         = Vector3.new(1,1,1) --effect begin size
    game:GetService("TweenService"):Create(effect,TweenInfo.new(0.5,Enum.EasingStyle.Quad,Enum.EasingDirection.InOut),{Transparency = 1, Size = Vector3.new(4,4,4)}):Play() --tween
        game:GetService("Debris"):AddItem(effect, 0.5) -- destroys effect
   
end)



while char.Humanoid.Health>0 do
    wait()
    datBoi.Position    = mouse.Hit.Position
    datBoi.Orientation = char.HumanoidRootPart.Orientation
end

  
  
