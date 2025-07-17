
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
# VoiceTyper: Whisper Lokale Installation
# ==========================================

Write-Host "VoiceTyper: Whisper Lokale Installation" -ForegroundColor Cyan
Write-Host "==========================================" -ForegroundColor Cyan
Write-Host ""

# Pruefe, ob Python verfuegbar ist
try {
    $pythonVersion = python --version 2>$null
    if ($LASTEXITCODE -eq 0) {
        Write-Host "[OK] Python gefunden: $pythonVersion" -ForegroundColor Green
    } else {
        throw "Python nicht gefunden"
    }
} catch {
    Write-Host "[FEHLER] Python ist nicht installiert oder nicht im PATH." -ForegroundColor Red
    Write-Host "         Bitte installieren Sie Python von https://python.org" -ForegroundColor Yellow
    Write-Host "         Stellen Sie sicher, dass 'Add to PATH' aktiviert ist." -ForegroundColor Yellow
    exit 1
}

# Pruefe, ob pip verfuegbar ist
try {
    $pipVersion = pip --version 2>$null
    if ($LASTEXITCODE -eq 0) {
        Write-Host "[OK] pip gefunden: $pipVersion" -ForegroundColor Green
    } else {
        throw "pip nicht gefunden"
    }
} catch {
    Write-Host "[FEHLER] pip ist nicht verfuegbar." -ForegroundColor Red
    Write-Host "         pip sollte mit Python installiert werden." -ForegroundColor Yellow
    exit 1
}

Write-Host ""

# Installiere OpenAI Whisper
Write-Host "[INFO] Installiere OpenAI Whisper..." -ForegroundColor Yellow
try {
    pip install openai-whisper
    if ($LASTEXITCODE -eq 0) {
        Write-Host "[OK] OpenAI Whisper erfolgreich installiert!" -ForegroundColor Green
    } else {
        throw "Installation fehlgeschlagen"
    }
} catch {
    Write-Host "[FEHLER] Installation von OpenAI Whisper fehlgeschlagen." -ForegroundColor Red
    Write-Host "         Versuchen Sie: pip install --user openai-whisper" -ForegroundColor Yellow
    exit 1
}

Write-Host ""

# Pruefe FFmpeg
Write-Host "[INFO] Pruefe FFmpeg-Installation..." -ForegroundColor Yellow
try {
    $ffmpegVersion = ffmpeg -version 2>$null
    if ($LASTEXITCODE -eq 0) {
        Write-Host "[OK] FFmpeg ist bereits installiert" -ForegroundColor Green
    } else {
        throw "FFmpeg nicht gefunden"
    }
} catch {
    Write-Host "[WARNUNG] FFmpeg ist nicht installiert." -ForegroundColor Yellow
    Write-Host "          FFmpeg wird fuer optimale Audio-Verarbeitung benoetigt." -ForegroundColor White
    Write-Host ""
    Write-Host "          Installation unter Windows:" -ForegroundColor White
    Write-Host "          - Chocolatey: choco install ffmpeg" -ForegroundColor Cyan
    Write-Host "          - Scoop: scoop install ffmpeg" -ForegroundColor Cyan
    Write-Host "          - Manuell: https://ffmpeg.org/download.html" -ForegroundColor Cyan
    Write-Host ""
}

Write-Host ""
Write-Host "[ERFOLG] Whisper-Installation abgeschlossen!" -ForegroundColor Green
Write-Host ""
Write-Host "Verfuegbare Whisper-Modelle:" -ForegroundColor Cyan
Write-Host "   - tiny   (~39MB)  - Schnell, niedrige Genauigkeit" -ForegroundColor White
Write-Host "   - base   (~74MB)  - Ausgewogen (empfohlen fuer Start)" -ForegroundColor White  
Write-Host "   - small  (~244MB) - Gut, mehr Genauigkeit" -ForegroundColor White
Write-Host "   - medium (~769MB) - Sehr gut, hohe Genauigkeit" -ForegroundColor White
Write-Host "   - large  (~1.5GB) - Beste Genauigkeit, langsam" -ForegroundColor White
Write-Host "   - turbo  (~809MB) - Sehr gut und schnell" -ForegroundColor White
Write-Host ""
Write-Host "TIPP: Modelle werden beim ersten Gebrauch automatisch heruntergeladen." -ForegroundColor Yellow
Write-Host "TIPP: Starten Sie VoiceTyper neu und waehlen Sie 'Whisper (Lokal)' in den Einstellungen." -ForegroundColor Yellow
Write-Host ""

# Pause fuer Benutzer
Write-Host "Druecken Sie eine beliebige Taste zum Beenden..." -ForegroundColor Gray
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
