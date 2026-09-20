🌍 VAELTHORN: LENDAS DO ABISMO — Código Gigante Final

Perfeito! Vou unir TODOS os códigos que criamos em um único jogo épico e colossal:

✅ Mundo aberto 2D com lagos, árvores realistas e ciclo de estações
✅ Sistema de chunks estilo Minecraft (mundo infinito)
✅ 9 companheiros domesticáveis com sprites reais
✅ 5 Chefes + 3 Heróis com design Genshin
✅ Vendedores/NPCs com lojas e itens
✅ Combate por turnos estilo Magic Rampage
✅ Baús, chaves, dungeons e portais
✅ Sistema de equipamento (armas, escudos, armaduras)
✅ HUD polida com minimapa, estações, companheiro ativo
✅ Compêndio completo (Heróis, Chefes, Companheiros, Itens)
✅ Level up, XP, moedas e progressão
✅ Partículas ambientais por estação

---

📁 Estrutura de Pastas

```
📂 Vaelthorn/
├── index.html
└── 📂 img/
    ├── lyra.png          (herói arqueira)
    ├── kael.png          (herói tanque)
    ├── nyx.png           (herói maga)
    ├── vorthak.png       (chefe dragão)
    ├── olho-umbra.png    (chefe olho)
    ├── rei-kharon.png    (chefe morto-vivo)
    ├── sylvaneth.png     (chefe árvore)
    ├── aeternum.png      (chefe final)
    ├── coruja.png  • aguia.png  • cavalo.png
    ├── cao.png     • gato.png   • raposa.png
    └── touro.png   • porco.png  • cordeiro.png
```

Se faltar alguma imagem, o sistema usa emoji automático. 🐾

---

