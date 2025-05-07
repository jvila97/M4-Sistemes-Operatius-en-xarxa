# Documentació de l'Activitat 6 Seguretat Informàtica  
**Mòdul 6 - Firewalls**  
**Nom:** Jan Vilaplana Bages
**Data:** 07/05/2025

---

## Part 1: Configuració de PeerBlock (Firewall)

### 1. Instal·lació
- Descarregat des de [peerblock.com](https://www.peerblock.com)
- Procés d'instal·lació estàndard (sense bloatware)

### 2. Configuració bàsica
'bash'
Llistes activades:
✓ P2P (bloqueig xarxes compartició)
✓ Ads (bloqueig publicitat)
✓ Spyware (bloqueig amenaces)

Ports oberts:
- 80 (HTTP)
- 443 (HTTPS)
Ports bloquejats:
- Entrants no autoritzats

### 3. Codi del script

# network_report.ps1
$logDir = "C:\log_[nom]"
if (!(Test-Path $logDir)) { 
    New-Item -ItemType Directory -Path $logDir
    icacls $logDir /grant:r "admin_[nom]:(OI)(CI)F" /remove "Tots"
}

$date = Get-Date -Format "yyyyMMdd_HHmmss"
$logFile = "$logDir\network_report_$date.txt"

@"
=== Informació Xarxa ===
$(ipconfig /all)

=== Taula Encaminament ===
$(route print)

=== Connexions Actives ===
$(netstat -ano)
"@ | Out-File $logFile
