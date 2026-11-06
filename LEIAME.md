# Glup! — Caça no Labirinto

Jogo de labirinto para navegador (celular e computador), em um único arquivo: `index.html`.

## Modos
- **1 jogador**
- **2 no mesmo aparelho**: cada um com seu controle na tela (ou teclado: Glup = WASD, Blup = setas)
- **Contra 3 bots**: você contra o computador
- **Online (até 4)**: quem cria a sala manda o link (ou o código de 5 letras) para até 3 amigos.
  Antes de começar, o anfitrião escolhe se as vagas livres serão completadas com bots.
  Se alguém sair no meio da partida, o personagem dele vira bot e o jogo continua.

Personagens: Glup (verde), Blup (roxo), Plup (amarelo) e Tlup (branco).
Cada jogador pode digitar o próprio nome (até 12 letras), que aparece no placar,
na sala online, no resumo final, no placar de vitórias e no recorde.

A cada fase o labirinto muda (Neon → Jardim → Cristal → Vulcão → recomeça mais rápido).
A cada 1000 pontos, +1 vida (máximo 6). Com 6 vidas, cada 1000 pontos vale +200 de bônus.
Turbinado, você pode trombar num rival, roubar 500 pontos e deixá-lo tonto por 5 segundos.
Com 2 ou mais jogadores, quem perde todas as vidas vira besouro: continua jogando, persegue os
outros e ganha +500 por jogador que pegar. Turbinado, dá para mandar esse besouro de volta à toca (+200).
A partida termina quando não sobra ninguém vivo.

## Como o online funciona
Usa WebRTC via [PeerJS](https://peerjs.com): os dois aparelhos se conectam direto.
O servidor gratuito público do PeerJS só faz a "apresentação" inicial. Por isso não
precisa de servidor próprio: basta hospedar o `index.html` em qualquer site estático.

O aparelho de quem cria a sala roda o jogo; o convidado envia os comandos e recebe a tela.

Limitações:
- O servidor público do PeerJS é gratuito e sem garantia. Se ele cair, o online não conecta
  (o jogo local continua funcionando).
- Em algumas redes muito restritas (Wi-Fi corporativo, certas operadoras), a conexão direta
  pode falhar.
- O link da sala só funciona com o jogo hospedado (não funciona abrindo o arquivo local).

## Hospedar de graça

### Opção 1: Netlify Drop (mais fácil, sem instalar nada)
1. Acesse https://app.netlify.com/drop
2. Arraste a pasta do jogo (com o `index.html`) para a página
3. Pronto: você recebe um endereço `https://nome-aleatorio.netlify.app`
   (crie uma conta grátis para o site não expirar e poder trocar o nome)

### Opção 2: GitHub Pages
```bash
cd jogo01
git init && git add index.html LEIAME.md && git commit -m "Glup!"
gh repo create glup --public --source=. --push
gh api repos/{dono}/glup/pages -X POST -f "source[branch]=main" -f "source[path]=/"
```
O jogo fica em `https://{dono}.github.io/glup/` (leva 1–2 minutos na primeira vez).

Para atualizar depois: `git commit -am "ajustes" && git push`.

## Testar localmente
```bash
python3 -m http.server 8000
```
Abra `http://localhost:8000` (ou `http://IP-DO-PC:8000` no celular, na mesma rede Wi-Fi).
