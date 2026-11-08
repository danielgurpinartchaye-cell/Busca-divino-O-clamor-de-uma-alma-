
import { initializeApp } from "https://www.gstatic.com/firebasejs/13.2.0/firebase-app.js";

import {
  getAuth,
  createUserWithEmailAndPassword,
  signInWithEmailAndPassword,
  signOut,
  onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/13.2.0/firebase-auth.js";

import {
  getFirestore,
  collection,
  addDoc,
  serverTimestamp
} from "https://www.gstatic.com/firebasejs/13.2.0/firebase-firestore.js";

// CONFIGURAÇÃO DO FIREBASE
const firebaseConfig = {
  apiKey: "AIzaSyCV1HFfOeT3NS4rwUWrZBkKYavxtkHDDq4",
  authDomain: "busca-divina.firebaseapp.com",
  projectId: "busca-divina",
  storageBucket: "busca-divina.firebasestorage.app",
  messagingSenderId: "616898461786",
  appId: "1:616898461786:web:13c1e57c4855fee6149863",
  measurementId: "G-8DPC1DVL2Y"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

let utilizadorAtual = null;

// NAVEGAÇÃO
document.querySelectorAll(".nav-btn").forEach(botao => {
  botao.addEventListener("click", () => {
    document.querySelectorAll(".nav-btn").forEach(b => b.classList.remove("active"));
    document.querySelectorAll(".page").forEach(p => p.classList.remove("active"));

    botao.classList.add("active");
    document.getElementById(botao.dataset.page)?.classList.add("active");
  });
});

// DATA E CONEXÃO
document.getElementById("date").textContent =
  new Date().toLocaleDateString("pt-PT", {
    weekday: "long",
    year: "numeric",
    month: "long",
    day: "numeric"
  });

document.getElementById("connection").textContent =
  navigator.onLine ? "Ligação à internet disponível" : "Modo offline";

// AUTENTICAÇÃO
const painel = document.createElement("section");
painel.id = "account-panel";
painel.className = "account-panel";

painel.innerHTML = `
  <h2>Minha conta Busca Divina</h2>
  <input id="user-email" type="email" placeholder="O teu email">
  <input id="user-password" type="password" placeholder="A tua palavra-passe">
  <div>
    <button id="register-btn">Criar conta</button>
    <button id="login-btn">Entrar</button>
    <button id="logout-btn" hidden>Sair</button>
  </div>
  <p id="account-message">Entra ou cria a tua conta para começar.</p>
`;

document.querySelector("main").prepend(painel);

const emailInput = document.getElementById("user-email");
const passwordInput = document.getElementById("user-password");
const accountMessage = document.getElementById("account-message");

document.getElementById("register-btn").addEventListener("click", async () => {
  try {
    await createUserWithEmailAndPassword(
      auth,
      emailInput.value.trim(),
      passwordInput.value
    );
    accountMessage.textContent = "Conta criada com sucesso!";
  } catch (erro) {
    accountMessage.textContent = "Erro: " + erro.message;
  }
});

document.getElementById("login-btn").addEventListener("click", async () => {
  try {
    await signInWithEmailAndPassword(
      auth,
      emailInput.value.trim(),
      passwordInput.value
    );
    accountMessage.textContent = "Sessão iniciada!";
  } catch (erro) {
    accountMessage.textContent = "Erro: " + erro.message;
  }
});

document.getElementById("logout-btn").addEventListener("click", async () => {
  await signOut(auth);
});

onAuthStateChanged(auth, utilizador => {
  utilizadorAtual = utilizador;

  document.getElementById("logout-btn").hidden = !utilizador;
  document.getElementById("register-btn").hidden = !!utilizador;
  document.getElementById("login-btn").hidden = !!utilizador;

  accountMessage.textContent = utilizador
    ? "Sessão iniciada: " + utilizador.email
    : "Entra ou cria a tua conta para começar.";
});

// BÍBLIA
const versiculos = [
  ["Salmos 23:1", "O Senhor é o meu pastor; nada me faltará."],
  ["João 14:6", "Eu sou o caminho, e a verdade, e a vida."],
  ["Filipenses 4:13", "Posso todas as coisas naquele que me fortalece."],
  ["Provérbios 3:5", "Confia no Senhor de todo o teu coração."],
  ["Isaías 41:10", "Não temas, porque eu sou contigo."]
];

document.getElementById("verses").innerHTML = versiculos.map(v =>
  `<article><h3>${v[0]}</h3><p>${v[1]}</p></article>`
).join("");

// ESTUDOS
const estudos = [
  ["A importância da oração", "A oração fortalece a comunhão com Deus. Reserva momentos diários para falar com Ele."],
  ["O poder da fé", "A fé ajuda-nos a confiar em Deus mesmo nos momentos difíceis."],
  ["O arrependimento", "Arrepender-se é reconhecer os erros e voltar o coração para Deus."],
  ["O amor ao próximo", "Jesus ensinou-nos a amar, perdoar e ajudar uns aos outros."]
];

document.getElementById("studies-content").innerHTML = estudos.map(e =>
  `<article><h3>${e[0]}</h3><p>${e[1]}</p></article>`
).join("");

// ORAÇÕES
const oracoes = [
  ["Oração da manhã", "Senhor, guia os meus passos neste novo dia. Dá-me sabedoria, paz e força. Amém."],
  ["Oração de proteção", "Pai, protege a minha família e acompanha-nos em todos os caminhos. Amém."],
  ["Oração de gratidão", "Obrigado, Senhor, pela vida, pela esperança e pelas bênçãos recebidas. Amém."]
];

document.getElementById("prayers-content").innerHTML = oracoes.map(o =>
  `<article><h3>${o[0]}</h3><p>${o[1]}</p></article>`
).join("");

// LOUVORES
const louvores = [
  "Louvar a Deus em todos os momentos.",
  "A minha esperança está no Senhor.",
  "Que a minha vida seja um testemunho de fé."
];

document.getElementById("songs-content").innerHTML = louvores.map(s =>
  `<article><p>♫ ${s}</p></article>`
).join("");

// JOGO BÍBLICO
const perguntas = [
  { q: "Quem construiu a arca?", a: ["Moisés", "Noé", "Pedro"], c: 1 },
  { q: "Quem derrotou Golias?", a: ["David", "Saul", "Salomão"], c: 0 },
  { q: "Onde nasceu Jesus?", a: ["Nazaré", "Jerusalém", "Belém"], c: 2 },
  { q: "Quem foi lançado na cova dos leões?", a: ["Daniel", "José", "Paulo"], c: 0 },
  { q: "Quantos discípulos Jesus escolheu?", a: ["10", "12", "15"], c: 1 }
];

let perguntaAtual = 0;
let pontos = 0;

function mostrarPergunta() {
  const p = perguntas[perguntaAtual];

  document.getElementById("game-content").innerHTML = `
    <h3>${p.q}</h3>
    ${p.a.map((a, i) =>
      `<button class="answer-btn" data-answer="${i}">${a}</button>`
    ).join("")}
    <p>Pergunta ${perguntaAtual + 1} de ${perguntas.length}</p>
    <p>Pontuação: ${pontos}</p>
    <p id="game-message"></p>
  `;

  document.querySelectorAll(".answer-btn").forEach(botao => {
    botao.addEventListener("click", () => {
      const resposta = Number(botao.dataset.answer);

      if (resposta === p.c) {
        pontos++;
        document.getElementById("game-message").textContent = "Correto! Muito bem!";
      } else {
        document.getElementById("game-message").textContent =
          "Resposta incorreta. Continua a aprender!";
      }

      document.querySelectorAll(".answer-btn").forEach(b => b.disabled = true);

      const proximo = document.createElement("button");
      proximo.textContent = perguntaAtual === perguntas.length - 1
        ? "Ver resultado"
        : "Próxima pergunta";

      proximo.onclick = finalizarOuContinuar;
      document.getElementById("game-content").appendChild(proximo);
    });
  });
}

async function finalizarOuContinuar() {
  perguntaAtual++;

  if (perguntaAtual < perguntas.length) {
    mostrarPergunta();
    return;
  }

  document.getElementById("game-content").innerHTML = `
    <h3>Desafio concluído!</h3>
    <p>Acertaste ${pontos} de ${perguntas.length} perguntas.</p>
    <button id="restart-game">Jogar novamente</button>
  `;

  if (utilizadorAtual) {
    try {
      await addDoc(collection(db, "pontuacoes"), {
        uid: utilizadorAtual.uid,
        pontos,
        total: perguntas.length,
        criadoEm: serverTimestamp()
      });
    } catch (erro) {
      console.error("Não foi possível guardar a pontuação:", erro);
    }
  }

  document.getElementById("restart-game").onclick = () => {
    perguntaAtual = 0;
    pontos = 0;
    mostrarPergunta();
  };
}

mostrarPergunta();

// DIÁRIO ESPIRITUAL
document.getElementById("save-diary").addEventListener("click", async () => {
  const texto = document.getElementById("diary-entry").value.trim();

  if (!texto) {
    alert("Escreve primeiro a tua reflexão.");
    return;
  }

  if (!utilizadorAtual) {
    alert("Entra na tua conta para guardar a reflexão online.");
    return;
  }

  try {
    await addDoc(collection(db, "reflexoes"), {
      uid: utilizadorAtual.uid,
      texto,
      criadoEm: serverTimestamp()
    });

    document.getElementById("diary-content").textContent =
      "Reflexão guardada na tua conta.";
    document.getElementById("diary-entry").value = "";
  } catch (erro) {
    alert("Não foi possível guardar. Verifica as regras do Firestore.");
    console.error(erro);
  }
});

console.log("Busca Divina preparado para usar o Firebase.");
