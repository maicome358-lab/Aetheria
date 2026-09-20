✦ VAELTHORN — Código Completo Unificado ✦

Aqui está TODOS os sistemas juntos em um único arquivo pronto para uso:

· 🌍 Mundo + 5 Regiões
· 🌸 Ciclo de 4 Estações (5h cada) com árvores que mudam
· ⚔️ 3 Heróis + 👹 5 Chefes
· 🐾 9 Companheiros domesticáveis com imagens reais
· 🛡️ Sistema de Equipamento para Companheiros
· 🗡️ Itens Lendários
· 🏰 Dungeons + 🌀 Portais + 🗝️ Chaves

📁 Instruções rápidas

Antes de usar, salve as 9 imagens dos animais na mesma pasta do HTML com estes nomes exatos:

```
coruja.png  • aguia.png  • cavalo.png
cao.png     • gato.png   • raposa.png
touro.png   • porco.png  • cordeiro.png
```

Se alguma faltar, o emoji aparece automaticamente como fallback. ✨

---

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Vaelthorn — RPG 2D com estações, portais, dungeons, chefes épicos e companheiros domesticáveis.">
<meta name="theme-color" content="#0f172a">
<title>✦ VAELTHORN — O Mundo e as Lendas ✦</title>
<style>
  /* ============================================================
     RESET E BASE
     ============================================================ */
  * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', system-ui, -apple-system, sans-serif; -webkit-tap-highlight-color: transparent; }

  :root {
    --ouro: #ffd700;
    --ouro-claro: #ffed4e;
    --roxo: #7c3aed;
    --roxo-claro: #a78bfa;
    --azul-profundo: #0f172a;
    --vermelho: #dc143c;
    --verde: #10b981;
    --card-bg: rgba(255,255,255,0.06);
    --borda: rgba(255,255,255,0.12);
    --sombra: 0 15px 40px rgba(0,0,0,0.5);
    --ceu-topo: #0f172a;
    --ceu-meio: #1e293b;
    --ceu-base: #311b92;
    --cor-particula: #a78bfa;
  }

  html { scroll-behavior: smooth; scrollbar-width: thin; scrollbar-color: var(--ouro) rgba(0,0,0,0.3); }
  ::-webkit-scrollbar { width: 10px; height: 10px; }
  ::-webkit-scrollbar-track { background: rgba(0,0,0,0.3); }
  ::-webkit-scrollbar-thumb { background: linear-gradient(180deg, var(--ouro), #b8860b); border-radius: 10px; border: 2px solid rgba(0,0,0,0.3); }
  ::-webkit-scrollbar-thumb:hover { background: var(--ouro-claro); }

  /* ============================================================
     FUNDO ANIMADO
     ============================================================ */
  body {
    background:
      radial-gradient(circle at 20% 10%, var(--cor-particula), transparent 40%),
      radial-gradient(circle at 80% 90%, rgba(255,215,0,0.12), transparent 45%),
      linear-gradient(180deg, var(--ceu-topo) 0%, var(--ceu-meio) 50%, var(--ceu-base) 100%);
    background-attachment: fixed;
    min-height: 100vh;
    color: #fff;
    padding: 20px;
    overflow-x: hidden;
    transition: background 2.5s ease;
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      radial-gradient(1px 1px at 20% 30%, #fff, transparent),
      radial-gradient(1px 1px at 70% 60%, #ffd700, transparent),
      radial-gradient(1px 1px at 40% 80%, #a0c0ff, transparent),
      radial-gradient(2px 2px at 90% 20%, #fff, transparent),
      radial-gradient(1px 1px at 10% 70%, #ffd700, transparent),
      radial-gradient(1px 1px at 55% 45%, #c080ff, transparent),
      radial-gradient(1px 1px at 85% 75%, #80ffc0, transparent);
    background-size: 550px 550px, 400px 400px, 300px 300px, 600px 600px, 350px 350px, 500px 500px, 450px 450px;
    opacity: 0.35;
    pointer-events: none;
    z-index: 0;
    animation: estrelas 120s linear infinite;
  }

  @keyframes estrelas {
    from { background-position: 0 0, 0 0, 0 0, 0 0, 0 0, 0 0, 0 0; }
    to { background-position: 550px 550px, -400px 400px, 300px -300px, -600px 600px, 350px 350px, -500px 500px, 450px -450px; }
  }

  /* ============================================================
     PARTÍCULAS
     ============================================================ */
  .particula {
    position: fixed;
    pointer-events: none;
    z-index: 1;
    animation: cairParticula linear infinite;
    opacity: 0.9;
    will-change: transform;
  }

  @keyframes cairParticula {
    0%   { transform: translateY(-10vh) translateX(0) rotate(0deg); opacity: 0; }
    10%  { opacity: 1; }
    90%  { opacity: 1; }
    100% { transform: translateY(110vh) translateX(40px) rotate(720deg); opacity: 0; }
  }

  /* ============================================================
     HEADER
     ============================================================ */
  header { position: relative; z-index: 2; text-align: center; padding: 10px 0; }

  .titulo-principal {
    font-size: clamp(2rem, 6vw, 3.6rem);
    margin: 20px 0 8px;
    background: linear-gradient(90deg, #ffd700, #ffed4e, #fff8b0, #ffd700);
    background-size: 200% auto;
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    letter-spacing: 6px;
    animation: brilhar 4s linear infinite;
    text-shadow: 0 0 40px rgba(255,215,0,0.25);
    font-weight: 900;
  }

  @keyframes brilhar { to { background-position: 200% center; } }

  .subtitulo { color: #b0b0d0; margin-bottom: 25px; font-size: clamp(0.85rem, 2vw, 1.1rem); letter-spacing: 1px; font-style: italic; }

  /* ============================================================
     PAINEL DE ESTAÇÃO
     ============================================================ */
  .painel-estacao {
    position: fixed;
    top: 20px;
    left: 20px;
    background: rgba(15,23,42,0.9);
    border: 1px solid rgba(255,215,0,0.5);
    border-radius: 16px;
    padding: 12px 18px;
    z-index: 100;
    backdrop-filter: blur(12px);
    box-shadow: 0 8px 30px rgba(0,0,0,0.5);
    min-width: 210px;
  }

  .painel-estacao .estacao-topo { display: flex; align-items: center; gap: 10px; margin-bottom: 8px; }
  .painel-estacao .estacao-icone { font-size: 1.8rem; animation: flutuar 3s ease-in-out infinite; }
  @keyframes flutuar { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-3px); } }
  .painel-estacao .estacao-nome { font-size: 1rem; font-weight: bold; color: #ffd700; letter-spacing: 0.5px; }
  .painel-estacao .estacao-desc { font-size: 0.7rem; color: #b0b0d0; margin-bottom: 8px; font-style: italic; line-height: 1.3; }
  .painel-estacao .estacao-track { height: 6px; background: rgba(0,0,0,0.5); border-radius: 6px; overflow: hidden; margin-bottom: 6px; }
  .painel-estacao .estacao-fill { height: 100%; background: linear-gradient(90deg, #ffd700, #ff8c00); border-radius: 6px; width: 0%; transition: width 1s linear; box-shadow: 0 0 10px rgba(255,215,0,0.6); }
  .painel-estacao .estacao-tempo { font-size: 0.72rem; color: #ffd700; text-align: right; font-weight: bold; letter-spacing: 0.5px; }

  /* ============================================================
     BARRA DE PROGRESSO
     ============================================================ */
  .barra-progresso {
    max-width: 1250px; margin: 0 auto 25px; background: rgba(0,0,0,0.3);
    border-radius: 30px; padding: 10px 20px; display: flex; align-items: center; gap: 15px;
    border: 1px solid rgba(255,215,0,0.2); position: relative; z-index: 1;
  }
  .barra-progresso .barra-texto { font-size: 0.82rem; color: #ffd700; font-weight: bold; white-space: nowrap; }
  .barra-progresso .barra-track { flex: 1; height: 10px; background: rgba(0,0,0,0.5); border-radius: 10px; overflow: hidden; }
  .barra-progresso .barra-fill { height: 100%; background: linear-gradient(90deg, #ffd700, #ff8c00, #dc143c); border-radius: 10px; width: 0%; transition: width 1.5s cubic-bezier(.4,0,.2,1); box-shadow: 0 0 15px rgba(255,215,0,0.6); }

  /* ============================================================
     CONTROLES
     ============================================================ */
  .controles-topo {
    position: fixed; top: 20px; right: 20px; display: flex; gap: 10px;
    z-index: 100; flex-wrap: wrap; justify-content: flex-end; max-width: 220px;
  }
  .ctrl-btn {
    width: 44px; height: 44px; border-radius: 50%; background: rgba(15,23,42,0.85);
    border: 1px solid rgba(255,215,0,0.4); color: var(--ouro); font-size: 1.2rem;
    cursor: pointer; transition: all 0.3s; display: flex; align-items: center; justify-content: center;
    backdrop-filter: blur(10px);
  }
  .ctrl-btn:hover { background: var(--ouro); color: #1a1a1a; transform: scale(1.1); box-shadow: 0 0 20px rgba(255,215,0,0.6); }
  .ctrl-btn.ativo { background: var(--ouro); color: #1a1a1a; }

  /* ============================================================
     MENU DE ABAS
     ============================================================ */
  .aba-menu-wrapper { position: relative; z-index: 1; margin-bottom: 30px; }
  .aba-menu { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; padding: 10px 0; }
  .aba {
    padding: 11px 22px; background: rgba(255,255,255,0.06); border: 1px solid var(--borda);
    color: #c0c0e0; border-radius: 30px; cursor: pointer;
    transition: all 0.3s cubic-bezier(.4,0,.2,1); font-size: 0.92rem;
    backdrop-filter: blur(8px); font-weight: 500; white-space: nowrap;
  }
  .aba.ativa { background: linear-gradient(135deg, var(--ouro), #ffb800); color: #2a1a00; font-weight: bold; box-shadow: 0 0 25px rgba(255,215,0,0.5), 0 4px 15px rgba(0,0,0,0.3); transform: translateY(-2px); border-color: transparent; }
  .aba:hover:not(.ativa) { transform: translateY(-2px); border-color: var(--ouro); color: var(--ouro); background: rgba(255,215,0,0.08); }

  /* ============================================================
     PAINÉIS
     ============================================================ */
  .painel { display: none; max-width: 1250px; margin: 0 auto; position: relative; z-index: 1; }
  .painel.visivel { display: block; animation: surgir 0.5s ease; }
  @keyframes surgir { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }
  .painel h2 { text-align: center; margin-bottom: 25px; font-size: clamp(1.3rem, 3vw, 1.8rem); letter-spacing: 1px; }

  /* ============================================================
     JARDIM DAS ESTAÇÕES
     ============================================================ */
  .jardim {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 220px), 1fr));
    gap: 20px; margin-bottom: 40px; padding: 25px;
    background: linear-gradient(160deg, rgba(255,255,255,0.05), rgba(0,0,0,0.2));
    border-radius: 20px; border: 1px solid var(--borda);
  }
  .jardim-titulo { grid-column: 1 / -1; text-align: center; font-size: 1.1rem; color: #ffd700; letter-spacing: 2px; margin-bottom: 5px; text-transform: uppercase; }
  .arvore-card {
    background: rgba(0,0,0,0.25); border-radius: 16px; padding: 15px;
    text-align: center; border: 1px solid rgba(255,255,255,0.1);
    transition: all 0.4s; position: relative; overflow: hidden; min-height: 280px;
    display: flex; flex-direction: column; align-items: center; justify-content: center;
  }
  .arvore-card:hover { transform: translateY(-5px); border-color: rgba(255,215,0,0.5); box-shadow: 0 10px 30px rgba(0,0,0,0.4); }
  .arvore-card .arvore-nome { font-size: 0.85rem; color: #ffe680; font-weight: bold; margin-top: 10px; }
  .arvore-card .arvore-sub { font-size: 0.7rem; color: #a0a0c0; margin-top: 3px; font-style: italic; }
  .arvore-svg { width: 100%; max-width: 200px; height: 200px; overflow: visible; filter: drop-shadow(0 5px 15px rgba(0,0,0,0.5)); }
  .arvore-svg .folha { transition: fill 1.5s ease, opacity 1.5s ease; }
  .estacao-verao .arvore-svg .folha-1 { fill: #22c55e; }
  .estacao-verao .arvore-svg .folha-2 { fill: #16a34a; }
  .estacao-verao .arvore-svg .folha-3 { fill: #4ade80; }
  .estacao-primavera .arvore-svg .folha-1 { fill: #ffb7d5; }
  .estacao-primavera .arvore-svg .folha-2 { fill: #ff8fb8; }
  .estacao-primavera .arvore-svg .folha-3 { fill: #ffd1e3; }
  .estacao-outono .arvore-svg .folha-1 { fill: #f97316; }
  .estacao-outono .arvore-svg .folha-2 { fill: #dc2626; }
  .estacao-outono .arvore-svg .folha-3 { fill: #fbbf24; }
  .estacao-inverno .arvore-svg .folha { opacity: 0.05; transition: opacity 2s ease; }
  @keyframes balancar { 0%, 100% { transform: rotate(0deg); } 50% { transform: rotate(1.5deg); } }
  .arvore-svg .copa { animation: balancar 6s ease-in-out infinite; transform-origin: center bottom; }

  /* ============================================================
     GRADES
     ============================================================ */
  .grade { display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 290px), 1fr)); gap: 25px; }

  .cartao {
    position: relative; background: linear-gradient(160deg, rgba(255,255,255,0.07), rgba(255,255,255,0.02));
    border-radius: 18px; padding: 20px; border: 1px solid var(--borda);
    transition: all 0.35s cubic-bezier(.4,0,.2,1); backdrop-filter: blur(10px); overflow: hidden;
  }
  .cartao::before {
    content: ''; position: absolute; inset: 0; border-radius: 18px; padding: 1.5px;
    background: linear-gradient(135deg, transparent, rgba(255,215,0,0.6), transparent);
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
    -webkit-mask-composite: xor; mask-composite: exclude;
    opacity: 0; transition: opacity 0.35s; pointer-events: none;
  }
  .cartao:hover::before { opacity: 1; }
  .cartao:hover { transform: translateY(-6px) scale(1.015); box-shadow: var(--sombra), 0 0 30px rgba(255,215,0,0.15); border-color: rgba(255,215,0,0.4); }
  .cartao h3 { margin-bottom: 10px; font-size: 1.2rem; color: #ffe680; letter-spacing: 0.5px; }
  .cartao p { color: #b0b0d0; font-size: 0.9rem; line-height: 1.6; margin-bottom: 12px; }

  .ilustracao {
    position: relative; width: 100%; height: 230px; border-radius: 14px; margin-bottom: 14px;
    display: flex; align-items: center; justify-content: center; overflow: hidden;
    background: linear-gradient(135deg, rgba(255,255,255,0.05), rgba(0,0,0,0.15));
    box-shadow: inset 0 0 40px rgba(0,0,0,0.5);
  }
  .ilustracao .fallback { font-size: 4rem; filter: drop-shadow(0 0 12px rgba(255,255,255,0.4)); animation: flutuar 3s ease-in-out infinite; }

  /* ============================================================
     ETIQUETAS
     ============================================================ */
  .etiqueta { display: inline-block; padding: 4px 13px; border-radius: 15px; font-size: 0.72rem; font-weight: bold; margin: 2px 2px 8px 0; letter-spacing: 0.5px; text-transform: uppercase; }
  .n1 { background: linear-gradient(135deg,#8b5a2b,#5a3a1a); color: #ffe8c0; }
  .n2 { background: linear-gradient(135deg,#cd853f,#8b5a2b); color: #fff; }
  .n3 { background: linear-gradient(135deg,#4169e1,#2a4a9a); color: #fff; }
  .n4 { background: linear-gradient(135deg,#ff8c00,#b36000); color: #fff; }
  .n5 { background: linear-gradient(135deg,#dc143c,#8b0a1a); color: #fff; box-shadow: 0 0 15px rgba(220,20,60,0.6); }
  .n6 { background: linear-gradient(135deg,#8b00ff,#4a0080); color: #fff; box-shadow: 0 0 20px rgba(139,0,255,0.7); }
  .n7 { background: linear-gradient(135deg,#00c9a7,#00806a); color: #fff; box-shadow: 0 0 18px rgba(0,201,167,0.6); }

  /* ============================================================
     LISTAS / FICHAS / CHAVES
     ============================================================ */
  .lista-itens { font-size: 0.85rem; color: #d0d0f0; line-height: 1.9; }
  .lista-itens li { list-style: none; padding-left: 4px; }
  .lista-itens li::before { content: '✦ '; color: var(--ouro); margin-right: 2px; }
  .ficha { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 12px; font-size: 0.78rem; }
  .ficha div { background: rgba(0,0,0,0.25); padding: 6px 10px; border-radius: 8px; color: #c0c0e0; border-left: 2px solid var(--ouro); }
  .ficha span { color: var(--ouro-claro); font-weight: bold; }
  .chave { display: inline-flex; align-items: center; gap: 6px; padding: 6px 14px; background: linear-gradient(135deg, rgba(255,215,0,0.2), rgba(255,215,0,0.05)); border: 1px solid rgba(255,215,0,0.5); border-radius: 20px; font-size: 0.8rem; font-weight: bold; color: #ffd700; margin: 4px 4px 8px 0; }

  /* ============================================================
     CHEFES
     ============================================================ */
  .grupo-chefes {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 240px), 1fr));
    gap: 18px; margin-bottom: 35px; padding: 20px;
    background: rgba(0,0,0,0.25); border-radius: 18px; border: 1px solid rgba(255,255,255,0.08);
  }
  .grupo-titulo { grid-column: 1 / -1; text-align: center; color: #ff8080; font-size: 1.1rem; letter-spacing: 2px; margin-bottom: 5px; text-transform: uppercase; }
  .mini-chefe { background: linear-gradient(160deg, rgba(255,255,255,0.06), rgba(0,0,0,0.2)); border-radius: 14px; padding: 14px; border: 1px solid rgba(255,255,255,0.1); transition: all 0.3s; text-align: center; }
  .mini-chefe:hover { transform: translateY(-5px); border-color: rgba(255,215,0,0.5); box-shadow: 0 10px 25px rgba(0,0,0,0.4); }
  .mini-chefe .sprite-box { height: 130px; border-radius: 10px; background: rgba(0,0,0,0.3); display: flex; align-items: center; justify-content: center; margin-bottom: 10px; overflow: hidden; font-size: 3rem; }
  .mini-chefe h4 { color: #ffe680; font-size: 0.95rem; margin-bottom: 4px; }
  .mini-chefe p { color: #a0a0c0; font-size: 0.78rem; line-height: 1.4; }
  .mini-chefe .nivel-tag { display: inline-block; margin-top: 6px; padding: 2px 10px; background: rgba(220,20,60,0.3); border: 1px solid rgba(220,20,60,0.6); border-radius: 12px; font-size: 0.7rem; color: #ff8080; font-weight: bold; }

  /* ============================================================
     SISTEMAS
     ============================================================ */
  .sistema-dungeon, .sistema-chaves {
    background: linear-gradient(160deg, rgba(255,100,0,0.08), rgba(0,0,0,0.2));
    border: 1px solid rgba(255,150,0,0.3); border-radius: 16px; padding: 25px;
    margin-bottom: 30px; text-align: center;
  }
  .sistema-chaves { background: linear-gradient(160deg, rgba(255,215,0,0.08), rgba(0,0,0,0.2)); border-color: rgba(255,215,0,0.3); }
  .sistema-dungeon h3, .sistema-chaves h3 { color: #ffaa00; margin-bottom: 12px; font-size: 1.3rem; }
  .sistema-chaves h3 { color: #ffd700; }
  .sistema-dungeon p, .sistema-chaves p { color: #d0d0f0; font-size: 0.92rem; line-height: 1.7; max-width: 800px; margin: 0 auto; }
  .fluxo-portal { display: flex; flex-wrap: wrap; justify-content: center; align-items: center; gap: 10px; margin-top: 20px; font-size: 0.82rem; }
  .fluxo-passo { background: rgba(0,0,0,0.4); border: 1px solid rgba(255,215,0,0.4); border-radius: 12px; padding: 8px 16px; color: #ffe680; }
  .fluxo-seta { color: #ffd700; font-size: 1.4rem; }
  .requisito { display: inline-flex; align-items: center; gap: 8px; padding: 8px 16px; background: rgba(0,0,0,0.4); border-radius: 12px; font-size: 0.82rem; color: #ffd700; border: 1px dashed rgba(255,215,0,0.5); margin-top: 8px; }

  /* ============================================================
     COMPANHEIROS — SPRITES COM IMAGENS REAIS
     ============================================================ */
  .comp-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 300px), 1fr));
    gap: 25px;
  }

  .comp-card {
    position: relative;
    background: linear-gradient(160deg, rgba(255,255,255,0.07), rgba(255,255,255,0.02));
    border-radius: 20px;
    padding: 20px;
    border: 1px solid var(--borda);
    transition: all 0.35s cubic-bezier(.4,0,.2,1);
    backdrop-filter: blur(10px);
    overflow: hidden;
    display: flex;
    flex-direction: column;
  }

  .comp-card::before {
    content: '';
    position: absolute;
    inset: 0;
    border-radius: 20px;
    padding: 1.5px;
    background: linear-gradient(135deg, transparent, rgba(255,215,0,0.7), transparent);
    -webkit-mask: linea
