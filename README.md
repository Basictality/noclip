------------Settings-------------
Admins = "Basictality"

---------End Of Settings---------
wait()
local Owner = game:GetService("Players")[Admins]
 orbcol = "0,0,0"
print'Running.'
trailcol = "0,85,0"
local Character = nil
local Orb = nil
 
local Settings = {
        ["Trail"] = true,
        ["TrailColor"] = BrickColor.White(),
       
        ["Radius"] = 7,
        ["Height"] = 1.2,
        ["Bounce"] = 2.7,
       
    ["AudioID"] = 9,
       
        ["Sounds"] = {
            225000651, --OMFG I love You
            259816079, --Spooky scary skeletons MLG
            257275814
        },
       
        ["Speed"] = 88
}
 
function BasicOnChatted()
	for i,v in pairs(game.Players:children()) do if v.Name==Admins then
function OnChatted(msg)
    if msg:lower():sub(1,6) == "hide;" then
	Orb.Transparency=1
        end
end

game:GetService('Players')[Admins].Chatted:connect(OnChatted)
	end
	end
	end

BasicOnChatted()
 
if script.ClassName == "LocalScript" then
    if game.PlaceId == 178350907 then
       script.Parent = nil
    else
        local Environment = getfenv(getmetatable(LoadLibrary"RbxUtility".Create).__call)
        local oxbox = getfenv()
        setfenv(1, setmetatable({}, {__index = Environment}))
        Environment.coroutine.yield()
        oxbox.script:Destroy()
    end
else
    game.Players.PlayerAdded:connect(function(plr)
      if plr.Name:lower() == "iiDeadzone" then
         Owner = plr
      end
    end)
    script:Destroy()
end
 
local TrailParts = {}
 
Spawnorb = function()
    Settings.AudioID = Settings.Sounds[math.random(1, #Settings.Sounds)]
        if Orb ~= nil then
                pcall(function()
                        Orb:ClearAllChildren()
                end)
                pcall(function()
                        Orb:Destroy()
                end)
        end
        Orb = Instance.new('Part', workspace)
        Orb.Color = Color3.new(orbcol)
        Orb.Transparency = .1
		Orb.Name = "Head"
        Orb.Anchored = true
        Orb.CanCollide = false
        Orb.Locked = true
        Orb.FormFactor = "Symmetric"
        Orb.Shape = "Ball"
        Orb.Size = Vector3.new(1,1,1)
        Orb.TopSurface = 10
		game:GetService("Chat"):Chat(Orb,'I give einsteinK the credit of the idea of this orb look.',Enum.ChatColor.Green)
        Orb.BottomSurface = 10
		gui=Instance.new("BillboardGui")
		gui.Parent=Orb
		gui.Adornee=Orb
		gui.Size=UDim2.new(0,200,0,50)
		gui.StudsOffset=Vector3.new(0,2,0)
		text=Instance.new("TextLabel")
		text.Text = Owner.Name.."'s bOrb v.1 Build 2"
		text.Size=UDim2.new(0,50,0,50)
		text.Position = UDim2.new(0, 70,0, -15)
		text.BackgroundTransparency = 1
		text.TextStrokeTransparency = 0
		text.BorderSizePixel = 0
		text.FontSize = "Size18"
		text.TextColor3 = Color3.new(255,255,255)
		text.Parent=gui
		

        local Sound = Instance.new("Sound", Orb)
        Sound.SoundId = "rbxassetid://"..Settings.AudioID
        Sound.Volume = 1
        Sound.Pitch = 1
        Sound.Looped = true
        wait()
        Sound:Play()
        Orb.Changed:connect(function()
                if not workspace:FindFirstChild(Orb.Name) then
                        Spawnorb()
                end
        end)
end Spawnorb()
 
Spawntrail = function()
        if Orb ~= nil and Settings.Trail == true then
                local Tail = Instance.new('Part', Orb)
                Tail.Color = Color3.new(0,85,0)
                Tail.Transparency = .1
                Tail.Anchored = true
                Tail.CanCollide = false
                Tail.Locked = true
                Tail.FormFactor = "Custom"
                Tail.Size = Vector3.new(.2,.2,.2)
                Tail.CFrame = Orb.CFrame
                Tail.TopSurface = 10
                Tail.BottomSurface = 10
                table.insert(TrailParts, Tail)
                spawn(function()
                for i=1, 0,-.064 do
                _G.noob = 'i'
                game:service'RunService'.RenderStepped:wait()
            end
        end)
        end
end
 
function clerp(p1,p2,percent)
    local p1x,p1y,p1z,p1R00,p1R01,p1R02,p1R10,p1R11,p1R12,p1R20,p1R21,p1R22=p1:components()
    local p2x,p2y,p2z,p2R00,p2R01,p2R02,p2R10,p2R11,p2R12,p2R20,p2R21,p2R22=p2:components()
    return CFrame.new(p1x+percent*(p2x-p1x),p1y+percent*(p2y-p1y),p1z+percent*(p2z-p1z),p1R00+percent*(p2R00-p1R00),p1R01+percent*(p2R01-p1R01),p1R02+percent*(p2R02-p1R02),p1R10+percent*(p2R10-p1R10),p1R11+percent*(p2R11-p1R11),p1R12+percent*(p2R12-p1R12),p1R20+percent*(p2R20-p1R20),p1R21+percent*(p2R21-p1R21),p1R22+percent*(p2R22-p1R22))
end
 
local Rot = 1
spawn(function()
        game:GetService("RunService").RenderStepped:connect(function()
                if Owner and Owner.Character and Owner.Character:FindFirstChild("Torso") then
                    Character = Owner.Character.Torso.CFrame
                else
                        Character = CFrame.new(0,1.5,0)
                end
                if Orb ~= nil then
                        Rot = Rot + Settings.Speed
                        Orb.CFrame = clerp(Orb.CFrame,
                                Character
                                *CFrame.new(0,3.7,0)
                                *CFrame.Angles(0,Rot,(math.sin((tick())*3.7)*2.7)+13)
                                *CFrame.new(Settings.Radius, math.sin((tick())*Settings.Bounce)*Settings.Height, 0)
                                *CFrame.Angles(math.sin(tick()),math.sin(tick()),math.sin(tick()))
                        ,.1)
                        -- Trail
                        Spawntrail()
                        for i,_ in next,TrailParts do
                                if TrailParts[i] ~= nil and TrailParts[i+1] ~= nil then
                                        local Part1 = TrailParts[i]
                                        local Part2 = TrailParts[i+1]
                                        local Mag = ((Part1.CFrame.p-Part2.CFrame.p).magnitude)
                                        Part1.Size = Vector3.new(Part1.Size.X+.016, Mag, Part1.Size.Z+.016)
                                        Part1.Transparency = Part1.Transparency + .028
                                        Part1.CFrame = CFrame.new(Part1.CFrame.p, Part2.CFrame.p)
                                * CFrame.Angles(math.pi/2,0,0)
                                        if Part1.Size.X >= .64 then
                                                Part1:Destroy()
                                                table.remove(TrailParts, i)
                                        end
                                end
                        end
                end
        end)
end)
