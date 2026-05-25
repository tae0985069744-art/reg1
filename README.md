$Host.UI.RawUI.WindowTitle = "NONG KIM - System Verification"
Clear-Host

$CorrectKey = "nongkim"

function Show-Logo {
    Clear-Host
    Write-Host @"
=================================================================
███    ██  ██████  ███    ██  ██████      ██   ██  ██ ███    ███ 
████   ██ ██    ██ ████   ██ ██           ██  ██   ██ ████  ████ 
██ ██  ██ ██    ██ ██ ██  ██ ██   ███     █████    ██ ██ ████ ██ 
██  ██ ██ ██    ██ ██  ██ ██ ██    ██     ██  ██   ██ ██  ██  ██ 
██   ████  ██████  ██   ████  ██████      ██   ██  ██ ██      ██ 
=================================================================
"@ -ForegroundColor Green
}

function Get-MaskedInput {
    param ([string]$Prompt = " Enter Access Key: ")
    Write-Host $Prompt -NoNewline -ForegroundColor Cyan
    $Password = New-Object System.Security.SecureString
    while ($true) {
        $Key = [Console]::ReadKey($true)
        if ($Key.Key -eq [ConsoleKey]::Enter) {
            Write-Host ""
            break
        }
        elseif ($Key.Key -eq [ConsoleKey]::Backspace) {
            if ($Password.Length -gt 0) {
                $Password.RemoveAt($Password.Length - 1)
                Write-Host "`b `b" -NoNewline
            }
        }
        elseif ($Key.KeyChar -ne [char]0) {
            $Password.AppendChar($Key.KeyChar)
            Write-Host "★" -NoNewline -ForegroundColor Yellow
        }
    }
    $BSTR = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($Password)
    $PlainPassword = [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($BSTR)
    return $PlainPassword
}

Show-Logo
Write-Host ""

$UserKey = Get-MaskedInput -Prompt "ENTER ACCESS KEY:"

if ($UserKey -ne $CorrectKey) {
    Write-Host "`n [X] ACCESS DENIED! Invalid Key. Exiting..." -ForegroundColor Red
    Start-Sleep -Seconds 3
    Exit
}

Show-Logo
Write-Host " [✓] Access Granted! Initializing Tweaks..." -ForegroundColor Green
Write-Host " -------------------------------------------------------" -ForegroundColor Cyan
Write-Host ""

for ($i = 1; $i -le 100; $i++) {
    Write-Host "`r [>] Optimizing System Registry... Progress: $i%" -ForegroundColor Magenta -NoNewline
    
reg import ".\Mouse king.reg"
reg import ".\Keyboard king.reg"
reg import ".\Priority.reg"

GTA

Start-Process ".\Profiler.exe" `
'-import ".\Base Profile.nip"' -Wait

Write-Host ""
Write-Host "[✓] SETTING 1 COMPLETE" -ForegroundColor Green
}

2{

Login

Write-Host ""
Write-Host "[+] Loading Setting 2..." -ForegroundColor Yellow
Start-Sleep 1

reg import ".\Mouse racha.reg"
reg import ".\Priority.reg"

GTA

cp ".\fivem.cfg" `
"$env:LOCALAPPDATA\FiveM\FiveM.app" -Force

Start-Process ".\Profiler.exe" `
'-import ".\Base Profile racha.nip"' -Wait

Write-Host ""
Write-Host "[✓] SETTING 2 COMPLETE" -ForegroundColor Yellow
}

default{
exit
}

}

Write-Host ""
Write-Host "╔═════════════════════════════════════════════╗" -ForegroundColor DarkCyan
Write-Host "║            Optimization Complete           ║" -ForegroundColor Cyan
Write-Host "╚═════════════════════════════════════════════╝" -ForegroundColor DarkCyan

Start-Sleep 2
