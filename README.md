<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Captação & Vendas - Imóveis</title>
  <style>
    :root{
      --azul: #4A90E2;
      --roxo: #7F5AF0;
      --laranja: #F5A623;
      --turquesa: #1ABC9C;
      --fundo: #0f111a;
      --fundoCard: #141a24;
      --texto: #e8eefc;
      --textoSec: #aab6d3;
      --bordas: rgba(255,255,255,.08);
    }
    *{box-sizing:border-box}
    html,body{margin:0;padding:0;height:100%}
    body{font-family: Inter, system-ui, -apple-system, Arial, sans-serif;
        background: linear-gradient(135deg, #0b1020 0%, #0a1220 60%, #0b1b2a 100%);
        color: var(--texto); display:flex; flex-direction:column; align-items:stretch;}
    header{display:flex; justify-content:space-between; align-items:center;
      padding:16px 24px; background: rgba(10,12,25,.9); border-bottom:1px solid var(--bordas);
      position: sticky; top:0; z-index: 10;}
    header h1{font-size:20px; margin:0; font-weight:600}
    header .subtitle{color:var(--textoSec); font-size:12px}
    .container{display:flex; gap:16px; padding:16px 24px; flex:1; min-height: calc(100vh - 72px);}
    .panel{ background: var(--fundoCard); border:1px solid var(--bordas); border-radius:12px;
            padding:16px; box-shadow: 0 8px 20px rgba(0,0,0,.25); width: 100%;}
    .panel h2{ margin:0 0 12px 0; font-size:16px; color:#eaf4ff}
    .grid{ display:grid; grid-template-columns: 1.1fr 0.9fr; gap:16px; width:100%;}
    .card{ background:#111522; border:1px solid var(--bordas); border-radius:10px; padding:12px; }
    .field{ display:flex; flex-direction:column; gap:6px; margin-bottom:10px; }
    .field label{ font-size:12px; color:var(--textoSec); }
    .field input, .field select, .field textarea{
      padding:10px 12px; border-radius:8px; border:1px solid var(--bordas);
      background:#0b1220; color:#eaf4ff; outline:none;
    }
    .row{ display:flex; gap:8px; align-items:center; }
    .btn{ padding:10px 14px; border-radius:8px; border:0; cursor:pointer;
           font-weight:600; color:white; background: var(--azul); }
    .btn.secondary{ background:#2a2f55; color:#e5eaff; }
    .btn.danger{ background:#e24a4a; }
    .cta{ display:inline-flex; align-items:center; justify-content:center;
           padding:10px 14px; border-radius:8px; background:linear-gradient(135deg, var(--azul), var(--roxo));
           color:white; text-decoration:none; font-weight:700; }
    .stats{ display:grid; grid-template-columns: repeat(4, 1fr); gap:12px; margin-top:8px;}
    .stat{ background:#0a1120; padding:12px; border-radius:8px; border:1px solid var(--bordas); text-align:center;}
    .stat .val{ font-size:18px; font-weight:700; }
    .table{ width:100%; border-collapse: collapse; margin-top:8px; }
    .table th, .table td{ padding:10px; border-bottom:1px solid var(--bordas); font-size:13px; text-align:left;}
    .badge{ padding:4px 8px; border-radius:999px; font-size:12px; background:#1e2a4a; color:#d7e7ff; }
    @media (max-width: 980px){
      .grid{ grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <header>
    <div>
      <h1>Captação & Vendas - Imóveis</h1>
      <div class="subtitle">Interface de captura, gestão e vendas. Copie o conteúdo para o Notion se desejar; use esta página como protótipo.</div>
    </div>
    <div class="row">
      <button class="btn" id="btnExport">Exportar CSV (Leads)</button>
    </div>
  </header>

  <main class="container">
    <section class="grid">
      <!-- Painel de Entrada / Leads -->
      <div class="panel" id="painelLeads">
        <h2>Captação & Leads</h2>
        <div class="card" style="margin-bottom:12px;">
          <div class="field">
            <label>Nome do Lead</label>
            <input type="text" id="leadNome" placeholder="Ex.: João da Silva" />
          </div>
          <div class="row" style="gap:8px;">
            <div class="field" style="flex:1;">
              <label>Telefone</label>
              <input type="text" id="leadTel" placeholder="(11) 99999-9999" />
            </div>
            <div class="field" style="flex:1;">
              <label>E-mail</label>
              <input type="email" id="leadEmail" placeholder="exemplo@dominio.com" />
            </div>
          </div>
          <div class="row" style="gap:8px;">
            <div class="field" style="flex:1;">
              <label>Fonte / Origem</label>
              <select id="leadFonte">
                <option>Website</option><option>Facebook</option><option>Instagram</option><option>Indicação</option><option>Eventos</option>
              </select>
            </div>
            <div class="field" style="flex:1;">
              <label>Interação mais recente</label>
              <input type="text" id="leadInteracao" placeholder="Data/Observação" />
            </div>
          </div>
          <div class="row" style="gap:8px;">
            <button class="btn" id="btnAddLead">Adicionar Lead</button>
            <button class="btn secondary" id="btnLimparLead">Limpar</button>
          </div>
        </div>

        <div class="stats" aria-label="Indicadores de desempenho">
          <div class="stat">
            <div class="label" style="font-size:12px; color:var(--textoSec)">Leads</div>
            <div class="val" id="statLeads">0</div>
          </div>
          <div class="stat">
            <div class="label" style="font-size:12px; color:var(--textoSec)">Conversões</div>
            <div class="val" id="statConv">0%</div>
          </div>
          <div class="stat">
            <div class="label" style="font-size:12px; color:var(--textoSec)">Valor estimado</div>
            <div class="val" id="statValor">R$ 0,00</div>
          </div>
          <div class="stat">
            <div class="label" style="font-size:12px; color:var(--textoSec)">Próximo passo</div>
            <div class="val" id="statPasso">—</div>
          </div>
        </div>

        <table class="table" id="tblLeads" aria-label="Tabela de leads">
          <thead>
            <tr>
              <th>Lead</th><th>Telefone</th><th>E-mail</th><th>Origem</th><th>Interação</th><th>Valor Estimado</th><th>Status</th>
            </tr>
          </thead>
          <tbody id="tbodyLeads">
            <!-- linhas dinâmicas -->
          </tbody>
        </table>
      </div>

      <!-- Painel de Vendas / Pipeline -->
      <div class="panel" id="painelVendas">
        <h2>Pipeline de Vendas</h2>

        <div class="field" style="margin-bottom:6px;">
          <label>Filtro rápido</label>
          <select id="filterStatus">
            <option>Todos</option><option>Nova</option><option>Em Contato</option><option>Negociando</option><option>Fechado</option>
          </select>
        </div>

        <table class="table" aria-label="Pipeline">
          <thead>
            <tr>
              <th>Lead</th><th>Imóvel</th><th>Valor</th><th>Etapa</th><th>Próximo passo</th><th>Responsável</th><th>Ações</th>
            </tr>
          </thead>
          <tbody id="tbodyPipeline">
            <!-- linhas dinâmicas -->
          </tbody>
        </table>

        <div class="row" style="margin-top:8px;">
          <button class="cta" id="btnNovaVenda" style="text-decoration:none;cursor:pointer;">
            + Nova Venda
          </button>
        </div>
      </div>
    </section>
  </main>

  <footer style="padding:12px 24px; text-align:center; color:var(--textoSec);">
    Interface protótipo. Adapte para integração com Notion (embeds/CSV) conforme necessário.
  </footer>

  <script>
    // Dados iniciais de exemplo
    const leads = [
      {nome:'Ana Maria', tel:'(11) 91234-5678', email:'ana@example.com', origem:'Facebook', interacao:'2025-10-20: ligação', valor:1200000, status:'Nova'},
      {nome:'Carlos Pereira', tel:'(11) 95555-1234', email:'carlos@example.com', origem:'Website', interacao:'2025-10-18: envio de propostas', valor:950000, status:'Em Contato'}
    ];

    const pipeline = [
      {lead:'Ana Maria', imovel:'Apartamento 3Q no Centro', valor:1200000, etapa:'Negociando', proximo:'Enviar proposta', resp:'Você'},
      {lead:'Carlos Pereira', imovel:'Casa com piscina em Vila Mariana', valor:950000, etapa:'Nova', proximo:'Agendar visita', resp:'Equipe'}
    ];

    // Helpers
    function formatBRL(n){
      return 'R$ ' + Number(n || 0).toLocaleString('pt-BR', {minimumFractionDigits: 2, maximumFractionDigits: 2});
    }

    // Render leads
    function renderLeads(){
      const tbody = document.getElementById('tbodyLeads');
      tbody.innerHTML = '';
      let totalLeads = 0, totalValor = 0, consec = 0;
      leads.forEach((l, idx) => {
        totalLeads++;
        totalValor += Number(l.valor || 0);
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${l.nome}</td>
          <td>${l.tel}</td>
          <td>${l.email}</td>
          <td><span class="badge">${l.origem}</span></td>
          <td>${l.interacao}</td>
          <td>${formatBRL(l.valor)}</td>
          <td>${l.status || 'Nova'}</td>
        `;
        tbody.appendChild(tr);
      });
      document.getElementById('statLeads').textContent = totalLeads;
      document.getElementById('statValor').textContent = formatBRL(totalValor);
    }

    // Render pipeline
    function renderPipeline(){
      const tbd = document.getElementById('tbodyPipeline');
      tbd.innerHTML = '';
      pipeline.forEach((p) => {
        const tr = document.createElement('tr');
        tr.innerHTML = `
          <td>${p.lead}</td>
          <td>${p.imovel}</td>
          <td>${formatBRL(p.valor)}</td>
          <td>${p.etapa}</td>
          <td>${p.proximo}</td>
          <td>${p.resp}</td>
          <td>
            <button class="btn secondary" onclick="alert('Editar ${p.imovel}')">Editar</button>
            <button class="btn danger" onclick="alert('Remover neste mock: ${p.imovel}')">Remover</button>
          </td>
        `;
        tbd.appendChild(tr);
      });
    }

    // Eventos
    document.getElementById('btnAddLead').addEventListener('click', () => {
      const nome = document.getElementById('leadNome').value.trim();
      const tel = document.getElementById('leadTel').value.trim();
      const email = document.getElementById('leadEmail').value.trim();
      const origem = document.getElementById('leadFonte').value;
      const interacao = document.getElementById('leadInteracao').value.trim() || new Date().toISOString().slice(0,10);
      if(!nome){ alert('Informe o nome do lead'); return; }
      leads.push({nome, tel, email, origem, interacao, valor: 0, status:'Nova'});
      renderLeads();
      // reset
      document.getElementById('leadNome').value = '';
      document.getElementById('leadTel').value = '';
      document.getElementById('leadEmail').value = '';
      document.getElementById('leadInteracao').value = '';
    });

    document.getElementById('btnLimparLead').addEventListener('click', () => {
      document.getElementById('leadNome').value = '';
      document.getElementById('leadTel').value = '';
      document.getElementById('leadEmail').value = '';
      document.getElementById('leadInteracao').value = '';
    });

    document.getElementById('btnNovaVenda').addEventListener('click', () => {
      // ação mock: adiciona entrada simples no pipeline
      const novo = {lead: leads.length ? leads[0].nome : 'Novo Lead', imovel:'Imóvel Exemplo', valor: 500000, etapa:'Nova', proximo:'Contato', resp:'Você'};
      pipeline.unshift(novo);
      renderPipeline();
    });

    document.getElementById('filterStatus').addEventListener('change', () => {
      // filtro simples (em um exemplo real, filtraria a lista de pipeline)
      renderPipeline();
    });

    document.getElementById('btnExport').addEventListener('click', () => {
      // Export simples: compila leads em CSV
      const header = ['Lead','Telefone','E-mail','Origem',
