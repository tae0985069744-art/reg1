# =========================
#         NONGPED
# =========================

$Host.UI.RawUI.WindowTitle = "NONGPED"
$Host.UI.RawUI.BackgroundColor = "Black"
$Host.UI.RawUI.ForegroundColor = "White"

# ---------- LOGIN ----------
function Login {

    Clear-Host

    Write-Host ""
    Write-Host "╔════════════════════════════════════╗" -ForegroundColor DarkCyan
    Write-Host "║           NONGPED LOGIN           ║" -ForegroundColor Cyan
    Write-Host "╚════════════════════════════════════╝" -ForegroundColor DarkCyan
    Write-Host ""

    $secure = Read-Host "Enter Key" -AsSecureString

    $BSTR = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($secure)
    $key = [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($BSTR)

    if ($key -ne "Nongped") {

        Write-Host ""
        Write-Host "[!] Invalid Key" -ForegroundColor Red

        Start-Sleep 2

        Login
    }
}

# ---------- GTA SETTINGS ----------
function GTA {

    Copy-Item ".\gta5_settings.xml" `
    "$env:USERPROFILE\Documents\Rockstar Games\GTA V\settings.xml" `
    -Force

    Copy-Item ".\camera_save_structure.xml" `
    "$env:USERPROFILE\Documents\Rockstar Games\GTA V\Profiles" `
    -Recurse -Force
}

# ---------- PRIORITY ----------
function Priority {

    reg add "HKLM\SYSTEM\CurrentControlSet\Control\PriorityControl" `
    /v Win32PrioritySeparation `
    /t REG_DWORD `
    /d 42 `
    /f | Out-Null
}

# ---------- LOGIN ----------
Login

Clear-Host

# ---------- HEADER ----------
Write-Host ""
Write-Host "╔══════════════════════════════════════════════════════════════════╗" -ForegroundColor DarkCyan
Write-Host "║                          NONGPED PANEL                         ║" -ForegroundColor Cyan
Write-Host "╚══════════════════════════════════════════════════════════════════╝" -ForegroundColor DarkCyan

Write-Host @"

                           __
                       ___( o)>
                       \ <_. )
                        `---'

███╗   ██╗ ██████╗ ███╗   ██╗ ██████╗ ██████╗ ███████╗██████╗
████╗  ██║██╔═══██╗████╗  ██║██╔════╝ ██╔══██╗██╔════╝██╔══██╗
██╔██╗ ██║██║   ██║██╔██╗ ██║██║  ███╗██████╔╝█████╗  ██║  ██║
██║╚██╗██║██║   ██║██║╚██╗██║██║   ██║██╔═══╝ ██╔══╝  ██║  ██║
██║ ╚████║╚██████╔╝██║ ╚████║╚██████╔╝██║     ███████╗██████╔╝
╚═╝  ╚═══╝ ╚═════╝ ╚═╝  ╚═══╝ ╚═════╝ ╚═╝     ╚══════╝╚═════╝

"@ -ForegroundColor Cyan

# ---------- MENU ----------
Write-Host "╔════════════════ SELECT MODE ════════════════╗" -ForegroundColor DarkYellow
Write-Host "║                                             ║" -ForegroundColor DarkYellow
Write-Host "║      [1] Setting 1  - FPS BOOST             ║" -ForegroundColor Green
Write-Host "║      [2] Setting 2  - RACHA BOOST           ║" -ForegroundColor Yellow
Write-Host "║      [3] Exit                               ║" -ForegroundColor Red
Write-Host "║                                             ║" -ForegroundColor DarkYellow
Write-Host "╚═════════════════════════════════════════════╝" -ForegroundColor DarkYellow
Write-Host ""

$select = Read-Host "Select"

switch ($select) {

# =========================
#       SETTING 1
# =========================
"1" {

    Write-Host ""
    Write-Host "[+] Loading Setting 1..." -ForegroundColor Green
    Start-Sleep 1

    reg import ".\Mouse king.reg"      | Out-Null
    reg import ".\Keyboard king.reg"   | Out-Null
    reg import ".\Priority.reg"        | Out-Null

    Priority
    GTA

    Start-Process ".\Profiler.exe" `
    '-import ".\Base Profile.nip"' `
    -Wait

    Write-Host ""
    Write-Host "[✓] SETTING 1 COMPLETE" -ForegroundColor Green
}

# =========================
#       SETTING 2
# =========================
"2" {

    Write-Host ""
    Write-Host "[+] Loading Setting 2..." -ForegroundColor Yellow
    Start-Sleep 1

    reg import ".\Mouse racha.reg" | Out-Null
    reg import ".\Priority.reg"    | Out-Null

    Priority
    GTA

    Copy-Item ".\fivem.cfg" `
    "$env:LOCALAPPDATA\FiveM\FiveM.app" `
    -Force

    Start-Process ".\Profiler.exe" `
    '-import ".\Base Profile racha.nip"' `
    -Wait

    Write-Host ""
    Write-Host "[✓] SETTING 2 COMPLETE" -ForegroundColor Yellow
}

# =========================
#          EXIT
# =========================
default {
    exit
}
}

# ---------- END ----------
Write-Host ""
Write-Host "╔═════════════════════════════════════════════╗" -ForegroundColor DarkCyan
Write-Host "║            Optimization Complete           ║" -ForegroundColor Cyan
Write-Host "╚═════════════════════════════════════════════╝" -ForegroundColor DarkCyan

Start-Sleep 2
