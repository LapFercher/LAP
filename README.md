Hier ist der gesamte Prozess als ein zusammenhängender Markdown-Abschnitt, den du direkt in deine `README.md` einfügen kannst:

```markdown
# SSH Agent Setup für GitHub (Windows)

Um GitHub über SSH auf einem Windows-Rechner zu verwenden, befolge diese Schritte:

### 1. SSH-Agent-Dienst aktivieren

- Öffne die **Dienste-Verwaltung**:
  - Drücke `Windows + R` und gebe `services.msc` ein.
- Suche nach dem Dienst **OpenSSH Authentication Agent**.
- Setze den **Starttyp** auf **Automatisch** und klicke auf **Starten**.

### 2. SSH-Key dem Agenten hinzufügen

- Starte den **SSH-Agent**:
  ```powershell
  Start-Service ssh-agent
  ```
- Füge deinen SSH-Schlüssel hinzu:
  ```powershell
  ssh-add $env:USERPROFILE\.ssh\id_rsa_lapfercher
  ```

### 3. Konfiguration der SSH `config`-Datei

- Öffne oder erstelle die `config`-Datei im Verzeichnis `~/.ssh/`:
  ```powershell
  notepad $env:USERPROFILE\.ssh\config
  ```
- Füge folgende Konfiguration hinzu, um GitHub über SSH mit dem richtigen Schlüssel zu verbinden:
  ```plaintext
  Host github.com-lapfercher
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_rsa_lapfercher
  ```

### 4. SSH-Verbindung testen

- Teste, ob die Verbindung zu GitHub funktioniert:
  ```powershell
  ssh -T git@github.com-lapfercher
  ```
  Du solltest folgende Nachricht erhalten:
  ```plaintext
  Hi LapFercher! You've successfully authenticated, but GitHub does not provide shell access.
  ```

### 5. Repository klonen

- Klone das Repository mit der SSH-URL:
  ```powershell
  git clone git@github.com-lapfercher:LapFercher/LAP.git
  ```

Mit diesen Schritten hast du die SSH-Authentifizierung für GitHub auf deinem Windows-Computer eingerichtet!
```
