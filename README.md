-- BackAura
local HeraBattlegrounds = Instance.new("ScreenGui")
local TopBg = Instance.new("Frame")
local UIGradient = Instance.new("UIGradient")
local Body = Instance.new("Frame")
local UIGradient_2 = Instance.new("UIGradient")
local BlockAura = Instance.new("TextButton")
local UICorner = Instance.new("UICorner")
local minimize = Instance.new("ImageButton")
local TextLabel = Instance.new("TextLabel")
 
--Properties:
 
HeraBattlegrounds.Name = "HeraBattlegrounds"
HeraBattlegrounds.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
HeraBattlegrounds.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
HeraBattlegrounds.ResetOnSpawn = false
 
TopBg.Name = "TopBg"
TopBg.Parent = HeraBattlegrounds
TopBg.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TopBg.BorderColor3 = Color3.fromRGB(27, 42, 53)
TopBg.BorderSizePixel = 0
TopBg.Position = UDim2.new(0.267471403, 0, 0.242474914, 0)
TopBg.Size = UDim2.new(0, 142, 0, 21)
 
UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(137, 0, 254)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(223, 0, 255))}
UIGradient.Parent = TopBg
 
Body.Name = "Body"
Body.Parent = TopBg
Body.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Body.BorderColor3 = Color3.fromRGB(27, 42, 53)
Body.BorderSizePixel = 0
Body.Position = UDim2.new(0, 0, 0.976190448, 0)
Body.Size = UDim2.new(0, 142, 0, 37)
 
UIGradient_2.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(55, 0, 103)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(223, 0, 255))}
UIGradient_2.Parent = Body
 
BlockAura.Name = "BlockAura"
BlockAura.Parent = Body
BlockAura.BackgroundColor3 = Color3.fromRGB(43, 41, 83)
BlockAura.BackgroundTransparency = 0.250
BlockAura.BorderSizePixel = 0
BlockAura.Position = UDim2.new(0, 0, 0.151454702, 0)
BlockAura.Size = UDim2.new(0, 142, 0, 24)
BlockAura.Font = Enum.Font.SourceSansBold
BlockAura.Text = "BlockAura: OFF"
BlockAura.TextColor3 = Color3.fromRGB(255, 98, 140)
BlockAura.TextSize = 14.000
 
UICorner.CornerRadius = UDim.new(1, 8)
UICorner.Parent = BlockAura
 
minimize.Name = "minimize"
minimize.Parent = TopBg
minimize.BackgroundTransparency = 1.000
minimize.Position = UDim2.new(0.823943675, 0, -0.119047642, 0)
minimize.Size = UDim2.new(0, 25, 0, 25)
minimize.ZIndex = 2
minimize.Image = "rbxassetid://3926307971"
minimize.ImageRectOffset = Vector2.new(164, 484)
minimize.ImageRectSize = Vector2.new(36, 36)
 
TextLabel.Parent = TopBg
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.BorderSizePixel = 0
TextLabel.Size = UDim2.new(0, 142, 0, 20)
TextLabel.Font = Enum.Font.SourceSansBold
TextLabel.Text = "SB by firelegodogs"
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.TextSize = 15.000
 
-- Scripts:
 
