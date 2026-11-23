# IC — Central Claude

App pessoal (PWA) com uma edição por dia: poema, notícias, obra, "Aprende", ciência e radar de oportunidades. Sem scroll infinito.

- **Site:** https://ivofr17-debug.github.io/ic/ — no iPhone: Safari → Partilhar → *Adicionar ao ecrã principal*.
- **Conteúdo:** escrito por tarefas agendadas do Claude, que fazem commit em `data/`:
  - `data/news.json` — todos os dias de manhã e às 19h
  - `data/ciencia.json` — terças e sextas
  - `data/weekly.json` — domingos (poemas, obras, lições, radar)
- **`state.json`** — o teu feedback ("Mais/Menos disto") e progresso; escrito pela app quando há uma chave do GitHub nas Definições.
- **Conversar:** abre o Claude Desktop (`claude://`) no PC ou a app do Claude no telemóvel, com o contexto já escrito.

Não edites os ficheiros de `data/` à mão: são reescritos pelas tarefas.
