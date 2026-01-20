# Claude Sessions

Gestionnaire de sessions Claude Code pour iTerm2 sur macOS.

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
