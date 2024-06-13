local lib = loadstring(game:HttpGet"https://raw.githubusercontent.com/dawid-scripts/UI-Libs/main/Vape.txt")()

local win = lib:Window("ailo",Color3.fromRGB(44, 120, 224), Enum.KeyCode.RightControl)

local tab = win:Tab("Main")

tab:Button("Fly", function()
    local plr = game.Players.LocalPlayer
    local mouse = plr:GetMouse()
    
    localplayer = plr
    
    if workspace:FindFirstChild("Core") then
    workspace.Core:Destroy()
    end
    
    local Core = Instance.new("Part")
    Core.Name = "Core"
    Core.Size = Vector3.new(0.05, 0.05, 0.05)
    
    spawn(function()
    Core.Parent = workspace
    local Weld = Instance.new("Weld", Core)
    Weld.Part0 = Core
    Weld.Part1 = localplayer.Character.LowerTorso
    Weld.C0 = CFrame.new(0, 0, 0)
    end)
    
    workspace:WaitForChild("Core")
    
    local torso = workspace.Core
    flying = true
    local speed=10
    local keys={a=false,d=false,w=false,s=false}
    local e1
    local e2
    local function start()
    local pos = Instance.new("BodyPosition",torso)
    local gyro = Instance.new("BodyGyro",torso)
    pos.Name="EPIXPOS"
    pos.maxForce = Vector3.new(math.huge, math.huge, math.huge)
    pos.position = torso.Position
    gyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
    gyro.cframe = torso.CFrame
    repeat
    wait()
    localplayer.Character.Humanoid.PlatformStand=true
    local new=gyro.cframe - gyro.cframe.p + pos.position
    if not keys.w and not keys.s and not keys.a and not keys.d then
    speed=5
    end
    if keys.w then
    new = new + workspace.CurrentCamera.CoordinateFrame.lookVector * speed
    speed=speed+0
    end
    if keys.s then
    new = new - workspace.CurrentCamera.CoordinateFrame.lookVector * speed
    speed=speed+0
    end
    if keys.d then
    new = new * CFrame.new(speed,0,0)
    speed=speed+0
    end
    if keys.a then
    new = new * CFrame.new(-speed,0,0)
    speed=speed+0
    end
    if speed>10 then
    speed=5
    end
    pos.position=new.p
    if keys.w then
    gyro.cframe = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(-math.rad(speed*0),0,0)
    elseif keys.s then
    gyro.cframe = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(math.rad(speed*0),0,0)
    else
    gyro.cframe = workspace.CurrentCamera.CoordinateFrame
    end
    until flying == false
    if gyro then gyro:Destroy() end
    if pos then pos:Destroy() end
    flying=false
    localplayer.Character.Humanoid.PlatformStand=false
    speed=10
    end
    e1=mouse.KeyDown:connect(function(key)
    if not torso or not torso.Parent then flying=false e1:disconnect() e2:disconnect() return end
    if key=="w" then
    keys.w=true
    elseif key=="s" then
    keys.s=true
    elseif key=="a" then
    keys.a=true
    elseif key=="d" then
    keys.d=true
    elseif key=="x" then
    if flying==true then
    flying=false
    else
    flying=true
    start()
    end
    end
    end)
    e2=mouse.KeyUp:connect(function(key)
    if key=="w" then
    keys.w=false
    elseif key=="s" then
    keys.s=false
    elseif key=="a" then
    keys.a=false
    elseif key=="d" then
    keys.d=false
    end
    end)
    start()
lib:Notification("Fly enabled", "yay!", "alright")
end)


tab:Button("macro", function()
    local Player = game:GetService("Players").LocalPlayer
    local Mouse = Player:GetMouse()
    local SpeedGlitch = false
    Mouse.KeyDown:Connect(function(Key)
        if Key == "x" then
            SpeedGlitch = not SpeedGlitch
            if SpeedGlitch == true then
                repeat game:GetService("VirtualInputManager"):SendMouseWheelEvent("0", "0", true, game)
                            wait(0.000001)
                            game:GetService("VirtualInputManager"):SendMouseWheelEvent("0", "0", false, game)
                            wait(0.000001)
                until SpeedGlitch == false
            end
        end
    end)
    lib:Notification("macro enabled", "yay!" , "alright")
end)



tab:Button("low-gfx", function()
    --[[ Anti-Lag Script Boost your fps ]]--
local decalsyeeted = true -- Leaving this on makes games look shitty but the fps goes up by at least 20.
local g = game
local w = g.Workspace
local l = g.Lighting
local t = w.Terrain
t.WaterWaveSize = 0
t.WaterWaveSpeed = 0
t.WaterReflectance = 0
t.WaterTransparency = 0
l.GlobalShadows = false
l.FogEnd = 9e9
l.Brightness = 0
settings().Rendering.QualityLevel = "Level01"
for i, v in pairs(g:GetDescendants()) do
    if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then
        v.Material = "Plastic"
        v.Reflectance = 0
    elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
        v.Transparency = 1
    elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
        v.Lifetime = NumberRange.new(0)
    elseif v:IsA("Explosion") then
        v.BlastPressure = 1
        v.BlastRadius = 1
    elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") then
        v.Enabled = false
    elseif v:IsA("MeshPart") then
        v.Material = "Plastic"
        v.Reflectance = 0
        v.TextureID = 10385902758728957
    end
end
for i, e in pairs(l:GetChildren()) do
    if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
        e.Enabled = false
    end
end
    lib:Notification("low-gfx enabled", "yay!", "alright")
end)


