repeat wait() until game:IsLoaded()

spawn(function()
while wait() do
if true then
pcall(function()
game:GetService("Players").LocalPlayer.PlayerGui.Character.Next.Size = UDim2.new(0, 10000, 0, 10000)
game:GetService("Players").LocalPlayer.PlayerGui.CustomizeGui.Play.Size = UDim2.new(10000, 10000, 10000, 10000)
game:GetService("Players").LocalPlayer.PlayerGui.CustomizeGui.Play.Position = UDim2.new(0, 0, 0, 0)
if game:GetService("Players").LocalPlayer.PlayerGui.Character.CreaturePreview.Back.Visible then
    game:GetService("Players").LocalPlayer.PlayerGui.Character.CreaturePreview.Back.Size = UDim2.new(0, 100000, 0, 100000)
    game:GetService("Players").LocalPlayer.PlayerGui.Character.CreaturePreview.Position = UDim2.new(0, 0, 0, 0)
end
--
end)
end
end
end)

spawn(function()
while wait() do
if true then
pcall(function()
if game:GetService("Players").LocalPlayer.PlayerGui.Character.Enabled or game:GetService("Players").LocalPlayer.PlayerGui.CustomizeGui.Enabled or game:GetService("Players").LocalPlayer.PlayerGui.Character.CreaturePreview.Enabled then
    Number = 0
    game:GetService'VirtualUser':Button1Down(Vector2.new(Number, Number))
    game:GetService'VirtualUser':Button1Up(Vector2.new(Number, Number))
end

game:GetService("Players").LocalPlayer.PlayerGui.LoginRewards.Enabled = false
end)
end
end
end)

spawn(function()
while wait() do
if true then
pcall(function()
local args = {
    [1] = "CreatureDeletion",
    [2] = game:GetService("Players").LocalPlayer.Data.Slot1
}

game:GetService("Players").LocalPlayer.RemoteEvent:FireServer(unpack(args))
end)
end
end
end)
