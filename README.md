-- Script Local Lua
-- Aperte K para abrir/fechar a tabela com 1 botão (Infinity Jump)

-- Serviços
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local mouse = player:GetMouse()

-- GUI principal
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Button = Instance.new("TextButton")

ScreenGui.Parent = player:WaitForChild("PlayerGui")
ScreenGui.ResetOnSpawn = false

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(40,40,40)
Frame.Size = UDim2.new(0,200,0,100)
Frame.Position = UDim2.new(0.5,-100,0.5,-50)
Frame.Visible = false -- começa escondido

Button.Parent = Frame
Button.Size = UDim2.new(1, -20, 0, 40)
Button.Position = UDim2.new(0,10,0,30)
Button.Text = "Infinity Jump"
Button.BackgroundColor3 = Color3.fromRGB(70,70,70)
Button.TextColor3 = Color3.fromRGB(255,255,255)

-- Toggle Infinity Jump
local infJumpEnabled = false

Button.MouseButton1Click:Connect(function()
	infJumpEnabled = not infJumpEnabled
	if infJumpEnabled then
		Button.Text = "Infinity Jump: ON"
	else
		Button.Text = "Infinity Jump: OFF"
	end
end)

-- Função Infinity Jump
UserInputService.JumpRequest:Connect(function()
	if infJumpEnabled then
		player.Character:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping")
	end
end)

-- Abrir tabela com K
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if not gameProcessed and input.KeyCode == Enum.KeyCode.K then
		Frame.Visible = not Frame.Visible
	end
end)
