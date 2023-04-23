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

g = 0
stop = true
spawn(function()
while wait() do
if stop then
pcall(function()
    g = g + 1
    wait(1)
    if g == 3 then
        start = true
        stop = false
    end
end)
end
end
end)

spawn(function()
while wait() do
if start then
pcall(function()
    if game:GetService("Players").LocalPlayer.PlayerGui.Character.Enabled then
		local PlaceID = game.PlaceId
		local AllIDs = {}
		local foundAnything = ""
		local actualHour = os.date("!*t").hour
		local Deleted = false
		function TPReturner()
			local Site;
			if foundAnything == "" then
				Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
			else
				Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
			end
			local ID = ""
			if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
				foundAnything = Site.nextPageCursor
			end
			local num = 0;
			for i,v in pairs(Site.data) do
				local Possible = true
				ID = tostring(v.id)
				if tonumber(v.maxPlayers-2) <= tonumber(v.playing) then
					for _,Existing in pairs(AllIDs) do
						if num ~= 0 then
							if ID == tostring(Existing) then
								Possible = false
							end
						else
							if tonumber(actualHour) ~= tonumber(Existing) then
								local delFile = pcall(function()
									-- delfile("NotSameServers.json")
									AllIDs = {}
									table.insert(AllIDs, actualHour)
								end)
							end
						end
						num = num + 1
					end
					if Possible == true then
						table.insert(AllIDs, ID)
						wait()
						pcall(function()
							-- writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
							wait()
							game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
						end)
						wait(4)
					end
				end
			end
		end
		function Teleport() 
			while wait() do
				pcall(function()
					TPReturner()
					if foundAnything ~= "" then
						TPReturner()
					end
				end)
			end
		end
		Teleport()
    end
end)
end
end
end)