tab:Button("cframe-gui", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/TeamSkid/RobloxScripts/main/neverlose"))()
    lib:Notification("cframe-gui enabled", "yay!", "alright")
end)


tab:Button("backflip-gui", function()
    local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
    local Window = Library.CreateLib("Random Scripts", "Sentinel")
    
    -- MAIN
    local Main = Window:NewTab("Main")
    local MainSection = Main:NewSection("Main")
    
    
    MainSection:NewButton("Front/Back flip", "makes u do flips", function()
      loadstring(game:HttpGet('https://pastebin.com/raw/7wDcPtLk'))()
    end)
    
    
    MainSection:NewToggle("Super-Human", "go superfast and jump rlly high", function(state)
        if state then
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 120
            game.Players.LocalPlayer.Character.Humanoid.JumpPower = 200
        else
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
            game.Players.LocalPlayer.Character.Humanoid.JumpPower = 50
        end
    end)
    
    
    
    MainSection:NewButton("Inf Yield", "Admin Cmds", function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
      end)
    
    --Player
    local Player = Window:NewTab("Player")
    local PlayerSection = Player:NewSection("Player")
    
    PlayerSection:NewSlider("WalkSpeed", "Changes your speed", 500, 16, function(s) -- 500 (MaxValue) | 0 (MinValue)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = s
    end)
    
    PlayerSection:NewSlider("JumpPower", "Changes your speed", 500, 50, function(s) -- 500 (MaxValue) | 0 (MinValue)
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = s
    end)
    
      PlayerSection:NewSlider("Max Health", "Changes your Hp", 999999, 100, function(s) -- 500 (MaxValue) | 0 (MinValue)
        game.Players.LocalPlayer.Character.Humanoid.MaxHealth = s
    end)
    lib:Notification("backflip-gui enabled", "yay!", "alright!")
end)


-- LOCK

local tab = win:Tab("Lock")

