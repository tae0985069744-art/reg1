# ==================================================
#                 NONGPED SYSTEM V2
# ==================================================

$Host.UI.RawUI.WindowTitle="NONGPED SYSTEM"

[console]::BackgroundColor = "Black"
[console]::ForegroundColor = "White"
cls

# ==================================================
# ADMIN CHECK
# ==================================================

$currentUser = New-Object Security.Principal.WindowsPrincipal([Security.Principal.WindowsIdentity]::GetCurrent())

if (-not $currentUser.IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)) {

    Write-Host ""
    Write-Host "[!] PLEASE RUN AS ADMINISTRATOR" -ForegroundColor Red
    Write-Host ""

    Pause
    Exit
}

# ==================================================
# LOGIN SYSTEM
# ==================================================

Write-Host "+==============================================================+" -ForegroundColor Cyan
Write-Host "|                                                              |" -ForegroundColor Cyan
Write-Host "|                  P R E M I U M   S Y S T E M                 |" -ForegroundColor Gray
Write-Host "|                                                              |" -ForegroundColor Cyan
Write-Host "+==============================================================+" -ForegroundColor Cyan
Write-Host ""

$key = Read-Host "A C C E S S   K E Y"

if ($key -ne "NONGPED") {

    Write-Host "`n[x] INVALID KEY! Access Denied." -ForegroundColor Red
    Start-Sleep -Seconds 2
    exit
}

# ==================================================
# MAIN MENU
# ==================================================

cls

Write-Host @"

+==============================================================+
|                                                              |
|         _   _  ____  _   _  ____  ____  _____ ____           |
|        | \ | |/ __ \| \ | |/ ___||  _ \| ____|  _ \          |
|        |  \| | |  | |  \| | |  _ | |_) |  _| | | | |         |
|        | |\  | |__| | |\  | |_| ||  __/| |___| |_| |         |
|        |_| \_|\____/|_| \_|\____||_|   |_____|____/          |
|                                                              |
|                  P R E M I U M   S Y S T E M                 |
|                                                              |
+==============================================================+

 [1] KING MODE
 [2] RACHA MODE
 [3] PRO MODE
 [4] BEAST MODE
 [5] Exit

"@ -ForegroundColor Cyan

$m = Read-Host "Select"

