<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Registro de Horas Extras - Julho</title>
<style>
body {font-family: Arial, sans-serif; background-color: #f4f6f9; margin:0; padding:20px;}
h2 {text-align:center; color:#333;}
table {border-collapse:collapse; width:100%; box-shadow:0 2px 8px rgba(0,0,0,0.1); background:white;}
th {background:#1976d2; color:white; padding:10px;}
th, td {border:1px solid #ccc; text-align:center; padding:8px;}
td {background:#fafafa;}
.botao {width:90%; margin:3px; padding:10px; cursor:pointer; border:none; border-radius:4px; font-weight:bold; transition:transform 0.1s;}
.botao:hover {transform:scale(1.03);}
.disponivel {background:#9e9e9e; color:white;}
.ocupado {background:#4caf50; color:white;}
.modal {display:none; position:fixed; z-index:1000; padding-top:100px; left:0; top:0; width:100%; height:100%; overflow:auto; background:rgba(0,0,0,0.4);}
.modal-content {background:#fff; margin:auto; padding:20px; border:1px solid #888; width:300px; border-radius:8px;}
.close {color:#aaa; float:right; font-size:28px; font-weight:bold;}
.close:hover,.close:focus {color:black; text-decoration:none; cursor:pointer;}
#salvarBtn, #alterarBtn {background:#1976d2; color:white; border:none; padding:8px 16px; border-radius:4px; cursor:pointer; margin-top:8px;}
#salvarBtn:hover, #alterarBtn:hover {background:#125ea3;}
#nomeInput, #senhaInput {width:90%; padding:6px; margin-top:10px;}
</style>
</head>
<body>
<h2>Registro de Horas Extras - Julho</h2>
<table>
<thead>
<tr>
<th>Dia / Local</th>
<th>PAI 06:30 ÀS 18:30</th>
<th>UPA SABARÁ DIA 06:30 ÀS 18:30</th>
<th>UPA SABARÁ NOTURNO 18:30 ÀS 06:30</th>
<th>UPA JARDIM DO SOL DIA 06:30 ÀS 18:30</th>
<th>UPA JARDIM DO SOL NOTURNO 18:30 ÀS 06:30</th>
<th>USINA DE ASFALTO  18:30 ÀS 06:30</th>
<th>UBS LEONOR DIURNO  08:00 ÀS 16:00</th>
</tr>
</thead>
<tbody>
<!-- Gerar linhas com JavaScript -->
</tbody>
</table>
<div id="modal" class="modal">
<div class="modal-content">
<span class="close" onclick="fecharModal()">&times;</span>
<p id="modalTexto"></p>
<input type="text" id="nomeInput" placeholder="Seu nome" style="display:none;">
<input type="password" id="senhaInput" placeholder="Senha" style="display:none;">
<br>
<button id="salvarBtn" style="display:none;" onclick="salvarNome()">Salvar</button>
<button id="alterarBtn" style="display:none;" onclick="alterarNome()">Alterar</button>
</div>
</div>
<script>
const tbody = document.querySelector("tbody");
for (let dia = 1; dia <= 31; dia++) {
  const tr = document.createElement("tr");
  const tdDia = document.createElement("td");
  tdDia.textContent = "Dia " + dia;
  tr.appendChild(tdDia);

  for (let local = 1; local <= 7; local++) {
    const td = document.createElement("td");

    if (local === 1 || local === 7) {
      const btn = document.createElement("button");
      btn.className = "botao disponivel";
      btn.textContent = "Reservar";
      btn.onclick = function(e) { abrirModal(e.target); };
      td.appendChild(btn);
    } else {
      for (let b = 1; b <= 2; b++) {
        const btn = document.createElement("button");
        btn.className = "botao disponivel";
        btn.textContent = "Reservar " + b;
        btn.onclick = function(e) { abrirModal(e.target); };
        td.appendChild(btn);
        td.appendChild(document.createElement("br"));
      }
    }
    tr.appendChild(td);
  }
  tbody.appendChild(tr);
}

let botaoAtual = null;
function abrirModal(botao) {
  botaoAtual = botao;
  const modal = document.getElementById("modal");
  const texto = document.getElementById("modalTexto");
  const inputNome = document.getElementById("nomeInput");
  const inputSenha = document.getElementById("senhaInput");
  const salvar = document.getElementById("salvarBtn");
  const alterar = document.getElementById("alterarBtn");

  if (botao.classList.contains("ocupado")) {
    texto.textContent = "Este horário já está reservado por: " + botao.dataset.nome + ". Para alterar, digite a senha:";
    inputNome.style.display = "block";
    inputSenha.style.display = "block";
    salvar.style.display = "none";
    alterar.style.display = "inline-block";
  } else {
    texto.textContent = "Deseja reservar este horário?";
    inputNome.style.display = "block";
    inputSenha.style.display = "none";
    salvar.style.display = "inline-block";
    alterar.style.display = "none";
  }
  modal.style.display = "block";
}

function fecharModal() {
  document.getElementById("modal").style.display = "none";
  document.getElementById("nomeInput").value = "";
  document.getElementById("senhaInput").value = "";
}

function salvarNome() {
  const nome = document.getElementById("nomeInput").value;
  if (!nome) return;
  botaoAtual.textContent = nome;
  botaoAtual.dataset.nome = nome;
  botaoAtual.classList.remove("disponivel");
  botaoAtual.classList.add("ocupado");
  fecharModal();
}

function alterarNome() {
  const senha = document.getElementById("senhaInput").value;
  const nome = document.getElementById("nomeInput").value;
  if (senha !== "GML25") {
    alert("Senha incorreta!");
    return;
  }
  if (!nome) return;
  botaoAtual.textContent = nome;
  botaoAtual.dataset.nome = nome;
  fecharModal();
}
</script>
</body>
</html>
