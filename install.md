
### 1. Whisper installieren

**Linux/macOS:**
```bash
chmod +x install_whisper.sh
./install_whisper.sh
```

**Windows:**
```powershell
powershell -ExecutionPolicy Bypass -File install_whisper.ps1
```

**Manuell:**
```bash
pip install openai-whisper
```





<br><br>
<br><br>

install_whisper.ps1:

<details><summary>Click to expand..</summary>

```powershell
#!/usr/bin/env powershell

Write-Host "🔧 VoiceTyper: Whisper Lokale Installation" -ForegroundColor Cyan
Write-Host "==========================================" -ForegroundColor Cyan
Write-Host ""

# Prüfe, ob Python verfügbar ist
try {
    $pythonVersion = python --version 2>$null
    if ($LASTEXITCODE -eq 0) {
        Write-Host "✅ Python gefunden: $pythonVersion" -ForegroundColor Green
    } else {
        throw "Python nicht gefunden"
    }
} catch {
    Write-Host "❌ Python ist nicht installiert oder nicht im PATH." -ForegroundColor Red
    Write-Host "   Bitte installieren Sie Python von https://python.org" -ForegroundColor Yellow
    Write-Host "   Stellen Sie sicher, dass 'Add to PATH' aktiviert ist." -ForegroundColor Yellow
    exit 1
}

# Prüfe, ob pip verfügbar ist
try {
    $pipVersion = pip --version 2>$null
    if ($LASTEXITCODE -eq 0) {
        Write-Host "✅ pip gefunden: $pipVersion" -ForegroundColor Green
    } else {
        throw "pip nicht gefunden"
    }
} catch {
    Write-Host "❌ pip ist nicht verfügbar." -ForegroundColor Red
    Write-Host "   pip sollte mit Python installiert werden." -ForegroundColor Yellow
    exit 1
}

Write-Host ""

# Installiere OpenAI Whisper
Write-Host "🔄 Installiere OpenAI Whisper..." -ForegroundColor Yellow
try {
    pip install openai-whisper
    if ($LASTEXITCODE -eq 0) {
        Write-Host "✅ OpenAI Whisper erfolgreich installiert!" -ForegroundColor Green
    } else {
        throw "Installation fehlgeschlagen"
    }
} catch {
    Write-Host "❌ Installation von OpenAI Whisper fehlgeschlagen." -ForegroundColor Red
    Write-Host "   Versuchen Sie: pip install --user openai-whisper" -ForegroundColor Yellow
    exit 1
}

Write-Host ""

# Prüfe FFmpeg
Write-Host "🔄 Prüfe FFmpeg-Installation..." -ForegroundColor Yellow
try {
    $ffmpegVersion = ffmpeg -version 2>$null
    if ($LASTEXITCODE -eq 0) {
        Write-Host "✅ FFmpeg ist bereits installiert" -ForegroundColor Green
    } else {
        throw "FFmpeg nicht gefunden"
    }
} catch {
    Write-Host "⚠️ FFmpeg ist nicht installiert." -ForegroundColor Yellow
    Write-Host "   FFmpeg wird für optimale Audio-Verarbeitung benötigt." -ForegroundColor White
    Write-Host ""
    Write-Host "   Installation unter Windows:" -ForegroundColor White
    Write-Host "   - Chocolatey: choco install ffmpeg" -ForegroundColor Cyan
    Write-Host "   - Scoop: scoop install ffmpeg" -ForegroundColor Cyan
    Write-Host "   - Manuell: https://ffmpeg.org/download.html" -ForegroundColor Cyan
    Write-Host ""
}

Write-Host ""
Write-Host "🎉 Whisper-Installation abgeschlossen!" -ForegroundColor Green
Write-Host ""
Write-Host "📋 Verfügbare Whisper-Modelle:" -ForegroundColor Cyan
Write-Host "   - tiny   (~39MB)  - Schnell, niedrige Genauigkeit" -ForegroundColor White
Write-Host "   - base   (~74MB)  - Ausgewogen (empfohlen für Start)" -ForegroundColor White  
Write-Host "   - small  (~244MB) - Gut, mehr Genauigkeit" -ForegroundColor White
Write-Host "   - medium (~769MB) - Sehr gut, hohe Genauigkeit" -ForegroundColor White
Write-Host "   - large  (~1.5GB) - Beste Genauigkeit, langsam" -ForegroundColor White
Write-Host "   - turbo  (~809MB) - Sehr gut und schnell" -ForegroundColor White
Write-Host ""
Write-Host "💡 Tipp: Modelle werden beim ersten Gebrauch automatisch heruntergeladen." -ForegroundColor Yellow
Write-Host "💡 Starten Sie VoiceTyper neu und wählen Sie 'Whisper (Lokal)' in den Einstellungen." -ForegroundColor Yellow
Write-Host ""

# Pause für Benutzer
Write-Host "Drücken Sie eine beliebige Taste zum Beenden..." -ForegroundColor Gray
$null = $Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown") 
```

