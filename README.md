-- Carregar OrionLib
local OrionLib = loadstring(game:HttpGet("https://pastefy.app/ELS4VXA7/raw"))()

-- Criar janela
local Window = OrionLib:MakeWindow({Name = "Menu de Jumpscare"})

-- Aba Jumpscares
local TabJumpscare = Window:MakeTab({Name = "Jumpscares"})

-- Loadstring do jumpscare (do seu primeiro gist)
local jumpscareCode = [[
    loadstring(game:HttpGet("https://gist.githubusercontent.com/matheusrafael99175-collab/3e2b7a2dcbd00cebe420f42b611feef6/raw/c7f6ccab1eef84a3ed3f17119a036c152273790a/gistfile1.txt"))()
]]

-- Botão que executa o jumpscare
TabJumpscare:AddButton({
    Name = "Jumpscare Scary loop",
    Callback = function()
        loadstring(jumpscareCode)()
    end
})

-- Nova aba Volume GUI
local TabVolume = Window:MakeTab({Name = "Volume GUI"})

-- Loadstring do Volume GUI (segundo gist)
local volumeGUICode = [[
    loadstring(game:HttpGet("https://gist.githubusercontent.com/matheusrafael99175-collab/f569ce78415558d85a11361d7b707412/raw/4bf0c5c6843b021f38130b18c572c368d56c4fdf/volumeGUI.lua"))()
]]

-- Botão que executa o Volume GUI
TabVolume:AddButton({
    Name = "Carregar Volume GUI",
    Callback = function()
        loadstring(volumeGUICode)()
    end
})
