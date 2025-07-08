print("Loading Herkle Hub -- Booga Booga Reborn")
print("-----------------------------------------")
local Library = loadstring(game:HttpGetAsync("https://github.com/1dontgiveaf/Fluent-Renewed/releases/download/v1.0/Fluent.luau"))()
local SaveManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/1dontgiveaf/Fluent-Renewed/refs/heads/main/Addons/SaveManager.luau"))()
local InterfaceManager = loadstring(game:HttpGetAsync("https://raw.githubusercontent.com/1dontgiveaf/Fluent-Renewed/refs/heads/main/Addons/InterfaceManager.luau"))()
 
local Window = Library:CreateWindow{
    Title = "Herkle Hub -- Booga Booga Reborn",
    SubTitle = "by herkle berlington",
    TabWidth = 160,
    Size = UDim2.fromOffset(830, 525),
    Resize = true,
    MinSize = Vector2.new(470, 380),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl
}

local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "menu" }),
    Combat = Window:AddTab({ Title = "Combat", Icon = "axe" }),
    Map = Window:AddTab({ Title = "Map", Icon = "trees" }),
    Pickup = Window:AddTab({ Title = "Pickup", Icon = "backpack" }),
    Farming = Window:AddTab({ Title = "Farming", Icon = "sprout" }),
    Extra = Window:AddTab({ Title = "Extra", Icon = "plus" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

local rs = game:GetService("ReplicatedStorage")
local packets = require(rs.Modules.Packets)
local plr = game.Players.LocalPlayer
local char = plr.Character or plr.CharacterAdded:Wait()
local root = char:WaitForChild("HumanoidRootPart")
local hum = char:WaitForChild("Humanoid")
local runs = game:GetService("RunService")
local httpservice = game:GetService("HttpService")
local Players = game:GetService("Players")
local localiservice = game:GetService("LocalizationService")
local marketservice = game:GetService("MarketplaceService")
local rbxservice = game:GetService("RbxAnalyticsService")
local placestructure
local tspmo = game:GetService("TweenService")
local itemslist = {
"Adurite", "Berry", "Bloodfruit", "Bluefruit", "Coin", "Essence", "Hide", "Ice Cube", "Iron", "Jelly", "Leaves", "Log", "Steel", "Stone", "Wood", "Gold", "Raw Gold", "Crystal Chunk", "Raw Emerald", "Pink Diamond", "Raw Adurite", "Raw Iron", "Coal"}
local Options = Library.Options
--{MAIN TAB}
local wstoggle = Tabs.Main:CreateToggle("wstoggle", { Title = "Walkspeed", Default = false })
local wsslider = Tabs.Main:CreateSlider("wsslider", { Title = "Value", Min = 1, Max = 35, Rounding = 1, Default = 16 })
local jptoggle = Tabs.Main:CreateToggle("jptoggle", { Title = "JumpPower", Default = false })
local jpslider = Tabs.Main:CreateSlider("jpslider", { Title = "Value", Min = 1, Max = 65, Rounding = 1, Default = 50 })
local hheighttoggle = Tabs.Main:CreateToggle("hheighttoggle", { Title = "HipHeight", Default = false })
local hheightslider = Tabs.Main:CreateSlider("hheightslider", { Title = "Value", Min = 0.1, Max = 6.5, Rounding = 1, Default = 2 })
local msatoggle = Tabs.Main:CreateToggle("msatoggle", { Title = "No Mountain Slip", Default = false })
Tabs.Main:CreateButton({Title = "Copy Job ID", Callback = function() setclipboard(game.JobId) end})
Tabs.Main:CreateButton({Title = "Copy HWID", Callback = function() setclipboard(rbxservice:GetClientId()) end})
Tabs.Main:CreateButton({Title = "Copy SID", Callback = function() setclipboard(rbxservice:GetSessionId()) end})
--{COMBAT TAB}
local killauratoggle = Tabs.Combat:CreateToggle("killauratoggle", { Title = "Kill Aura", Default = false })
local killaurarangeslider = Tabs.Combat:CreateSlider("killaurarange", { Title = "Range", Min = 1, Max = 9, Rounding = 1, Default = 5 })
local katargetcountdropdown = Tabs.Combat:CreateDropdown("katargetcountdropdown", { Title = "Max Targets", Values = { "1", "2", "3", "4", "5", "6" }, Default = "1" })
local kaswingcooldownslider = Tabs.Combat:CreateSlider("kaswingcooldownslider", { Title = "Attack Cooldown (s)", Min = 0.01, Max = 1.01, Rounding = 2, Default = 0.1 })
--{MAP TAB}
local resourceauratoggle = Tabs.Map:CreateToggle("resourceauratoggle", { Title = "Resource Aura", Default = false })
local resourceaurarange = Tabs.Map:CreateSlider("resourceaurarange", { Title = "Range", Min = 1, Max = 20, Rounding = 1, Default = 20 })
local resourcetargetdropdown = Tabs.Map:CreateDropdown("resourcetargetdropdown", { Title = "Max Targets", Values = { "1", "2", "3", "4", "5", "6" }, Default = "1" })
local resourcecooldownslider = Tabs.Map:CreateSlider("resourcecooldownslider", { Title = "Swing Cooldown (s)", Min = 0.01, Max = 1.01, Rounding = 2, Default = 0.1 })
local critterauratoggle = Tabs.Map:CreateToggle("critterauratoggle", { Title = "Critter Aura", Default = false })
local critterrangeslider = Tabs.Map:CreateSlider("critterrangeslider", { Title = "Range", Min = 1, Max = 20, Rounding = 1, Default = 20 })
local crittertargetdropdown = Tabs.Map:CreateDropdown("crittertargetdropdown", { Title = "Max Targets", Values = { "1", "2", "3", "4", "5", "6" }, Default = "1" })
local crittercooldownslider = Tabs.Map:CreateSlider("crittercooldownslider", { Title = "Swing Cooldown (s)", Min = 0.01, Max = 1.01, Rounding = 2, Default = 0.1 })
--{PICKUP TAB}
local autopickuptoggle = Tabs.Pickup:CreateToggle("autopickuptoggle", { Title = "Auto Pickup", Default = false })
local chestpickuptoggle = Tabs.Pickup:CreateToggle("chestpickuptoggle", { Title = "Auto Pickup From Chests", Default = false })
local pickuprangeslider = Tabs.Pickup:CreateSlider("pickuprange", { Title = "Pickup Range", Min = 1, Max = 35, Rounding = 1, Default = 20 })
local itemdropdown = Tabs.Pickup:CreateDropdown("itemdropdown", {Title = "Items", Values = {"Berry", "Bloodfruit", "Bluefruit", "Lemon", "Strawberry", "Gold", "Raw Gold", "Crystal Chunk", "Coin", "Coins", "Coin2", "Coin Stack", "Essence", "Emerald", "Raw Emerald", "Pink Diamond", "Raw Pink Diamond", "Void Shard","Jelly", "Magnetite", "Raw Magnetite", "Adurite", "Raw Adurite", "Ice Cube", "Stone", "Iron", "Raw Iron", "Steel", "Hide", "Leaves", "Log", "Wood", "Pie"}, Multi = true, Default = { Leaves = true, Log = true }})
local droptoggle = Tabs.Pickup:AddToggle("droptoggle", { Title = "Auto Drop", Default = false })
local dropdropdown = Tabs.Pickup:AddDropdown("dropdropdown", {Title = "Select Item to Drop", Values = { "Bloodfruit", "Jelly", "Bluefruit", "Log", "Leaves", "Wood" }, Default = "Bloodfruit"})
local droptogglemanual = Tabs.Pickup:AddToggle("droptogglemanual", { Title = "Auto Drop Custom", Default = false })
local droptextbox = Tabs.Pickup:AddInput("droptextbox", { Title = "Custom Item", Default = "Bloodfruit", Numeric = false, Finished = false })
--{FARMING TAB}
local fruitdropdown = Tabs.Farming:CreateDropdown("fruitdropdown", {Title = "Select Fruit",Values = {"Bloodfruit", "Bluefruit", "Lemon", "Coconut", "Jelly", "Banana", "Orange", "Oddberry", "Berry", "Strangefruit", "Strawberry", "Sunjfruit", "Pumpkin", "Prickly Pear", "Apple",  "Barley", "Cloudberry", "Carrot"}, Default = "Bloodfruit"})
local planttoggle = Tabs.Farming:CreateToggle("planttoggle", { Title = "Auto Plant", Default = false })
local plantrangeslider = Tabs.Farming:CreateSlider("plantrange", { Title = "Plant Range", Min = 1, Max = 30, Rounding = 1, Default = 30 })
local plantdelayslider = Tabs.Farming:CreateSlider("plantdelay", { Title = "Plant Delay (s)", Min = 0.01, Max = 1, Rounding = 2, Default = 0.1 })
local harvesttoggle = Tabs.Farming:CreateToggle("harvesttoggle", { Title = "Auto Harvest", Default = false })
local harvestrangeslider = Tabs.Farming:CreateSlider("harvestrange", { Title = "Harvest Range", Min = 1, Max = 30, Rounding = 1, Default = 30 })
Tabs.Farming:CreateParagraph("Aligned Paragraph", {Title = "Tween Stuff", Content = "wish this ui was more like linoria :(", TitleAlignment = "Middle", ContentAlignment = Enum.TextXAlignment.Center})
local tweenplantboxtoggle = Tabs.Farming:AddToggle("tweentoplantbox", { Title = "Tween to Plant Box", Default = false })
local tweenbushtoggle = Tabs.Farming:AddToggle("tweentobush", { Title = "Tween to Bush + Plant Box", Default = false })
local tweenrangeslider = Tabs.Farming:AddSlider("tweenrange", { Title = "Range", Min = 1, Max = 250, Rounding = 1, Default = 250 })
Tabs.Farming:CreateParagraph("Aligned Paragraph", {Title = "Plantbox Stuff", Content = "wish this ui was more like linoria :(", TitleAlignment = "Middle", ContentAlignment = Enum.TextXAlignment.Center})
Tabs.Farming:CreateButton({Title = "Place 16x16 Plantboxes (256)", Callback = function() placestructure(16) end })
Tabs.Farming:CreateButton({Title = "Place 15x15 Plantboxes (225)", Callback = function() placestructure(15) end })
Tabs.Farming:CreateButton({Title = "Place 10x10 Plantboxes (100)", Callback = function() placestructure(10) end })
Tabs.Farming:CreateButton({Title = "Place 5x5 Plantboxes (25)", Callback = function() placestructure(5) end })
--{EXTRA TAB}
Tabs.Extra:CreateButton({Title = "Infinite Yield", Description = "inf yield chat", Callback = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/decryp1/herklesiy/refs/heads/main/hiy"))()end})
Tabs.Extra:CreateParagraph("Aligned Paragraph", {Title = "orbit breaks sometimes", Content = "i dont give a shit", TitleAlignment = "Middle", ContentAlignment = Enum.TextXAlignment.Center})
local orbittoggle = Tabs.Extra:CreateToggle("orbittoggle", { Title = "Item Orbit", Default = false })
local orbitrangeslider = Tabs.Extra:CreateSlider("orbitrange", { Title = "Grab Range", Min = 1, Max = 50, Rounding = 1, Default = 20 })
local orbitradiusslider = Tabs.Extra:CreateSlider("orbitradius", { Title = "Orbit Radius", Min = 0, Max = 30, Rounding = 1, Default = 10 })
local orbitspeedslider = Tabs.Extra:CreateSlider("orbitspeed", { Title = "Orbit Speed", Min = 0, Max = 10, Rounding = 1, Default = 5 })
local itemheightslider = Tabs.Extra:CreateSlider("itemheight", { Title = "Item Height", Min = -3, Max = 10, Rounding = 1, Default = 3 })
--{END OF TAB ELEMENTS}

local wscon, hhcon
local function updws()
    if wscon then wscon:Disconnect() end

    if Options.wstoggle.Value or Options.jptoggle.Value then
        wscon = runs.RenderStepped:Connect(function()
            if hum then
                hum.WalkSpeed = Options.wstoggle.Value and Options.wsslider.Value or 16
                hum.JumpPower = Options.jptoggle.Value and Options.jpslider.Value or 50
            end
        end)
    end
end

local function updhh()
    if hhcon then hhcon:Disconnect() end

    if Options.hheighttoggle.Value then
        hhcon = runs.RenderStepped:Connect(function()
            if hum then
                hum.HipHeight = Options.hheightslider.Value
            end
        end)
    end
end

local function onplradded(newChar)
    char = newChar
    root = char:WaitForChild("HumanoidRootPart")
    hum = char:WaitForChild("Humanoid")

    updws()
    updhh()
end

plr.CharacterAdded:Connect(onplradded)
Options.wstoggle:OnChanged(updws)
Options.jptoggle:OnChanged(updws)
Options.hheighttoggle:OnChanged(updhh)

local slopecon
local function updmsa()
    if slopecon then slopecon:Disconnect() end

    if Options.msatoggle.Value then
        slopecon = game:GetService("RunService").RenderStepped:Connect(function()
            if hum then
                hum.MaxSlopeAngle = 90
            end
        end)
    else
        if hum then
            hum.MaxSlopeAngle = 46
        end
    end
end

Options.msatoggle:OnChanged(updmsa)

local function getlayout(itemname)
    local inventory = game:GetService("Players").LocalPlayer.PlayerGui.MainGui.RightPanel.Inventory:FindFirstChild("List")
    if not inventory then
        return nil
    end
    for _, child in ipairs(inventory:GetChildren()) do
        if child:IsA("ImageLabel") and child.Name == itemname then
            return child.LayoutOrder
        end
    end
    return nil
end

local function swingtool(tspmogngicl)
    if packets.SwingTool and packets.SwingTool.send then
        packets.SwingTool.send(tspmogngicl)
    end
end

local function pickup(entityid)
    if packets.Pickup and packets.Pickup.send then
        packets.Pickup.send(entityid)
    end
end

local function drop(itemname)
    local inventory = game:GetService("Players").LocalPlayer.PlayerGui.MainGui.RightPanel.Inventory:FindFirstChild("List")
    if not inventory then return end

    for _, child in ipairs(inventory:GetChildren()) do
        if child:IsA("ImageLabel") and child.Name == itemname then
            if packets and packets.DropBagItem and packets.DropBagItem.send then
                packets.DropBagItem.send(child.LayoutOrder)
            end
        end
    end
end

local selecteditems = {}
itemdropdown:OnChanged(function(Value)
    selecteditems = {} 
    for item, State in pairs(Value) do
        if State then
            table.insert(selecteditems, item)
        end
    end
end)

task.spawn(function()
    while true do
        if not Options.killauratoggle.Value then
            task.wait(0.1)
            continue
        end

        local range = tonumber(Options.killaurarange.Value) or 20
        local targetCount = tonumber(Options.katargetcountdropdown.Value) or 1
        local cooldown = tonumber(Options.kaswingcooldownslider.Value) or 0.1
        local targets = {}

        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= plr then
                local playerfolder = workspace.Players:FindFirstChild(player.Name)
                if playerfolder then
                    local rootpart = playerfolder:FindFirstChild("HumanoidRootPart")
                    local entityid = playerfolder:GetAttribute("EntityID")

                    if rootpart and entityid then
                        local dist = (rootpart.Position - root.Position).Magnitude
                        if dist <= range then
                            table.insert(targets, { eid = entityid, dist = dist })
                        end
                    end
                end
            end
        end

        if #targets > 0 then
            table.sort(targets, function(a, b)
                return a.dist < b.dist
            end)

            local selectedTargets = {}
            for i = 1, math.min(targetCount, #targets) do
                table.insert(selectedTargets, targets[i].eid)
            end

            swingtool(selectedTargets)
        end

        task.wait(cooldown)
    end
end)

task.spawn(function()
    while true do
        if not Options.resourceauratoggle.Value then
            task.wait(0.1)
            continue
        end

        local range = tonumber(Options.resourceaurarange.Value) or 20
        local targetCount = tonumber(Options.resourcetargetdropdown.Value) or 1
        local cooldown = tonumber(Options.resourcecooldownslider.Value) or 0.1
        local targets = {}
        local allresources = {}

        for _, r in pairs(workspace.Resources:GetChildren()) do
            table.insert(allresources, r)
        end
        for _, r in pairs(workspace:GetChildren()) do
            if r:IsA("Model") and r.Name == "Gold Node" then
                table.insert(allresources, r)
            end
        end

        for _, res in pairs(allresources) do
            if res:IsA("Model") and res:GetAttribute("EntityID") then
                local eid = res:GetAttribute("EntityID")
                local ppart = res.PrimaryPart or res:FindFirstChildWhichIsA("BasePart")
                if ppart then
                    local dist = (ppart.Position - root.Position).Magnitude
                    if dist <= range then
                        table.insert(targets, { eid = eid, dist = dist })
                    end
                end
            end
        end

        if #targets > 0 then
            table.sort(targets, function(a, b)
                return a.dist < b.dist
            end)

            local selectedTargets = {}
            for i = 1, math.min(targetCount, #targets) do
                table.insert(selectedTargets, targets[i].eid)
            end

            swingtool(selectedTargets)
        end

        task.wait(cooldown)
    end
end)

task.spawn(function()
    while true do
        if not Options.critterauratoggle.Value then
            task.wait(0.1)
            continue
        end

        local range = tonumber(Options.critterrangeslider.Value) or 20
        local targetCount = tonumber(Options.crittertargetdropdown.Value) or 1
        local cooldown = tonumber(Options.crittercooldownslider.Value) or 0.1
        local targets = {}

        for _, critter in pairs(workspace.Critters:GetChildren()) do
            if critter:IsA("Model") and critter:GetAttribute("EntityID") then
                local eid = critter:GetAttribute("EntityID")
                local ppart = critter.PrimaryPart or critter:FindFirstChildWhichIsA("BasePart")

                if ppart then
                    local dist = (ppart.Position - root.Position).Magnitude
                    if dist <= range then
                        table.insert(targets, { eid = eid, dist = dist })
                    end
                end
            end
        end

        if #targets > 0 then
            table.sort(targets, function(a, b)
                return a.dist < b.dist
            end)

            local selectedTargets = {}
            for i = 1, math.min(targetCount, #targets) do
                table.insert(selectedTargets, targets[i].eid)
            end

            swingtool(selectedTargets)
        end

        task.wait(cooldown)
    end
end)



task.spawn(function()
    while true do
        local range = tonumber(Options.pickuprange.Value) or 35

        if Options.autopickuptoggle.Value then
            for _, item in ipairs(workspace.Items:GetChildren()) do
                if item:IsA("BasePart") or item:IsA("MeshPart") then
                    local selecteditem = item.Name
                    local entityid = item:GetAttribute("EntityID")

                    if entityid and table.find(selecteditems, selecteditem) then
                        local dist = (item.Position - root.Position).Magnitude
                        if dist <= range then
                            pickup(entityid)
                        end
                    end
                end
            end
        end

        if Options.chestpickuptoggle.Value then
            for _, chest in ipairs(workspace.Deployables:GetChildren()) do
                if chest:IsA("Model") and chest:FindFirstChild("Contents") then
                    for _, item in ipairs(chest.Contents:GetChildren()) do
                        if item:IsA("BasePart") or item:IsA("MeshPart") then
                            local selecteditem = item.Name
                            local entityid = item:GetAttribute("EntityID")

                            if entityid and table.find(selecteditems, selecteditem) then
                                local dist = (chest.PrimaryPart.Position - root.Position).Magnitude
                                if dist <= range then
                                    pickup(entityid)
                                end
                            end
                        end
                    end
                end
            end
        end

        task.wait(0.01)
    end
end)

local debounce = 0
local cd = 0 -- i genuinely dont know why it breaks now, but turn this up to 0.3 - 0.2 to stop it from dropping other items
runs.Heartbeat:Connect(function()
    if Options.droptoggle.Value then
        if tick() - debounce >= cd then
            local selectedItem = Options.dropdropdown.Value
            drop(selectedItem)
            debounce = tick()
        end
    end
end)

runs.Heartbeat:Connect(function()
    if Options.droptogglemanual.Value then
        if tick() - debounce >= cd then
            local itemname = Options.droptextbox.Value
            drop(itemname)
            debounce = tick()
        end
    end
end)

local plantedboxes = {}
local fruittoitemid = {
    Bloodfruit = 94,
    Bluefruit = 377,
    Lemon = 99,
    Coconut = 1,
    Jelly = 604,
    Banana = 606,
    Orange = 602,
    Oddberry = 32,
    Berry = 35,
    Strangefruit = 302,
    Strawberry = 282,
    Sunfruit = 128,
    Pumpkin = 80,
    ["Prickly Pear"] = 378,
    Apple = 243,
    Barley = 247,
    Cloudberry = 101,
    Carrot = 147
}

local function plant(entityid, itemID)
    if packets.InteractStructure and packets.InteractStructure.send then
        packets.InteractStructure.send({ entityID = entityid, itemID = itemID })
        plantedboxes[entityid] = true
    end
end

local function getpbs(range)
    local plantboxes = {}
    for _, deployable in ipairs(workspace.Deployables:GetChildren()) do
        if deployable:IsA("Model") and deployable.Name == "Plant Box" then
            local entityid = deployable:GetAttribute("EntityID")
            local ppart = deployable.PrimaryPart or deployable:FindFirstChildWhichIsA("BasePart")
            if entityid and ppart then
                local dist = (ppart.Position - root.Position).Magnitude
                if dist <= range then
                    table.insert(plantboxes, { entityid = entityid, deployable = deployable, dist = dist })
                end
            end
        end
    end
    return plantboxes
end

local function getbushes(range, fruitname)
    local bushes = {}
    for _, model in ipairs(workspace:GetChildren()) do
        if model:IsA("Model") and model.Name:find(fruitname) then
            local ppart = model.PrimaryPart or model:FindFirstChildWhichIsA("BasePart")
            if ppart then
                local dist = (ppart.Position - root.Position).Magnitude
                if dist <= range then
                    local entityid = model:GetAttribute("EntityID")
                    if entityid then
                        table.insert(bushes, { entityid = entityid, model = model, dist = dist })
                    end
                end
            end
        end
    end
    return bushes
end

local tweening = nil
local function tween(target)
    if tweening then tweening:Cancel() end
    local distance = (root.Position - target.Position).Magnitude
    local duration = distance / 21
    local tweenInfo = TweenInfo.new(duration, Enum.EasingStyle.Linear)
    local tween = tspmo:Create(root, tweenInfo, { CFrame = target })
    tween:Play()
    
    tweening = tween
end

local function tweenplantbox(range)
    while tweenplantboxtoggle.Value do
        local plantboxes = getpbs(range)
        table.sort(plantboxes, function(a, b) return a.dist < b.dist end)

        for _, box in ipairs(plantboxes) do
            if not box.deployable:FindFirstChild("Seed") then
                local target = box.deployable.PrimaryPart.CFrame + Vector3.new(0, 5, 0)
                tween(target)
                break
            end
        end

        task.wait(0.1)
    end
end

local function tweenpbs(range, fruitname)
    while tweenbushtoggle.Value do
        local bushes = getbushes(range, fruitname)
        table.sort(bushes, function(a, b) return a.dist < b.dist end)

        if #bushes > 0 then
            for _, bush in ipairs(bushes) do
                local target = bush.model.PrimaryPart.CFrame + Vector3.new(0, 5, 0)
                tween(target)
                break
            end
        else
            local plantboxes = getpbs(range)
            table.sort(plantboxes, function(a, b) return a.dist < b.dist end)

            for _, box in ipairs(plantboxes) do
                if not box.deployable:FindFirstChild("Seed") then
                    local target = box.deployable.PrimaryPart.CFrame + Vector3.new(0, 5, 0)
                    tween(target)
                    break
                end
            end
        end

        task.wait(0.1)
    end
end

task.spawn(function()
    while true do
        if not Options.planttoggle.Value then
            task.wait(0.1)
            continue
        end

        local range = tonumber(Options.plantrange.Value) or 30
        local delay = tonumber(Options.plantdelay.Value) or 0.1
        local selectedfruit = Options.fruitdropdown.Value
        local itemID = fruittoitemid[selectedfruit] or 94
        local plantboxes = getpbs(range)
        table.sort(plantboxes, function(a, b) return a.dist < b.dist end)

        for _, box in ipairs(plantboxes) do
            if not box.deployable:FindFirstChild("Seed") then
                plant(box.entityid, itemID)
            else
                plantedboxes[box.entityid] = true
            end
        end
        task.wait(delay)
    end
end)

task.spawn(function()
    while true do
        if not Options.harvesttoggle.Value then
            task.wait(0.1)
            continue
        end
        local harvestrange = tonumber(Options.harvestrange.Value) or 30
        local selectedfruit = Options.fruitdropdown.Value
        local bushes = getbushes(harvestrange, selectedfruit)
        table.sort(bushes, function(a, b) return a.dist < b.dist end)
        for _, bush in ipairs(bushes) do
            pickup(bush.entityid)
        end
        task.wait(0.1)
    end
end)

task.spawn(function()
    while true do
        if not tweenplantboxtoggle.Value then
            task.wait(0.1)
            continue
        end
        local range = tonumber(Options.tweenrange.Value) or 250
        tweenplantbox(range)
    end
end)

task.spawn(function()
    while true do
        if not tweenbushtoggle.Value then
            task.wait(0.1)
            continue
        end
        local range = tonumber(Options.tweenrange.Value) or 20
        local selectedfruit = Options.fruitdropdown.Value
        tweenpbs(range, selectedfruit)
    end
end)

placestructure = function(gridsize)
    if not plr or not plr.Character then return end

    local torso = plr.Character:FindFirstChild("HumanoidRootPart")
    if not torso then return end

    local startpos = torso.Position - Vector3.new(0, 3, 0)
    local spacing = 6.04

    for x = 0, gridsize - 1 do
        for z = 0, gridsize - 1 do
            task.wait(0.3)
            local position = startpos + Vector3.new(x * spacing, 0, z * spacing)

            if packets.PlaceStructure and packets.PlaceStructure.send then
                packets.PlaceStructure.send{
                    ["buildingName"] = "Plant Box",
                    ["yrot"] = 45,
                    ["vec"] = position,
                    ["isMobile"] = false
                }
            end
        end
    end
end

local orbiton, range, orbitradius, orbitspeed, itemheight = false, 20, 10, 5, 3
local attacheditems, itemangles, lastpositions = {}, {}, {}
local itemsfolder = workspace:WaitForChild("Items")

orbittoggle:OnChanged(function(value)
    orbiton = value
    if not orbiton then
        for _, bp in pairs(attacheditems) do bp:Destroy() end
        table.clear(attacheditems)
        table.clear(itemangles)
        table.clear(lastpositions)
    else
        task.spawn(function()
            while orbiton do
                for item, bp in pairs(attacheditems) do
                    if item then
                        local currentpos = item.Position
                        local lastpos = lastpositions[item]
                        
                        if lastpos and (currentpos - lastpos).Magnitude < 0.1 then
                            if packets.ForceInteract and packets.ForceInteract.send then
                                packets.ForceInteract.send(item:GetAttribute("EntityID"))
                            end
                        end

                        lastpositions[item] = currentpos
                    end
                end
                task.wait(0.1)
            end
        end)
    end
end)

orbitrangeslider:OnChanged(function(value) range = value end)
orbitradiusslider:OnChanged(function(value) orbitradius = value end)
orbitspeedslider:OnChanged(function(value) orbitspeed = value end)
itemheightslider:OnChanged(function(value) itemheight = value end)

runs.RenderStepped:Connect(function()
    if not orbiton then return end
    local time = tick() * orbitspeed
    for item, bp in pairs(attacheditems) do
        if item then
            local angle = itemangles[item] + time
            bp.Position = root.Position + Vector3.new(math.cos(angle) * orbitradius, itemheight, math.sin(angle) * orbitradius)
        end
    end
end)

task.spawn(function()
    while true do
        if orbiton then
            local children, index = itemsfolder:GetChildren(), 0
            local anglestep = (math.pi * 2) / math.max(#children, 1)

            for _, item in pairs(children) do
                local primary = item:IsA("BasePart") and item or item:IsA("Model") and item.PrimaryPart
                if primary and (primary.Position - root.Position).Magnitude <= range then
                    if not attacheditems[primary] then
                        local bp = Instance.new("BodyPosition")
                        bp.MaxForce, bp.D, bp.P, bp.Parent = Vector3.new(math.huge, math.huge, math.huge), 1500, 25000, primary
                        attacheditems[primary], itemangles[primary], lastpositions[primary] = bp, index * anglestep, primary.Position
                        index += 1
                    end
                end
            end
        end
        task.wait()
    end
end)

SaveManager:SetLibrary(Library)
InterfaceManager:SetLibrary(Library)
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes{}
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")
InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)
Window:SelectTab(1)
Library:Notify{
    Title = "Herkle Hub",
    Content = "Loaded, Enjoy!",
    Duration = 8
}
SaveManager:LoadAutoloadConfig()
print("Done! Enjoy Herkle Hub!")
