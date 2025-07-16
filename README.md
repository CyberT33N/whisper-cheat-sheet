# whisper-cheat-sheet


## 📊 Whisper-Modelle im Vergleich

| Modell   | Größe  | Geschwindigkeit | Genauigkeit | VRAM   | Empfehlung |
|----------|--------|-----------------|-------------|--------|------------|
| `tiny`   | ~39MB  | ~10x           | Niedrig     | ~1GB   | Testing    |
| `base`   | ~74MB  | ~7x            | Mittel      | ~1GB   | **Start**  |
| `small`  | ~244MB | ~4x            | Gut         | ~2GB   | Ausgewogen |
| `medium` | ~769MB | ~2x            | Sehr gut    | ~5GB   | Qualität   |
| `large`  | ~1.5GB | 1x             | Excellent   | ~10GB  | Beste      |
| `turbo`  | ~809MB | ~8x            | Sehr gut    | ~6GB   | **Empfohlen** |

### 🎯 Modell-Empfehlungen:

- **Einsteiger**: `base` - Guter Kompromiss zwischen Geschwindigkeit und Qualität
- **Beste Balance**: `turbo` - Sehr gute Qualität bei hoher Geschwindigkeit
- **Maximale Qualität**: `large` - Beste Ergebnisse, braucht mehr Zeit
- **Schwache Hardware**: `tiny` - Für sehr langsame Computer

---

## ⚙️ Systemanforderungen

### Minimum:
- **CPU**: Moderne CPU (2015+)
- **RAM**: 2GB verfügbar
- **Speicher**: 500MB für kleinste Modelle
- **Python**: 3.8+

### Empfohlen:
- **CPU**: Multi-Core Prozessor
- **RAM**: 8GB+ 
- **GPU**: Nvidia GPU mit CUDA (optional, aber deutlich schneller)
- **Speicher**: 2GB für größere Modelle

### GPU-Beschleunigung:
Whisper nutzt automatisch verfügbare GPUs:
- **Nvidia**: CUDA (automatisch erkannt)
- **AMD**: ROCm (experimentell)
- **Apple Silicon**: Metal Performance Shaders (automatisch)
