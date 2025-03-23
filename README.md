local Library = loadstring(Game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/wizard"))()
local Hub = Library:NewWindow("nil.lua | Hub - Glass Bridge 2")
local Main = Hub:NewSection("AutoFarm Options")

_G.works = false
local AutoFarmThread

local function AutoFarm()
    local player = game:GetService("Players").LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
    local location = game:GetService("Workspace"):WaitForChild("Finish"):WaitForChild("Chest")

    if not character or not humanoidRootPart or not location then
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "Error",
            Text = "AutoFarm cannot start, missing parts.",
            Icon = "rbxassetid://111491696505833"
        })
        return
    end

    -- AutoFarm Loop
    while _G.works do
        humanoidRootPart.CFrame = location.CFrame
        task.wait(3.5) -- Prevents glitches
    end
end

Main:CreateToggle("Auto Farm", function()
    _G.works = not _G.works 

    if _G.works then
        AutoFarmThread = task.spawn(AutoFarm)

        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "AutoFarm",
            Text = "AutoFarm Enabled!",
            Icon = "rbxassetid://111491696505833"
        })
    else
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "AutoFarm",
            Text = "AutoFarm Disabled!",
            Icon = "rbxassetid://111491696505833"
        })

        _G.works = false
    end
end)
