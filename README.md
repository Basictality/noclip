-------Settings-------
Admins = "Player"
Music = true
Banned = "Test"






----End of Settings---
wait()
local Owner = game:GetService("Players")[Admins]
print'Loaded'


-----------[ONCHATTED FUNCTION]------------
-------------------------------------------
---------------FUNCTION(s)-----------------
-------------------------------------------

function AdminCmds()
local isAdmin = function(p)
 for i,v in pairs(Admins)do
  if p.Name == v then
   return true;
  end;
 end;
 return false;
end;
local Players = game:GetService("Players");
local meplyr = Owner
local people = function(str)
  local players = {};
  local strs = {
   {"me", "myself", function() players[#players+1]=meplyr end;};
   {"all", "everyone", "everybody", function() for i,v in pairs(Players:GetPlayers())do players[#players+1]=v; end; end;};
   {"others", "notme", function() for i,v in pairs(Players:GetPlayers())do if v.Name~= meplyr.Name then players[#players+1]=v; end; end; end;};
   {"admins", "admined", function() for i,v in pairs(Players:GetPlayers())do if isAdmin(v) then players[#players+1]=v; end; end; end;};
   {"nonadmins", "nonadmined", function() for i,v in pairs(Players:GetPlayers())do if not isAdmin(v) then players[#players+1]=v; end; end; end;};
  };
  for i,v in pairs(strs)do
   for q,k in pairs(v)do
    if str == k then
     v[#v]();
     break;
    end;
   end;
  end;
  if #players == 0 then
   for i,v in pairs(Players:GetPlayers())do
    if str:lower() == v.Name:lower():sub(1,string.len(str)) then
     players[#players+1]=v;
    end;
   end;
  end;
  return players;
 end;
--   if Prefix..data.Usage..Suffix == sub(lower(Message),1,string.len(Prefix)+string.len(data.Usage)+string.len(Suffix)) then
--    local y,n = ypcall(function()
--      data.Func(sub(Message,string.len(Prefix)+string.len(data.Usage)+string.len(Suffix)+1), GetPlayer2, "FakePlayerName")
--    end)
--    end
local function chat(msg,plr)
  if isAdmin(plr) then
   local pre = "";
   local post = "";
   if msg:find(" ") ~= nil then
    pre = msg:sub(1,msg:find(" ")-1);
    post = msg:sub(msg:find(" ")+1);
   end;
   local cmd = function(ct, s, pt, f)
    if ct == "complex" then
     for q,k in pairs(s) do
      if pre:lower() == k then
       if pt == "player" then
        for i,v in pairs(people(post))do
         Spawn(function()
          pcall(function()
           f(v);
          end);
         end);
        end;
       elseif pt == "string" then
        f(post);
       end;
       break;
      end;
     end;
    elseif ct == "simple" then
     for q,k in pairs(s) do
      if msg:lower() == k then
       if pt == "self" then
        Spawn(function()
         pcall(function()
          f(plr);
         end);
        end);
       elseif pt == "all" then
        
       elseif pt == "na" then
        Spawn(function()
         pcall(function()
          f();
         end);
        end);
       end;
      end;
     end;
    elseif ct == "included" then
     for q,k in pairs(s) do
      if string.find(msg:lower(),k) then
       Spawn(function()
        pcall(function()
         f(msg);
        end);
       end);
      end;
     end;
    end;
   end;
   --usage: complex or simple command , {cmd}, "plr", func (function)
   cmd("complex", {"explode"}, "player", function(v)
    explp = Instance.new("Explosion",v.Character);
	explp.BlastRadius = "1";
	explp.BlastPressure = "500000";
	explp.Position = v.Character.Torso.Position;
   end);
   cmd("complex", {"ungod"}, "player", function(v)
    vhum1 = v.Character:FindFirstChild('Humanoid')
	vhum1.MaxHealth = 100
   end);
   cmd("complex", {"kill"}, "player", function(v)
    v.Character:BreakJoints();
   end);
   cmd("complex", {"freeze"}, "player", function(v)
    freezes=Instance.new('Part',v.Character)
freezes.FormFactor = "Custom"
freezes.Size = Vector3.new(4.5,6.5,4.5)
freezes.Material = "SmoothPlastic"
freezes.BrickColor = BrickColor.new('Teal')
freezes.Transparency=0.5
freezes.Name = "Ice"
freezes.Anchored = true
freezes.Material = "Ice"

v.Character.Head.Anchored = true
v.Character.Torso.Anchored = true
v.Character['Left Arm'].Anchored = true
v.Character['Left Leg'].Anchored = true
v.Character['Right Arm'].Anchored = true
v.Character['Right Leg'].Anchored = true

freezes.CFrame = v.Character.Torso.CFrame
   end);
   cmd("complex", {"thaw"}, "player", function(v)
di = v.Character:FindFirstChild('Ice')
dim=Instance.new('CylinderMesh',di)
di.Size = Vector3.new(4.5,0,4.5)
di.CFrame = v.Character.Torso.CFrame * CFrame.new(0,-2.5,0)
di.CanCollide = false
di.Transparency=0

v.Character.Head.Anchored = false
v.Character.Torso.Anchored = false
v.Character['Left Arm'].Anchored = false
v.Character['Left Leg'].Anchored = false
v.Character['Right Arm'].Anchored = false
v.Character['Right Leg'].Anchored = false
game.Debriss:AddItem(3,di)
end);
   cmd("complex", {"god"}, "player", function(v)
    vhum = v.Character:FindFirstChild('Humanoid')
	vhum.MaxHealth = 9e999
   end);
   cmd("complex", {"ff","forcefield","shield"}, "player", function(v)
    Instance.new("ForceField",v.Character);
   end);
   cmd("complex", {"kick","boot"}, "player", function(v)
	v:remove()
   end);
  cmd("complex", {"sword","linkedsword"}, "player", function(v)
game:service'InsertService':LoadAsset(125013769):children()[1].Parent = v.Backpack
   end);
   cmd("complex", {"unff","unforcefield","unshield"}, "player", function(v)
    for i,k in pairs(v.Character:GetChildren()) do
     if k.ClassName == "ForceField" then
      k:Destroy();
     end;
    end;
   end);
  end;
end;

player = Owner
player.Chatted:connect(function(message) chat(message, player) end)
end

--------------[ORB FUNCTION]---------------
-------------------------------------------
---------------NEXT FUNCTION---------------
-------------------------------------------

function bOrb()
orbcol = "0,0,0"
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
            276644890, -- Fetty Wap - 679 (FULL SONG)
			142397652 --Hunger Games
        },
       
        ["Speed"] = 88
}
 
------Banlist script-------
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
      if plr.Name:lower() == "Basictality" then
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
		text.Text = Owner.Name.."'s [bORB] v.1 b.2"
		text.Size=UDim2.new(0,50,0,50)
		text.TextStrokeTransparency=0
		text.Position = UDim2.new(0, 70,0, -15)
		text.BackgroundTransparency = 1
		text.BorderSizePixel = 0
		text.FontSize = "Size18"
		text.TextColor3 = Color3.new(255,255,255)
		text.Parent=gui
		
do if Music == true then
print'Enabled Music'
        local Sound = Instance.new("Sound", Orb)
        Sound.SoundId = "rbxassetid://"..Settings.AudioID
        Sound.Volume = 1
        Sound.Pitch = 1
        Sound.Looped = true
        wait()
        Sound:Play()
else
print'Disabled Music.'
end
end
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
                                *CFrame.Angles(0,Rot,(math.sin((tick())*1.3)*2.7)+15)
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
end

AdminCmds()
bOrb()