tab:Button("camlock", function()
    getgenv().AimPart = "HumanoidRootPart"
	getgenv().AimlockKey = "q"
	getgenv().AimRadius = 30
	getgenv().ThirdPerson = true
	getgenv().FirstPerson = true
	getgenv().TeamCheck = false
	getgenv().PredictMovement = true
	getgenv().PredictionVelocity = 6
	local L_27_, L_28_, L_29_, L_30_ =
            game:GetService "Players",
            game:GetService "UserInputService",
            game:GetService "RunService",
            game:GetService "StarterGui"
	local L_31_, L_32_, L_33_, L_34_, L_35_, L_36_, L_37_ =
            L_27_.LocalPlayer,
            L_27_.LocalPlayer:GetMouse(),
            workspace.CurrentCamera,
            CFrame.new,
            Ray.new,
            Vector3.new,
            Vector2.new
	local L_38_, L_39_, L_40_ = true, false, false
	local L_41_
	getgenv().CiazwareUniversalAimbotLoaded = true
	getgenv().WorldToViewportPoint = function(L_42_arg0)
		return L_33_:WorldToViewportPoint(L_42_arg0)
	end
	getgenv().WorldToScreenPoint = function(L_43_arg0)
		return L_33_.WorldToScreenPoint(L_33_, L_43_arg0)
	end
	getgenv().GetObscuringObjects = function(L_44_arg0)
		if L_44_arg0 and L_44_arg0:FindFirstChild(getgenv().AimPart) and L_31_ and L_31_.Character:FindFirstChild("Head") then
			local L_45_ = workspace:FindPartOnRay(L_35_(L_44_arg0[getgenv().AimPart].Position, L_31_.Character.Head.Position))
			if L_45_ then
				return L_45_:IsDescendantOf(L_44_arg0)
			end
		end
	end
	getgenv().GetNearestTarget = function()
		local L_46_ = {}
		local L_47_ = {}
		local L_48_ = {}
		for L_50_forvar0, L_51_forvar1 in pairs(L_27_:GetPlayers()) do
			if L_51_forvar1 ~= L_31_ then
				table.insert(L_46_, L_51_forvar1)
			end
		end
		for L_52_forvar0, L_53_forvar1 in pairs(L_46_) do
			if L_53_forvar1.Character ~= nil then
				local L_54_ = L_53_forvar1.Character:FindFirstChild("Head")
				if getgenv().TeamCheck == true and L_53_forvar1.Team ~= L_31_.Team then
					local L_55_ =
                            (L_53_forvar1.Character:FindFirstChild("Head").Position - game.Workspace.CurrentCamera.CFrame.p).magnitude
					local L_56_ =
                            Ray.new(
                            game.Workspace.CurrentCamera.CFrame.p,
                            (L_32_.Hit.p - game.Workspace.CurrentCamera.CFrame.p).unit * L_55_
                        )
					local L_57_, L_58_ = game.Workspace:FindPartOnRay(L_56_, game.Workspace)
					local L_59_ = math.floor((L_58_ - L_54_.Position).magnitude)
					L_47_[L_53_forvar1.Name .. L_52_forvar0] = {}
					L_47_[L_53_forvar1.Name .. L_52_forvar0].dist = L_55_
					L_47_[L_53_forvar1.Name .. L_52_forvar0].plr = L_53_forvar1
					L_47_[L_53_forvar1.Name .. L_52_forvar0].diff = L_59_
					table.insert(L_48_, L_59_)
				elseif getgenv().TeamCheck == false and L_53_forvar1.Team == L_31_.Team then
					local L_60_ =
                            (L_53_forvar1.Character:FindFirstChild("Head").Position - game.Workspace.CurrentCamera.CFrame.p).magnitude
					local L_61_ =
                            Ray.new(
                            game.Workspace.CurrentCamera.CFrame.p,
                            (L_32_.Hit.p - game.Workspace.CurrentCamera.CFrame.p).unit * L_60_
                        )
					local L_62_, L_63_ = game.Workspace:FindPartOnRay(L_61_, game.Workspace)
					local L_64_ = math.floor((L_63_ - L_54_.Position).magnitude)
					L_47_[L_53_forvar1.Name .. L_52_forvar0] = {}
					L_47_[L_53_forvar1.Name .. L_52_forvar0].dist = L_60_
					L_47_[L_53_forvar1.Name .. L_52_forvar0].plr = L_53_forvar1
					L_47_[L_53_forvar1.Name .. L_52_forvar0].diff = L_64_
					table.insert(L_48_, L_64_)
				end
			end
		end
		if unpack(L_48_) == nil then
			return nil
		end
		local L_49_ = math.floor(math.min(unpack(L_48_)))
		if L_49_ > getgenv().AimRadius then
			return nil
		end
		for L_65_forvar0, L_66_forvar1 in pairs(L_47_) do
			if L_66_forvar1.diff == L_49_ then
				return L_66_forvar1.plr
			end
		end
		return nil
	end
	L_32_.KeyDown:Connect(
            function(L_67_arg0)
		if L_67_arg0 == AimlockKey and L_41_ == nil then
			pcall(
                        function()
				if L_39_ ~= true then
					L_39_ = true
				end
				local L_68_
				L_68_ = GetNearestTarget()
				if L_68_ ~= nil then
					L_41_ = L_68_
				end
			end
                    )
		elseif L_67_arg0 == AimlockKey and L_41_ ~= nil then
			if L_41_ ~= nil then
				L_41_ = nil
			end
			if L_39_ ~= false then
				L_39_ = false
			end
		end
	end
        )
	L_29_.RenderStepped:Connect(
            function()
		if getgenv().ThirdPerson == true and getgenv().FirstPerson == true then
			if
                        (L_33_.Focus.p - L_33_.CoordinateFrame.p).Magnitude > 1 or
                            (L_33_.Focus.p - L_33_.CoordinateFrame.p).Magnitude <= 1
                     then
				L_40_ = true
			else
				L_40_ = false
			end
		elseif getgenv().ThirdPerson == true and getgenv().FirstPerson == false then
			if (L_33_.Focus.p - L_33_.CoordinateFrame.p).Magnitude > 1 then
				L_40_ = true
			else
				L_40_ = false
			end
		elseif getgenv().ThirdPerson == false and getgenv().FirstPerson == true then
			if (L_33_.Focus.p - L_33_.CoordinateFrame.p).Magnitude <= 1 then
				L_40_ = true
			else
				L_40_ = false
			end
		end
		if L_38_ == true and L_39_ == true then
			if L_41_ and L_41_.Character and L_41_.Character:FindFirstChild(getgenv().AimPart) then
				if getgenv().FirstPerson == true then
					if L_40_ == true then
						if getgenv().PredictMovement == true then
							L_33_.CFrame =
                                        L_34_(
                                        L_33_.CFrame.p,
                                        L_41_.Character[getgenv().AimPart].Position +
                                            L_41_.Character[getgenv().AimPart].Velocity / PredictionVelocity
                                    )
						elseif getgenv().PredictMovement == false then
							L_33_.CFrame = L_34_(L_33_.CFrame.p, L_41_.Character[getgenv().AimPart].Position)
						end
					end
				elseif getgenv().ThirdPerson == true then
					if L_40_ == true then
						if getgenv().PredictMovement == true then
							L_33_.CFrame =
                                        L_34_(
                                        L_33_.CFrame.p,
                                        L_41_.Character[getgenv().AimPart].Position +
                                            L_41_.Character[getgenv().AimPart].Velocity / PredictionVelocity
                                    )
						elseif getgenv().PredictMovement == false then
							L_33_.CFrame = L_34_(L_33_.CFrame.p, L_41_.Character[getgenv().AimPart].Position)
						end
					end
				end
			end
		end
	end)
    lib:Notification("camlock enabled", "yay!", "alright!")
end)