switch ($m) {

# ==================================================
# KING MODE
# ==================================================

"1" {

    Write-Host "`n[*] APPLYING KING MODE..." -ForegroundColor Yellow

    reg add "HKCU\Control Panel\Mouse" /v MouseSpeed /t REG_SZ /d 1 /f | Out-Null

    $profiler = "$PSScriptRoot\Profiler.exe"
    $profile  = "$PSScriptRoot\Base Profile.nip"

    if (Test-Path $profiler) {

        if (Test-Path $profile) {

            Start-Process -FilePath $profiler `
                -ArgumentList "-silentImport `"$profile`"" `
                -WindowStyle Hidden `
                -Wait

            Write-Host "[+] NVIDIA PROFILE IMPORTED" -ForegroundColor Green

        } else {

            Write-Host "[x] Base Profile.nip NOT FOUND" -ForegroundColor Red
        }

    } else {

        Write-Host "[x] Profiler.exe NOT FOUND" -ForegroundColor Red
    }

    Write-Host "`n[+] KING MODE APPLIED" -ForegroundColor Green

    Start-Sleep 1
    Add-Type -AssemblyName PresentationFramework
    [System.Windows.MessageBox]::Show("KING MODE APPLIED SUCCESSFULLY","NONGPED SYSTEM")

    exit
}

# ==================================================
# RACHA MODE
# ==================================================

"2" {

    Write-Host "`n[*] APPLYING RACHA MODE..." -ForegroundColor Yellow

    reg add "HKCU\Control Panel\Keyboard" /v KeyboardSpeed /t REG_SZ /d 28 /f | Out-Null
    reg add "HKCU\Control Panel\Desktop" /v MenuShowDelay /t REG_SZ /d 0 /f | Out-Null

    $profiler = "$PSScriptRoot\Profiler.exe"
    $profile  = "$PSScriptRoot\Base Profile racha.nip"

    if (Test-Path $profiler) {

        if (Test-Path $profile) {

            Start-Process -FilePath $profiler `
                -ArgumentList "-silentImport `"$profile`"" `
                -WindowStyle Hidden `
                -Wait

            Write-Host "[+] NVIDIA PROFILE IMPORTED" -ForegroundColor Green

        } else {

            Write-Host "[x] Base Profile racha.nip NOT FOUND" -ForegroundColor Red
        }

    } else {

        Write-Host "[x] Profiler.exe NOT FOUND" -ForegroundColor Red
    }

    Write-Host "`n[+] RACHA MODE APPLIED" -ForegroundColor Green

    Start-Sleep 1
    Add-Type -AssemblyName PresentationFramework
    [System.Windows.MessageBox]::Show("RACHA MODE APPLIED SUCCESSFULLY","NONGPED SYSTEM")

    exit
}

# ==================================================
# PRO MODE
# ==================================================

"3" {

    Write-Host "`n[*] APPLYING PRO MODE..." -ForegroundColor Yellow

    reg add "HKCU\Control Panel\Keyboard" /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null
    reg add "HKCU\Control Panel\Keyboard" /v KeyboardDelay /t REG_SZ /d 0 /f | Out-Null

    $profiler = "$PSScriptRoot\Profiler.exe"
    $profile  = "$PSScriptRoot\Base Profile.nip"

    if (Test-Path $profiler) {

        if (Test-Path $profile) {

            Start-Process -FilePath $profiler `
                -ArgumentList "-silentImport `"$profile`"" `
                -WindowStyle Hidden `
                -Wait

            Write-Host "[+] NVIDIA PROFILE IMPORTED" -ForegroundColor Green

        } else {

            Write-Host "[x] Base Profile.nip NOT FOUND" -ForegroundColor Red
        }

    } else {

        Write-Host "[x] Profiler.exe NOT FOUND" -ForegroundColor Red
    }

    Write-Host "`n[+] PRO MODE APPLIED" -ForegroundColor Green

    Start-Sleep 1
    Add-Type -AssemblyName PresentationFramework
    [System.Windows.MessageBox]::Show("PRO MODE APPLIED SUCCESSFULLY","NONGPED SYSTEM")

    exit
}

# ==================================================
# BEAST MODE
# ==================================================

"4" {

    Write-Host "`n[*] LOADING BEAST MODE..." -ForegroundColor Yellow

    reg add "HKCU\Control Panel\Mouse" /v MouseSpeed /t REG_SZ /d 0 /f | Out-Null
    reg add "HKCU\Control Panel\Mouse" /v MouseThreshold1 /t REG_SZ /d 0 /f | Out-Null
    reg add "HKCU\Control Panel\Mouse" /v MouseThreshold2 /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Keyboard" /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null
    reg add "HKCU\Control Panel\Keyboard" /v KeyboardDelay /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Desktop" /v MenuShowDelay /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\System\GameConfigStore" /v GameDVR_Enabled /t REG_DWORD /d 0 /f | Out-Null

    powercfg -setactive SCHEME_MIN

    $profiler = "$PSScriptRoot\Profiler.exe"
    $profile  = "$PSScriptRoot\Base Profile racha.nip"

    if (Test-Path $profiler) {

        if (Test-Path $profile) {

            Start-Process -FilePath $profiler `
                -ArgumentList "-silentImport `"$profile`"" `
                -WindowStyle Hidden `
                -Wait

            Write-Host "[+] NVIDIA PROFILE IMPORTED" -ForegroundColor Green

        } else {

            Write-Host "[x] Base Profile racha.nip NOT FOUND" -ForegroundColor Red
        }

    } else {

        Write-Host "[x] Profiler.exe NOT FOUND" -ForegroundColor Red
    }

    Write-Host "[+] BEAST MODE APPLIED" -ForegroundColor Green

    Start-Sleep 1
    Add-Type -AssemblyName PresentationFramework
    [System.Windows.MessageBox]::Show("BEAST MODE APPLIED SUCCESSFULLY","NONGPED SYSTEM")

    exit
}

# ==================================================
# EXIT
# ==================================================

"5" {

    Write-Host "`n[!] EXITING..." -ForegroundColor Red
    Exit
}

default {

    Write-Host "`n[x] INVALID MODE" -ForegroundColor Red
}

}
