local userKey = "MINHA_CHAVE123" -- ou input do jogador

if userKey ~= "MINHA_CHAVE123" then
    return warn("Chave inválida! Você não pode usar este script.")
end

-- Pega a versão mais nova do GitHub
loadstring(game:HttpGet('https://raw.githubusercontent.com/seu_usuario/seu_repositorio/main/SCRIPT_READ.lua?time='..tick()))()
Fox