</details>




<br><br>
<br><br>

install_whisper.sh:

<details><summary>Click to expand..</summary>

```bash
#!/bin/bash

echo "🔧 VoiceTyper: Whisper Lokale Installation"
echo "=========================================="
echo ""

# Prüfe, ob Python verfügbar ist
if ! command -v python3 &> /dev/null; then
    echo "❌ Python3 ist nicht installiert. Bitte installieren Sie Python3 zuerst."
    exit 1
fi

# Prüfe, ob pip verfügbar ist
if ! command -v pip3 &> /dev/null; then
    echo "❌ pip3 ist nicht installiert. Bitte installieren Sie pip3 zuerst."
    exit 1
fi

echo "✅ Python3 und pip3 gefunden"
echo ""

# Installiere OpenAI Whisper
echo "🔄 Installiere OpenAI Whisper..."
pip3 install openai-whisper

if [ $? -eq 0 ]; then
    echo "✅ OpenAI Whisper erfolgreich installiert!"
else
    echo "❌ Installation von OpenAI Whisper fehlgeschlagen."
    exit 1
fi

echo ""

# Prüfe FFmpeg
echo "🔄 Prüfe FFmpeg-Installation..."
if command -v ffmpeg &> /dev/null; then
    echo "✅ FFmpeg ist bereits installiert"
else
    echo "⚠️ FFmpeg ist nicht installiert."
    echo "   FFmpeg wird für optimale Audio-Verarbeitung benötigt."
    echo ""
    echo "   Installation unter verschiedenen Systemen:"
    echo "   - Ubuntu/Debian: sudo apt update && sudo apt install ffmpeg"
    echo "   - macOS (Homebrew): brew install ffmpeg" 
    echo "   - Windows (Chocolatey): choco install ffmpeg"
    echo "   - Windows (Scoop): scoop install ffmpeg"
    echo ""
fi

echo ""
echo "🎉 Whisper-Installation abgeschlossen!"
echo ""
echo "📋 Verfügbare Whisper-Modelle:"
echo "   - tiny   (~39MB)  - Schnell, niedrige Genauigkeit"
echo "   - base   (~74MB)  - Ausgewogen (empfohlen für Start)"
echo "   - small  (~244MB) - Gut, mehr Genauigkeit"
echo "   - medium (~769MB) - Sehr gut, hohe Genauigkeit"
echo "   - large  (~1.5GB) - Beste Genauigkeit, langsam"
echo "   - turbo  (~809MB) - Sehr gut und schnell"
echo ""
echo "💡 Tipp: Modelle werden beim ersten Gebrauch automatisch heruntergeladen."
echo "💡 Starten Sie VoiceTyper neu und wählen Sie 'Whisper (Lokal)' in den Einstellungen."
echo "" 
```

</details>