local function JLXHHH_fake_script() -- BlockAura.BlockAura 
	local script = Instance.new('LocalScript', BlockAura)
 
	local Usuario = game:GetService("Players").LocalPlayer
 
	function Blocking()
		local args = {
			[1] = {
				["Goal"] = "KeyPress",
				["Key"] = Enum.KeyCode.F
			}
		}
		game:GetService("Players").LocalPlayer.Character.Communicate:FireServer(unpack(args))
	end
 
	function Unblock()
		local args = {
			[1] = {
				["Goal"] = "KeyRelease",
				["Key"] = Enum.KeyCode.F
			}
		}
		game:GetService("Players").LocalPlayer.Character.Communicate:FireServer(unpack(args))
	end
 
	_G.BlockAura = false
	script.Parent.MouseButton1Click:Connect(function()
		if _G.BlockAura == false then
			_G.BlockAura = true
			script.Parent.TextColor3 = Color3.fromRGB(76, 241, 46)
			script.Parent.Text = "BlockAura: ON"
			while _G.BlockAura do
				local closestDistance = math.huge
				local closestPlayer = nil
 
				for i,v in next, game:GetService("Players"):GetPlayers() do
					if (v ~= Usuario and Usuario.Character and Usuario.Character:FindFirstChild("HumanoidRootPart") and v.Character and v.Character:FindFirstChild("HumanoidRootPart")) then
						local distance = (v.Character.HumanoidRootPart.Position - Usuario.Character.HumanoidRootPart.Position).magnitude
 
						if (distance < closestDistance and distance <= 17) then -- Verificando se é o jogador mais próximo e se ele está dentro da distância permitida
							closestDistance = distance
							closestPlayer = v
						end
					end
				end
 
				if closestPlayer then
					Blocking()
					local playerPosition = closestPlayer.Character.HumanoidRootPart
					Usuario.Character.HumanoidRootPart.CFrame = playerPosition.CFrame * CFrame.new(0, 0, 3)
					Unblock()
				end
				wait()
			end
		else
			_G.BlockAura = false
			script.Parent.TextColor3 = Color3.fromRGB(255, 98, 140)
			script.Parent.Text = "BlockAura: OFF"
		end
	end)
 
	local UIB = game:GetService("UserInputService")
	UIB.InputBegan:Connect(function(tecla,gameprocess)
		if not gameprocess then
			if tecla.KeyCode == Enum.KeyCode.LeftControl then
				if _G.BlockAura == false then
					_G.BlockAura = true
					script.Parent.TextColor3 = Color3.fromRGB(76, 241, 46)
					script.Parent.Text = "BlockAura: ON"
					while _G.BlockAura do
						local closestDistance = math.huge
						local closestPlayer = nil
 
						for i,v in next, game:GetService("Players"):GetPlayers() do
							if (v ~= Usuario and Usuario.Character and Usuario.Character:FindFirstChild("HumanoidRootPart") and v.Character and v.Character:FindFirstChild("HumanoidRootPart")) then
								local distance = (v.Character.HumanoidRootPart.Position - Usuario.Character.HumanoidRootPart.Position).magnitude
 
								if (distance < closestDistance and distance <= 17) then -- Verificando se é o jogador mais próximo e se ele está dentro da distância permitida
									closestDistance = distance
									closestPlayer = v
								end
							end
						end
 
						if closestPlayer then
							Blocking()
							local playerPosition = closestPlayer.Character.HumanoidRootPart
							Usuario.Character.HumanoidRootPart.CFrame = playerPosition.CFrame * CFrame.new(0, 0, 3)
							Unblock()
						end
						wait()
					end
				else
					_G.BlockAura = false
					script.Parent.TextColor3 = Color3.fromRGB(255, 98, 140)
					script.Parent.Text = "BlockAura: OFF"
				end
			end
		end
	end)
end
coroutine.wrap(JLXHHH_fake_script)()
local function IECHPZY_fake_script() -- minimize.LocalScript 
	local script = Instance.new('LocalScript', minimize)
 
	script.Parent.MouseButton1Click:Connect(function()
		script.Parent.Parent.Body.Visible = not script.Parent.Parent.Body.Visible
	end)
end
coroutine.wrap(IECHPZY_fake_script)()
local function JHSE_fake_script() -- TopBg.Drag 
	local script = Instance.new('LocalScript', TopBg)
 
	local UserInputService = game:GetService("UserInputService")
	local gui = script.Parent
	local dragging
	local dragInput
	local dragStart
	local startPos
 
	local function update(input)
		local delta = input.Position - dragStart
		gui.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end
 
	gui.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPos = gui.Position
 
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)
 
	gui.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)
 
	UserInputService.InputChanged:Connect(function(input)
		if input == dragInput and dragging then
			update(input)
		end
	end)
end
coroutine.wrap(JHSE_fake_script)()
local function KMSN_fake_script() -- TopBg.ToggleUI 
	local script = Instance.new('LocalScript', TopBg)
 
	local UIS = game:GetService("UserInputService")
	UIS.InputBegan:Connect(function(tecla,gameprocess)
		if not gameprocess then
			if tecla.KeyCode == Enum.KeyCode.RightControl then
				script.Parent.Parent.TopBg.Visible = not script.Parent.Parent.TopBg.Visible
			end
		end
	end)
end
coroutine.wrap(KMSN_fake_script)()