🎮 Código Completo (index.html)

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Vaelthorn: Lendas do Abismo — RPG 2D de mundo aberto com estações, companheiros, chefes, vendedores e dungeons.">
<title>✦ VAELTHORN — Lendas do Abismo ✦</title>
<style>
  /* ============================================================
     RESET E BASE
     ============================================================ */
  * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', system-ui, -apple-system, sans-serif; -webkit-tap-highlight-color: transparent; user-select: none; }

  :root {
    --ouro: #ffd700;
    --ouro-claro: #ffed4e;
    --roxo: #7c3aed;
    --roxo-claro: #a78bfa;
    --azul-profundo: #0f172a;
    --vermelho: #dc143c;
    --verde: #10b981;
    --borda: rgba(255,255,255,0.12);
    --sombra: 0 15px 40px rgba(0,0,0,0.5);
    --ceu-topo: #0f172a;
    --ceu-meio: #1e293b;
    --ceu-base: #311b92;
    --cor-particula: #a78bfa;
  }

  html, body { width: 100%; height: 100%; overflow: hidden; background: #0b0f19; color: #fff; }

  ::-webkit-scrollbar { width: 10px; }
  ::-webkit-scrollbar-track { background: rgba(0,0,0,0.3); }
  ::-webkit-scrollbar-thumb { background: linear-gradient(180deg, var(--ouro), #b8860b); border-radius: 10px; }

  #gameCanvas { display: block; position: absolute; inset: 0; z-index: 1; cursor: crosshair; }

  /* ============================================================
     HUD JOGADOR
     ============================================================ */
  .hud-jogador {
    position: fixed; top: 20px; left: 20px; z-index: 10;
    background: rgba(10,15,30,0.88);
    border: 1px solid rgba(255,215,0,0.4);
    border-radius: 18px;
    padding: 14px 18px;
    backdrop-filter: blur(12px);
    box-shadow: 0 10px 40px rgba(0,0,0,0.7), 0 0 30px rgba(255,215,0,0.1);
    min-width: 280px;
  }

  .hud-jogador .topo { display: flex; align-items: center; justify-content: space-between; margin-bottom: 10px; }

  .hud-jogador .avatar {
    width: 46px; height: 46px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--roxo), var(--roxo-claro));
    display: flex; align-items: center; justify-content: center;
    font-size: 1.6rem;
    border: 2px solid var(--ouro);
    box-shadow: 0 0 15px rgba(255,215,0,0.4);
    overflow: hidden;
  }
  .hud-jogador .avatar img { width: 100%; height: 100%; object-fit: cover; }

  .hud-jogador .info { flex: 1; margin-left: 12px; }
  .hud-jogador .nome { font-size: 0.9rem; font-weight: bold; color: #ffe680; letter-spacing: 0.5px; }
  .hud-jogador .nivel { font-size: 0.72rem; color: #a0a0c0; }

  .hud-jogador .barra {
    width: 100%; height: 10px;
    background: rgba(0,0,0,0.6);
    border-radius: 6px;
    overflow: hidden;
    margin-bottom: 5px;
    border: 1px solid rgba(255,255,255,0.1);
  }

  .hud-jogador .barra-fill {
    height: 100%;
    border-radius: 6px;
    transition: width 0.4s ease;
  }

  .barra-hp .barra-fill { background: linear-gradient(90deg, #dc143c, #ff6b6b); box-shadow: 0 0 10px rgba(220,20,60,0.6); }
  .barra-xp .barra-fill { background: linear-gradient(90deg, #7c3aed, #a78bfa); box-shadow: 0 0 10px rgba(124,58,237,0.6); }
  .barra-mana .barra-fill { background: linear-gradient(90deg, #2563eb, #60a5fa); box-shadow: 0 0 10px rgba(37,99,235,0.6); }

  .hud-jogador .texto-barra {
    display: flex; justify-content: space-between;
    font-size: 0.7rem; color: #b0b0d0;
    margin-bottom: 5px;
  }

  .hud-jogador .extras {
    display: flex; gap: 10px; margin-top: 8px;
    font-size: 0.72rem;
  }
  .hud-jogador .extra-item {
    background: rgba(0,0,0,0.4);
    border-radius: 8px;
    padding: 4px 10px;
    display: flex; align-items: center; gap: 4px;
    color: #ffd700;
  }

  /* ============================================================
     HUD CHAVES / MOEDAS
     ============================================================ */
  .hud-recursos {
    position: fixed; top: 20px; right: 180px; z-index: 10;
    background: rgba(10,15,30,0.88);
    border: 1px solid rgba(255,215,0,0.5);
    border-radius: 18px;
    padding: 12px 16px;
    backdrop-filter: blur(12px);
    box-shadow: 0 10px 40px rgba(0,0,0,0.7);
    display: flex; gap: 16px;
  }

  .recurso {
    display: flex; align-items: center; gap: 8px;
  }

  .recurso .icone {
    width: 36px; height: 36px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.1rem;
    color: #2a1a00;
    font-weight: bold;
  }

  .recurso.chave .icone { background: linear-gradient(135deg, #ffd700, #b8860b); box-shadow: 0 0 20px rgba(255,215,0,0.6); }
  .recurso.moeda .icone { background: linear-gradient(135deg, #fbbf24, #f59e0b); box-shadow: 0 0 20px rgba(251,191,36,0.6); }
  .recurso .contador { font-size: 1.3rem; font-weight: bold; color: #ffd700; }
  .recurso .label { font-size: 0.65rem; color: #a0a0c0; letter-spacing: 1px; }

  /* ============================================================
     HUD ESTAÇÃO
     ============================================================ */
  .hud-estacao {
    position: fixed; bottom: 20px; left: 20px; z-index: 10;
    background: rgba(10,15,30,0.88);
    border: 1px solid rgba(255,215,0,0.4);
    border-radius: 18px;
    padding: 12px 18px;
    backdrop-filter: blur(12px);
    box-shadow: 0 10px 40px rgba(0,0,0,0.7);
    min-width: 230px;
  }

  .hud-estacao .topo { display: flex; align-items: center; gap: 10px; margin-bottom: 6px; }
  .hud-estacao .icone { font-size: 1.8rem; animation: flutuar 3s ease-in-out infinite; }
  @keyframes flutuar { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-4px); } }
  .hud-estacao .nome { font-size: 1rem; font-weight: bold; color: #ffd700; }
  .hud-estacao .track { height: 6px; background: rgba(0,0,0,0.6); border-radius: 6px; overflow: hidden; margin-bottom: 4px; }
  .hud-estacao .fill { height: 100%; background: linear-gradient(90deg, #ffd700, #ff8c00); border-radius: 6px; width: 0%; transition: width 1s linear; }
  .hud-estacao .tempo { font-size: 0.7rem; color: #ffd700; text-align: right; font-weight: bold; }

  /* ============================================================
     HUD COMPANHEIRO
     ============================================================ */
  .hud-companheiro {
    position: fixed; bottom: 20px; right: 20px; z-index: 10;
    background: rgba(10,15,30,0.88);
    border: 1px solid rgba(167,139,250,0.5);
    border-radius: 18px;
    padding: 12px 16px;
    backdrop-filter: blur(12px);
    box-shadow: 0 10px 40px rgba(0,0,0,0.7);
    display: flex; align-items: center; gap: 12px;
    min-width: 220px;
  }

  .hud-companheiro .sprite {
    width: 52px; height: 52px;
    border-radius: 12px;
    background: rgba(0,0,0,0.4);
    display: flex; align-items: center; justify-content: center;
    font-size: 2rem;
    border: 1px solid rgba(167,139,250,0.4);
    overflow: hidden;
  }
  .hud-companheiro .sprite img { width: 100%; height: 100%; object-fit: contain; padding: 2px; }

  .hud-companheiro .info { flex: 1; }
  .hud-companheiro .nome { font-size: 0.8rem; font-weight: bold; color: #c4b5fd; }
  .hud-companheiro .habs { font-size: 0.65rem; color: #a0a0c0; margin-top: 2px; }
  .hud-companheiro .barra-mini { height: 4px; background: rgba(0,0,0,0.5); border-radius: 4px; overflow: hidden; margin-top: 4px; }
  .hud-companheiro .barra-mini-fill { height: 100%; background: linear-gradient(90deg, #a78bfa, #c4b5fd); border-radius: 4px; width: 100%; }

  /* ============================================================
     MINI-MAPA
     ============================================================ */
  .minimapa {
    position: fixed; top: 20px; right: 20px; z-index: 10;
    width: 150px; height: 150px;
    border-radius: 50%;
    background: rgba(10,15,30,0.88);
    border: 2px solid rgba(255,215,0,0.5);
    overflow: hidden;
    box-shadow: 0 10px 40px rgba(0,0,0,0.7), inset 0 0 20px rgba(0,0,0,0.8);
    backdrop-filter: blur(10px);
  }

  .minimapa canvas { width: 100%; height: 100%; }

  /* ============================================================
     CONTROLES DE BATALHA
     ============================================================ */
  .controles-batalha {
    position: fixed; bottom: 130px; left: 50%; transform: translateX(-50%);
    z-index: 20;
    display: none;
    gap: 12px;
    background: rgba(5,10,20,0.95);
    padding: 18px 26px;
    border-radius: 22px;
    border: 2px solid #dc143c;
    box-shadow: 0 0 40px rgba(220,20,60,0.5), inset 0 0 30px rgba(220,20,60,0.1);
    backdrop-filter: blur(15px);
    flex-wrap: wrap;
    justify-content: center;
    max-width: 90vw;
  }

  .controles-batalha.ativo { display: flex; }

  .botao-acao {
    padding: 12px 22px;
    font-size: 0.9rem;
    font-weight: bold;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.15s ease;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: #fff;
    box-shadow: 0 4px 0 rgba(0,0,0,0.5);
    display: flex;
    align-items: center;
    gap: 6px;
    font-family: inherit;
  }

  .botao-acao:active { transform: translateY(4px); box-shadow: 0 0 0; }
  .botao-acao:disabled { opacity: 0.4; cursor: not-allowed; }

  .botao-atacar { background: linear-gradient(135deg, #e74c3c, #c0392b); }
  .botao-atacar:hover:not(:disabled) { background: linear-gradient(135deg, #ff5545, #d63c2b); }
  .botao-curar { background: linear-gradient(135deg, #2ecc71, #27ae60); }
  .botao-curar:hover:not(:disabled) { background: linear-gradient(135deg, #3fe082, #2fc070); }
  .botao-habilidade { background: linear-gradient(135deg, #7c3aed, #5b21b6); }
  .botao-habilidade:hover:not(:disabled) { background: linear-gradient(135deg, #8b4ef0, #6b28c0); }
  .botao-fugir { background: linear-gradient(135deg, #f39c12, #d35400); }
  .botao-fugir:hover:not(:disabled) { background: linear-gradient(135deg, #ffac2a, #e36400); }

  /* ============================================================
     INFO INIMIGO
     ============================================================ */
  .info-inimigo {
    position: fixed; top: 80px; left: 50%; transform: translateX(-50%);
    z-index: 20;
    background: rgba(10,15,30,0.92);
    border: 2px solid #dc143c;
    border-radius: 18px;
    padding: 12px 24px;
    backdrop-filter: blur(12px);
    display: none;
    min-width: 340px;
    text-align: center;
    box-shadow: 0 0 40px rgba(220,20,60,0.5);
  }

  .info-inimigo.ativo { display: block; }

  .info-inimigo .nome {
    color: #ff8080;
    font-size: 1.1rem;
    font-weight: bold;
    margin-bottom: 8px;
    letter-spacing: 1px;
    text-shadow: 0 0 15px rgba(220,20,60,0.6);
  }

  .info-inimigo .hp-barra {
    height: 12px; background: rgba(0,0,0,0.7);
    border-radius: 6px; overflow: hidden;
    border: 1px solid rgba(220,20,60,0.5);
  }

  .info-inimigo .hp-fill {
    height: 100%;
    background: linear-gradient(90deg, #dc143c, #8b0a1a);
    border-radius: 6px;
    transition: width 0.4s ease;
    box-shadow: 0 0 15px rgba(220,20,60,0.8);
  }

  .info-inimigo .hp-texto { font-size: 0.75rem; color: #ff8080; margin-top: 4px; font-weight: bold; }

  /* ============================================================
     LOG MENSAGENS
     ============================================================ */
  .log-mensagens {
    position: fixed; bottom: 230px; left: 50%; transform: translateX(-50%);
    z-index: 15;
    display: flex; flex-direction: column;
    align-items: center;
    gap: 6px;
    pointer-events: none;
    max-width: 90vw;
  }

  .mensagem {
    background: rgba(10,15,30,0.95);
    border: 1px solid rgba(255,215,0,0.4);
    border-radius: 20px;
    padding: 8px 20px;
    color: #ffd700;
    font-size: 0.85rem;
    font-weight: bold;
    backdrop-filter: blur(10px);
    box-shadow: 0 4px 15px rgba(0,0,0,0.6);
    animation: slideUp 0.4s ease;
    white-space: nowrap;
    max-width: 100%;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

  /* ============================================================
     INVENTÁRIO (hotbar)
     ============================================================ */
  .hotbar {
    position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
    z-index: 15;
    display: flex; gap: 8px;
    background: rgba(10,15,30,0.85);
    padding: 8px;
    border-radius: 14px;
    border: 2px solid rgba(255,215,0,0.4);
    backdrop-filter: blur(10px);
    box-shadow: 0 10px 30px rgba(0,0,0,0.6);
  }

  .slot-hotbar {
    width: 54px; height: 54px;
    background: rgba(255,255,255,0.06);
    border: 2px solid rgba(255,255,255,0.15);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.8rem;
    cursor: pointer;
    transition: all 0.2s;
    position: relative;
  }

  .slot-hotbar:hover { border-color: #ffd700; transform: translateY(-3px); }
  .slot-hotbar.selecionado { border-color: #ffd700; background: rgba(255,215,0,0.15); box-shadow: 0 0 15px rgba(255,215,0,0.4); }
  .slot-hotbar .qtd {
    position: absolute; bottom: 2px; right: 4px;
    font-size: 0.65rem; color: #fff; font-weight: bold;
    background: rgba(0,0,0,0.7); padding: 1px 5px; border-radius: 8px;
  }
  .slot-hotbar .num {
    position: absolute; top: 2px; left: 4px;
    font-size: 0.6rem; color: #a0a0c0;
  }

  /* ============================================================
     BOTÕES RÁPIDOS
     ============================================================ */
  .acoes-rapidas {
    position: fixed; top: 190px; right: 20px; z-index: 10;
    display: flex; flex-direction: column; gap: 10px;
  }

  .botao-rapido {
    width: 52px; height: 52px;
    border-radius: 50%;
    background: rgba(15,23,42,0.9);
    border: 1px solid rgba(255,215,0,0.5);
    color: #ffd700;
    font-size: 1.4rem;
    cursor: pointer;
    transition: all 0.3s;
    display: flex; align-items: center; justify-content: center;
    backdrop-filter: blur(10px);
    box-shadow: 0 6px 20px rgba(0,0,0,0.5);
  }

  .botao-rapido:hover {
    background: #ffd700; color: #1a1a1a;
    transform: scale(1.12);
    box-shadow: 0 0 25px rgba(255,215,0,0.7);
  }

  /* ============================================================
     MODAIS
     ============================================================ */
  .modal-overlay {
    position: fixed; inset: 0;
    background: rgba(0,0,0,0.85);
    backdrop-filter: blur(10px);
    z-index: 100;
    display: none;
    align-items: center;
    justify-content: center;
    padding: 20px;
    animation: fadeIn 0.3s ease;
  }

  .modal-overlay.ativo { display: flex; }

  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

  .modal-caixa {
    background: linear-gradient(160deg, #1e293b, #0f172a);
    border: 2px solid var(--ouro);
    border-radius: 22px;
    max-width: 720px;
    width: 100%;
    max-height: 85vh;
    overflow-y: auto;
    padding: 32px;
    position: relative;
    box-shadow: 0 20px 60px rgba(0,0,0,0.9), 0 0 60px rgba(255,215,0,0.2);
    animation: scaleIn 0.35s cubic-bezier(.4,0,.2,1);
  }

  @keyframes scaleIn { from { transform: scale(0.9); opacity: 0; } to { transform: scale(1); opacity: 1; } }

  .modal-titulo { color: #ffd700; font-size: 1.4rem; margin-bottom: 8px; text-align: center; letter-spacing: 1px; }
  .modal-sub { text-align: center; color: #a0a0c0; font-size: 0.85rem; margin-bottom: 20px; font-style: italic; }

  .modal-botao {
    display: block;
    margin: 20px auto 0;
    padding: 12px 32px;
    font-size: 0.95rem;
    font-weight: bold;
    background: linear-gradient(135deg, var(--ouro), #ffb800);
    color: #2a1a00;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.2s;
    box-shadow: 0 4px 15px rgba(255,215,0,0.4);
    letter-spacing: 0.5px;
  }
  .modal-botao:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(255,215,0,0.6); }

  /* Loja */
  .loja-item {
    display: flex; justify-content: space-between; align-items: center;
    padding: 12px 16px;
    margin: 8px 0;
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.25s;
  }

  .loja-item:hover { background: rgba(255,215,0,0.12); border-color: rgba(255,215,0,0.5); transform: translateX(4px); }

  .loja-item .esquerda { display: flex; align-items: center; gap: 12px; }
  .loja-item .icon { font-size: 1.8rem; }
  .loja-item .nome { color: #fff; font-size: 0.9rem; font-weight: 600; }
  .loja-item .tipo { color: #a0a0c0; font-size: 0.7rem; font-style: italic; }
  .loja-item .preco { color: #ffd700; font-weight: bold; font-size: 0.9rem; }
  .loja-item .preco.caro { color: #ff5555; }

  /* Compêndio abas */
  .compendio-abas { display: flex; flex-wrap: wrap; gap: 6px; justify-content: center; margin-bottom: 20px; }
  .compendio-aba {
    padding: 8px 16px;
    background: rgba(255,255,255,0.06);
    border: 1px solid var(--borda);
    color: #c0c0e0;
    border-radius: 20px;
    cursor: pointer;
    font-size: 0.8rem;
    transition: all 0.25s;
  }
  .compendio-aba.ativa { background: linear-gradient(135deg, var(--ouro), #ffb800); color: #2a1a00; font-weight: bold; }
  .compendio-aba:hover:not(.ativa) { border-color: var(--ouro); color: var(--ouro); }

  .compendio-conteudo { max-height: 55vh; overflow-y: auto; padding-right: 8px; }

  .compendio-card {
    background: rgba(0,0,0,0.3);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 12px;
    padding: 14px 16px;
    margin-bottom: 10px;
    display: flex; gap: 14px; align-items: center;
    transition: all 0.3s;
  }

  .compendio-card:hover { border-color: rgba(255,215,0,0.5); transform: translateX(4px); background: rgba(255,215,0,0.05); }

  .compendio-sprite {
    width: 64px; height: 64px;
    border-radius: 12px;
    background: rgba(0,0,0,0.4);
    display: flex; align-items: center; justify-content: center;
    font-size: 2rem;
    flex-shrink: 0;
    overflow: hidden;
    border: 1px solid rgba(255,215,0,0.3);
  }
  .compendio-sprite img { width: 100%; height: 100%; object-fit: contain; }

  .compendio-info h4 { color: #ffe680; font-size: 0.95rem; margin-bottom: 3px; }
  .compendio-info p { color: #a0a0c0; font-size: 0.78rem; line-height: 1.4; }

  /* Companheiros grid */
  .companheiros-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 12px; margin-top: 16px; }
  .companheiro-opcao
