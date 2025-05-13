local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/jensonhirst/Orion/refs/heads/main/source')))()
local Player = game.Players.LocalPlayer

local Window = OrionLib:MakeWindow({
	Name = "Key System",
	HidePremium = false,
	SaveConfig = true,
	ConfigFolder = "KeySystem",
	IntroText = "Verificando Chave..."
})

getgenv().Key = "teste"
getgenv().KeyInput = ""

-- Lista de jogadores permitidos (WhiteList)
local WhiteList = {
	"Franciscogames438",
	"TOM360584",
  "Vacalebrenj",
	"AliceVitoriaMig",
}

local Tab = Window:MakeTab({
	Name = "Key",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Tab:AddTextbox({
	Name = "Insira a Chave",
	Default = "",
	TextDisappear = true,
	Callback = function(Value)
		getgenv().KeyInput = Value
	end
})

local function executarScript()
	OrionLib:MakeNotification({
		Name = "Sucesso!",
		Content = "Chave correta ou acesso WhiteList! Script carregado.",
		Image = "rbxassetid://0",
		Time = 5
	})
	wait(1)
	OrionLib:Destroy()
	wait(0.3)
	-- Adicione o seu script aqui
	print("bote seu script aqui")
end

Tab:AddButton({
	Name = "Verificar Chave",
	Callback = function()
		if getgenv().KeyInput == getgenv().Key then
			executarScript()
		else
			OrionLib:MakeNotification({
				Name = "Erro!",
				Content = "Chave incorreta. Tente novamente.",
				Image = "rbxassetid://0",
				Time = 5
			})
		end
	end
})

Tab:AddButton({
	Name = "WhiteList {ENTRADA DIRETA}",
	Callback = function()
		local playerNick = Player.Name

 	local isInWhiteList = false
		for _, whitelistedName in ipairs(WhiteList) do
			if playerNick == whitelistedName then
				isInWhiteList = true
				break
			end
		end

		if isInWhiteList then
			executarScript()
		else
			Player:Kick("Você não tá na White list")
		end
	end
})

OrionLib:Init()
