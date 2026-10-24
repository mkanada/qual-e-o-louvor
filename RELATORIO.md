# Qual é o Louvor? — relatório do que foi feito

Atualizado em 24/10/2026.

## Resultado

- Site: https://mkanada.github.io/qual-e-o-louvor/
- Repositório (público): https://github.com/mkanada/qual-e-o-louvor
- Branch `main`, publicada na raiz via GitHub Pages (`legacy`, arquivo `.nojekyll` presente).
- Últimos commits: `c127bdd` (primeira versão), `7850925` (resposta digitada e dicas escolhidas).
- Não abri o jogo num navegador. Verifiquei que as 100 notas existem, que o JavaScript não tem erro de sintaxe e que a comparação de respostas se comporta como esperado (testes em Node).

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `index.html` | O jogo inteiro (HTML, CSS e JavaScript em um só arquivo). |
| `*.mp3` | 100 notas: 10 músicas × 1 a 10 notas. O sufixo do nome é o número de notas. `maranata` usa `-NN-nota.mp3`; as outras, `-NN.mp3`. |
| `dicas.md` | As 10 dicas escolhidas por você, uma por título. |
| `.nojekyll` | Evita o processamento Jekyll do GitHub Pages. |
| `RELATORIO.md` | Este documento. |

## Histórico

1. **Conversa anterior.** O link compartilhado não pôde ser lido (a página exige JavaScript e só devolveu o rodapé da Anthropic). Você colou as charadas e as dicas em três estilos, e usei esse material.
2. **Primeira versão.** O jogador escolhia o título numa lista de 10 botões. Havia 5 dicas pagas (charada em dois passos, palavra a palavra, bíblica, do dia a dia).
3. **Discussão sobre IA.** Você cogitou usar o opencode-go para julgar respostas, com a chave digitada no início. Expliquei que no GitHub Pages isso é possível (a chave só na memória da aba), mas depende de a API aceitar chamadas do navegador (CORS), que não verifiquei. Você optou por uma comparação por script, sem IA.
4. **Entrevista das dicas.** Fizemos título por título; as respostas estão em `dicas.md`.
5. **Versão atual.** Campo de texto, comparação local, uma dica por música.

## Como o jogo funciona

- 10 rodadas, em ordem aleatória a cada partida. Não há repetição dentro de uma partida.
- A dica da música aparece desde o início, de graça. O título fica escondido.
- Começa com 1 nota. O botão "+ Mais uma nota" libera a seguinte (até 10) e toca de novo.
- Um acerto vale `10 − (notas extras) − (erros)`, com mínimo de 1 ponto.
- Cada erro custa 1 ponto. "Desistir" revela o título e vale 0.
- No fim das 10 rodadas aparece o total e o botão de jogar de novo.
- O tema segue o claro/escuro do aparelho e pode ser trocado pelo botão no rodapé.

## Comparação das respostas

Está em `index.html`, funções `norm`, `lev` e `matches`.

- Normaliza: minúsculas, remove acentos e pontuação, junta espaços.
- Aceita se a distância de edição (Levenshtein) for no máximo `floor(tamanho do título / 6)`, ou seja, cerca de um erro a cada 6 letras.
- Além do título completo, aceita variantes, no campo `a` de cada música:
  - "Vencendo vem"
  - "Esperança é Jesus"
  - "Vitória em nome"
- Testado: aceita "lado a lado", "Santo, santo, santo!", "esperanca e jesus", "marana ta"; recusa "santo", "minha luz" e o título de outra música.
- Para aceitar mais variantes, acrescente textos ao campo `a` da música em `SONGS`.

## Dicas em uso

Ver `dicas.md`. Resumo das escolhas:

- Textos do seu próprio punho: Lado a lado, Santo santo santo, Vencendo vem Jesus, Meu farol, Rumo ao lar, Maranata.
- Dica bíblica: Sou de Jesus.
- Charada completa: Canção da vida, Vitória em nome de Jesus.
- Do dia a dia: A esperança é Jesus.

Pequenos ajustes meus: "à frente" com crase (Lado a lado) e "bússola" no lugar de "bússula" (Rumo ao lar).

## Observações e pontos em aberto

- Os títulos estão no código da página. Quem abrir o código-fonte consegue lê-los (aceitável para uma brincadeira entre amigos).
- Os nomes dos arquivos são curtos (`esperanca`, `vitoria`, `vencendo-vem`, `cancao-vida`); os títulos completos vieram das charadas.
- Para mudar uma dica: editar o campo `h` da música em `SONGS` (em `index.html`) e, se quiser manter o registro, `dicas.md`.
- A comparação sem IA é rígida para respostas muito diferentes do título (por exemplo, sinônimos). Se isso atrapalhar, a ideia de IA com chave digitada no início continua possível (precisa testar CORS da API).
- Não implementado: ranking, modo de vários jogadores, dicas extras ou número de palavras/traços ao lado do campo.

## Para publicar mudanças

```
cd /home/mauricio/tmp/qual-e-o-louvor
git add -A && git commit -m "mensagem" && git push
```

A atualização aparece no site em alguns minutos.
