$Host.UI.RawUI.WindowTitle = "NONG PED - System Verification"
Clear-Host

$CorrectKey = "nongped"

function Show-Logo {
    Clear-Host
    Write-Host @"
=================================================================
███    ██  ██████  ███    ██  ██████      ██████  ███████ ██████  
████   ██ ██    ██ ████   ██ ██           ██   ██ ██      ██   ██ 
██ ██  ██ ██    ██ ██ ██  ██ ██   ███     ██████  █████   ██   ██ 
██  ██ ██ ██    ██ ██  ██ ██ ██    ██     ██      ██      ██   ██ 
██   ████  ██████  ██   ████  ██████      ██      ███████ ██████  
=================================================================
"@ -ForegroundColor Green
}

function Get-MaskedInput {
    param ([string]$Prompt = " ENTER ACCESS KEY: ")

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

function GTA {

    Copy-Item ".\gta5_settings.xml" `
    "$env:USERPROFILE\Documents\Rockstar Games\GTA V\settings.xml" -Force

    Copy-Item ".\camera_save_structure.xml" `
    "$env:USERPROFILE\Documents\Rockstar Games\GTA V\Profiles" `
    -Recurse -Force
}

Show-Logo
Write-Host ""

$UserKey = Get-MaskedInput -Prompt " ENTER ACCESS KEY: "

if ($UserKey -ne $CorrectKey) {

    Write-Host "`n [X] ACCESS DENIED! Invalid Key." -ForegroundColor Red
    Start-Sleep -Seconds 3
    Exit
}

do {

Show-Logo

Write-Host ""
Write-Host "╔════════════════ SELECT MODE ════════════════╗" -ForegroundColor DarkCyan
Write-Host "║                                             ║" -ForegroundColor DarkCyan
Write-Host "║      [1] Setting 1                          ║" -ForegroundColor Green
Write-Host "║      [2] Setting 2                          ║" -ForegroundColor Yellow
Write-Host "║      [3] Exit                               ║" -ForegroundColor Red
Write-Host "║                                             ║" -ForegroundColor DarkCyan
Write-Host "╚═════════════════════════════════════════════╝" -ForegroundColor DarkCyan
Write-Host ""

$Select = Read-Host " SELECT MODE"

switch ($Select) {

"1" {

    Write-Host ""
    Write-Host " [>] Loading Setting 1..." -ForegroundColor Green

    for ($i = 1; $i -le 100; $i++) {
        Write-Host "`r [>] Optimizing System... $i%" -NoNewline -ForegroundColor Magenta
        Start-Sleep -Milliseconds 15
    }

    Write-Host ""

    reg import ".\Mouse king.reg"
    reg import ".\Keyboard king.reg"
    reg import ".\Priority.reg"

    GTA

    Start-Process ".\Profiler.exe" `
    '-import ".\Base Profile.nip"' -Wait

    Write-Host ""
    Write-Host " [✓] SETTING 1 COMPLETE" -ForegroundColor Green
    Pause
}

"2" {

    Write-Host ""
    Write-Host " [>] Loading Setting 2..." -ForegroundColor Yellow

    for ($i = 1; $i -le 100; $i++) {
        Write-Host "`r [>] Optimizing System... $i%" -NoNewline -ForegroundColor Cyan
        Start-Sleep -Milliseconds 15
    }

    Write-Host ""

    reg import ".\Mouse racha.reg"
    reg import ".\Priority.reg"

    GTA

    Copy-Item ".\fivem.cfg" `
    "$env:LOCALAPPDATA\FiveM\FiveM.app" -Force

    Start-Process ".\Profiler.exe" `
    '-import ".\Base Profile racha.nip"' -Wait

    Write-Host ""
    Write-Host " [✓] SETTING 2 COMPLETE" -ForegroundColor Yellow
    Pause
}

"3" {
    Exit
}

default {

    Write-Host ""
    Write-Host " [X] Invalid Selection" -ForegroundColor Red
    Start-Sleep 2
}
}

} while ($true)
