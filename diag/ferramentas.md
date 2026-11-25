# Diagnóstico: ferramentas disponíveis nas tarefas agendadas

Data: 2026-11-25 · Sessão: tarefa agendada na cloud (projeto "IC App") · Modelo configurado: claude-opus-5-5

Nada na app foi alterado. Só se recolheu informação e se publicou uma página de teste privada e separada.

## 1. Ferramentas encontradas

### `mcp__claude-artifacts__*`: NÃO EXISTEM nesta sessão
Pesquisas feitas com ToolSearch: `claude-artifacts`, `+claude-artifacts publish`, `publish_version`, `db_write`, `artifact`, `database write artifact data`.
- `claude-artifacts` → "No matching deferred tools found"
- `publish_version` → "No matching deferred tools found"
- `db_write` → "No matching deferred tools found"
- `+claude-artifacts publish` → "No matching deferred tools found"

Ou seja, não há `mcp__claude-artifacts__publish_version`, `mcp__claude-artifacts__db_write`, `list_types`, `create_from_type`, etc.

### Equivalentes nativos (sem prefixo `mcp__`)
- **`Artifact`**: publica, lê, lista, apaga, abre, fixa páginas (ações `publish`, `read`, `list`, `delete`, `open`, `pin`, `unpin`, `quickstart`). Publica a partir de um **ficheiro local** (`file_path`), não de um parâmetro `content`. Atualizar um artefacto existente: `url` + `file_path` (é preciso fazer `read` primeiro).
- **`ArtifactData`**: base de dados partilhada de um artefacto (ações `get`, `list`, `query`, `set`, `update`, `str_replace`, `delete`, `batch`, `profiles`). É o equivalente a `read_db`/`write_db`. **Existe; não foi usado para escrever nada.**
- **`ArtifactComments`**: ler/responder/resolver comentários e gerir "watches".

### `mcp__Claude_Docs__*` (existem)
- `mcp__Claude_Docs__batch` (carregada)
- `mcp__Claude_Docs__guide` (carregada)
- `mcp__Claude_Docs__update` (carregada)
- `mcp__Claude_Docs__create` (diferida)
- `mcp__Claude_Docs__delete` (diferida)
- `mcp__Claude_Docs__export` (diferida)
- `mcp__Claude_Docs__query` (diferida)
- `mcp__Claude_Docs__read` (diferida)

### Outras `mcp__*` presentes
- **memory**: `mcp__memory__memory_list`, `memory_read`, `memory_write`, `memory_str_replace`, `memory_append`, `memory_delete` (diferida)
- **claude-code-remote**: `mcp__claude-code-remote__create_trigger`, `delete_trigger`, `fire_trigger`, `list_triggers`, `send_later`, `update_trigger`
- **github**: `mcp__github__actions_get`, `actions_list`, `actions_run_trigger`, `add_comment_to_pending_review`, `add_issue_comment`, `add_reply_to_pull_request_comment`, `create_branch`, `create_or_update_file`, `create_pull_request`, `create_repository`, `delete_file`, `disable_pr_auto_merge`, `enable_pr_auto_merge`, `fork_repository`, `get_check_run`, `get_commit`, `get_file_contents`, `get_job_logs`, `get_label`, `get_latest_release`, `get_me`, `get_release_by_tag`, `get_tag`, `get_team_members`, `get_teams`, `issue_read`, `issue_write`, `list_branches`, `list_commits`, `list_issue_fields`, `list_issue_types`, `list_issues`, `list_pull_requests`, `list_releases`, `list_repository_collaborators`, `list_tags`, `merge_pull_request`, `pull_request_read`, `pull_request_review_write`, `push_files`, `request_copilot_review`, `resolve_review_thread`, `run_secret_scanning`, `sub_issue_write`, `subscribe_pr_activity`, `unresolve_review_thread`, `unsubscribe_pr_activity`, `update_issue_comment`, `update_pull_request`, `update_pull_request_branch`
- **Gmail**: `mcp__Gmail__*` (create_draft, send_message, search_threads, get_message, get_thread, labels, trash, spam, etc.)
- **Microsoft_365**: `mcp__Microsoft_365__*` (chat_message_search, find_meeting_availability, get_me, sharepoint_*, search_people, read_resource, get_granted_scopes)
- **Miro**: `mcp__Miro__*` (board_*, canvas_*, comment_*, image_*, section_*, space_*, etc.)

Outras ferramentas diferidas não-MCP: ArtifactComments, ArtifactData, CronCreate/Delete/List, DesignSync, EnterWorktree/ExitWorktree, ListConnectors, ListPlugins, ListSkills, Monitor, NotebookEdit, SearchMcpRegistry, SearchPlugins, SearchSkills, SendMessage, SuggestConnectors, SuggestPluginInstall, SuggestSkills, TaskCreate/Get/List/Stop/Update, WebSearch, ListMcpResourcesTool, ReadMcpResourceTool, ReadMcpResourceDirTool.

## 2. Teste de publicação

Como `mcp__claude-artifacts__publish_version` não existe, usou-se a ferramenta `Artifact` (ação `publish`), com o HTML pedido gravado num ficheiro temporário.

- Parâmetros: `file_path` (ficheiro com o HTML pedido), `title: "IC — teste de publicação"`, `icon: "test"`
- Resultado: **sucesso, sem erros**
- URL: https://claude.ai/artifact/BW8rFZQnZPSAm3xay7cS5J
- Slug: `BW8rFZQnZPSAm3xay7cS5J`
- Versão: `Version 1`, version id `1795618919-adfc`
- Privado (só o dono abre o link)
- Nota textual devolvida: "Live subscription: not supported yet from remote sessions — nothing notifies this session of new versions or of comments sent to Claude"

## 3. Base de dados

- `mcp__claude-artifacts__db_write`: não existe.
- `ArtifactData` (equivalente, com `set`/`update`/`batch`/…): existe. Não se escreveu nada.

## Conclusão para a app IC

Nas tarefas agendadas, publicar/atualizar páginas faz-se com `Artifact` (a partir de ficheiro, `url` para atualizar uma existente depois de `read`) e escrever na base de dados com `ArtifactData`. Os prompts que referem `mcp__claude-artifacts__publish_version` / `db_write` têm de passar a usar estes nomes.
