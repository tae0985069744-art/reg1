$Host.UI.RawUI.WindowTitle="NONGSUNNY"
$Host.UI.RawUI.BackgroundColor="Black"
$Host.UI.RawUI.ForegroundColor="White"
Clear-Host

Write-Host ""

Write-Host "╔══════════════════════════════════════════════════════════════════╗" -ForegroundColor DarkCyan
Write-Host "║                     🦆 NONGSUNNY PANEL 🦆                      ║" -ForegroundColor Cyan
Write-Host "╚══════════════════════════════════════════════════════════════════╝" -ForegroundColor DarkCyan

Write-Host @"

                           __
                       ___( o)>
                       \ <_. )
                        `---'

███╗   ██╗ ██████╗ ███╗   ██╗ ███████╗██╗   ██╗███╗   ██╗███╗   ██╗██╗   ██╗
████╗  ██║██╔═══██╗████╗  ██║ ██╔════╝██║   ██║████╗  ██║████╗  ██║╚██╗ ██╔╝
██╔██╗ ██║██║   ██║██╔██╗ ██║ ███████╗██║   ██║██╔██╗ ██║██╔██╗ ██║ ╚████╔╝
██║╚██╗██║██║   ██║██║╚██╗██║ ╚════██║██║   ██║██║╚██╗██║██║╚██╗██║  ╚██╔╝
██║ ╚████║╚██████╔╝██║ ╚████║ ███████║╚██████╔╝██║ ╚████║██║ ╚████║   ██║
╚═╝  ╚═══╝ ╚═════╝ ╚═╝  ╚═══╝ ╚══════╝ ╚═════╝ ╚═╝  ╚═══╝╚═╝  ╚═══╝   ╚═╝

"@ -ForegroundColor Cyan

Write-Host "╔════════════════ SELECT MODE ════════════════╗" -ForegroundColor DarkYellow
Write-Host "║                                             ║" -ForegroundColor DarkYellow
Write-Host "║      [1] 🟢 Setting 1                       ║" -ForegroundColor Green
Write-Host "║      [2] 🟡 Setting 2                       ║" -ForegroundColor Yellow
Write-Host "║      [3] 🔴 Exit                            ║" -ForegroundColor Red
Write-Host "║                                             ║" -ForegroundColor DarkYellow
Write-Host "╚═════════════════════════════════════════════╝" -ForegroundColor DarkYellow
Write-Host ""

function GTA{
cp ".\gta5_settings.xml" `
"$env:USERPROFILE\Documents\Rockstar Games\GTA V\settings.xml" -Force

cp ".\camera_save_structure.xml" `
"$env:USERPROFILE\Documents\Rockstar Games\GTA V\Profiles" `
-Recurse -Force
}

switch(Read-Host "Select"){

1{

Write-Host "`n🦆 Loading Setting 1..." -ForegroundColor Green

reg import ".\Mouse king.reg"
reg import ".\Keyboard king.reg"
reg import ".\Priority.reg"

GTA

Start-Process ".\Profiler.exe" `
'-import ".\Base Profile.nip"' -Wait

Write-Host "`n[✓] SETTING 1 COMPLETE" -ForegroundColor Green
}

2{

Write-Host "`n🦆 Loading Setting 2..." -ForegroundColor Yellow

reg import ".\Mouse racha.reg"
reg import ".\Priority.reg"

GTA

cp ".\fivem.cfg" `
"$env:LOCALAPPDATA\FiveM\FiveM.app" -Force

Start-Process ".\Profiler.exe" `
'-import ".\Base Profile racha.nip"' -Wait

Write-Host "`n[✓] SETTING 2 COMPLETE" -ForegroundColor Yellow
}

default{
exit
}

}

Write-Host ""
Write-Host "╔═════════════════════════════════════════════╗" -ForegroundColor DarkCyan
Write-Host "║        🦆 Optimization Complete 🦆         ║" -ForegroundColor Cyan
Write-Host "╚═════════════════════════════════════════════╝" -ForegroundColor DarkCyan

Start-Sleep 2
