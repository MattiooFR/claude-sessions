# Claude Sessions

> **macOS only** | **Claude Code** | **iTerm2**

Session manager for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) on [iTerm2](https://iterm2.com/) for macOS.

List, save, kill, and restore active Claude Code sessions in iTerm2.

## Installation

1. Clone the repository:
```bash
git clone https://github.com/MattiooFR/claude-sessions.git
cd claude-sessions
```

2. Make the script executable (if not already):
```bash
chmod +x claude-sessions
```

3. Create a symbolic link to use the command globally:
```bash
# Option 1: In /usr/local/bin (recommended)
sudo ln -s "$(pwd)/claude-sessions" /usr/local/bin/claude-sessions

# Option 2: In ~/.local/bin (no sudo, make sure this folder is in your PATH)
mkdir -p ~/.local/bin
ln -s "$(pwd)/claude-sessions" ~/.local/bin/claude-sessions
```

4. Verify the installation:
```bash
claude-sessions help
```

## Usage

### List active sessions

```bash
# Sessions in the current iTerm2 window
claude-sessions list

# Sessions in all iTerm2 windows
claude-sessions list --all
```

### Save sessions

```bash
# Save sessions from the current window
claude-sessions save

# Save all sessions
claude-sessions save --all
```

Each session receives a unique identifier via Claude Code's `/rename` command. Sessions are stored in `~/.claude/saved-sessions.json`.

### Kill sessions

```bash
# Kill sessions in the current window (auto-saves before killing)
claude-sessions kill

# Kill all sessions
claude-sessions kill --all
```

### Restore sessions

```bash
claude-sessions restore
```

Opens a new iTerm2 tab for each saved session and runs `claude --resume <session-id>`.

## Requirements

- macOS
- iTerm2
- Claude Code CLI
- `jq` (for JSON parsing)

```bash
brew install jq
```

## How it works

1. **List**: Finds `claude` processes attached to iTerm2 TTYs
2. **Save**: Sends `/rename <id>` to each session via AppleScript
3. **Kill**: Saves then sends SIGTERM to Claude processes
4. **Restore**: Opens tabs and runs `claude --resume <id>`

---

# Claude Sessions (Français)

> **macOS uniquement** | **Claude Code** | **iTerm2**

Gestionnaire de sessions [Claude Code](https://docs.anthropic.com/en/docs/claude-code) pour [iTerm2](https://iterm2.com/) sur macOS.

Permet de lister, sauvegarder, tuer et restaurer des sessions Claude Code actives dans iTerm2.

## Installation

1. Cloner le repository :
```bash
git clone https://github.com/MattiooFR/claude-sessions.git
cd claude-sessions
```

2. Rendre le script exécutable (si ce n'est pas déjà fait) :
```bash
chmod +x claude-sessions
```

3. Créer un lien symbolique pour utiliser la commande globalement :
```bash
# Option 1 : Dans /usr/local/bin (recommandé)
sudo ln -s "$(pwd)/claude-sessions" /usr/local/bin/claude-sessions

# Option 2 : Dans ~/.local/bin (sans sudo, assurez-vous que ce dossier est dans votre PATH)
mkdir -p ~/.local/bin
ln -s "$(pwd)/claude-sessions" ~/.local/bin/claude-sessions
```

4. Vérifier l'installation :
```bash
claude-sessions help
```

## Utilisation

### Lister les sessions actives

```bash
# Sessions dans la fenêtre iTerm2 courante
claude-sessions list

# Sessions dans toutes les fenêtres iTerm2
claude-sessions list --all
```

### Sauvegarder les sessions

```bash
# Sauvegarder les sessions de la fenêtre courante
claude-sessions save

# Sauvegarder toutes les sessions
claude-sessions save --all
```

Chaque session reçoit un identifiant unique via la commande `/rename` de Claude Code. Les sessions sont enregistrées dans `~/.claude/saved-sessions.json`.

### Tuer les sessions

```bash
# Tuer les sessions de la fenêtre courante (sauvegarde automatique avant)
claude-sessions kill

# Tuer toutes les sessions
claude-sessions kill --all
```

### Restaurer les sessions

```bash
claude-sessions restore
```

Ouvre un nouvel onglet iTerm2 pour chaque session sauvegardée et exécute `claude --resume <session-id>`.

## Prérequis

- macOS
- iTerm2
- Claude Code CLI
- `jq` (pour le parsing JSON)

```bash
brew install jq
```

## Fonctionnement

1. **Liste** : Trouve les processus `claude` attachés aux TTY d'iTerm2
2. **Sauvegarde** : Envoie `/rename <id>` à chaque session via AppleScript
3. **Kill** : Sauvegarde puis envoie SIGTERM aux processus Claude
4. **Restauration** : Ouvre des onglets et lance `claude --resume <id>`
