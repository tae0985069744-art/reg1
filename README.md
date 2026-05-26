# ==================================================
#                    NONGPED
#         FINAL OPTIMIZED VERSION
# ==================================================
# MODES:
# 1 = KING
# 2 = RACHA
# 3 = PRO
# 4 = BEAST X RP LITE
# ==================================================

$Host.UI.RawUI.WindowTitle = "NONGPED"

# ==================================================
# UI
# ==================================================

Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

function Show-UI {

    $imagePath = Join-Path $PSScriptRoot "ui.jpg"

    if (!(Test-Path $imagePath)) {

        Write-Host ""
        Write-Host "ui.jpg NOT FOUND" -ForegroundColor Red
        Pause
        return
    }

    $form = New-Object System.Windows.Forms.Form
    $form.Text = "NONGPED"
    $form.Width = 900
    $form.Height = 900
    $form.StartPosition = "CenterScreen"
    $form.BackColor = "Black"
    $form.FormBorderStyle = "FixedSingle"
    $form.MaximizeBox = $false
    $form.TopMost = $true

    $pictureBox = New-Object System.Windows.Forms.PictureBox
    $pictureBox.Dock = "Fill"
    $pictureBox.SizeMode = "StretchImage"

    try {

        $pictureBox.Image = [System.Drawing.Image]::FromFile($imagePath)
    }
    catch {

        Write-Host "FAILED TO LOAD IMAGE" -ForegroundColor Red
        Pause
        return
    }

    $form.Controls.Add($pictureBox)

    $button = New-Object System.Windows.Forms.Button
    $button.Text = "ENTER NONGPED"
    $button.Width = 240
    $button.Height = 50
    $button.BackColor = "Black"
    $button.ForeColor = "White"
    $button.FlatStyle = "Flat"

    $button.Font = New-Object System.Drawing.Font(
        "Arial",
        12,
        [System.Drawing.FontStyle]::Bold
    )

    $button.Location = New-Object System.Drawing.Point(320,780)

    $button.Add_Click({

        $form.Close()
    })

    $form.Controls.Add($button)

    [void]$form.ShowDialog()
}

# ==================================================
# LOGIN
# ==================================================

function Login {

    Clear-Host

    Write-Host ""
    Write-Host "================================="
    Write-Host "         NONGPED LOGIN"
    Write-Host "================================="
    Write-Host ""

    $key = Read-Host "ENTER KEY"

    if ($key -eq "Nongped") {

        Write-Host ""
        Write-Host "LOGIN SUCCESS" -ForegroundColor Green

        Start-Sleep 1

        return
    }
    else {

        Write-Host ""
        Write-Host "INVALID KEY" -ForegroundColor Red

        Start-Sleep 2

        Login
    }
}

# ==================================================
# APPLY SAFE
# ==================================================

function Restart-Safe {

    Write-Host ""
    Write-Host "================================="
    Write-Host " APPLY COMPLETE"
    Write-Host " NO AUTO RESTART"
    Write-Host "================================="
    Write-Host ""

    RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters
    gpupdate /force | Out-Null

    Write-Host "SETTINGS APPLIED" -ForegroundColor Green
    Write-Host ""

    Pause
}

# ==================================================
# PRIORITY
# ==================================================

function Priority {

    reg add "HKCU\Control Panel\Desktop" `
    /v MenuShowDelay /t REG_SZ /d 0 /f | Out-Null
}

# ==================================================
# INPUT BOOST
# ==================================================

function Input-Boost {

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseSpeed /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseThreshold1 /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseThreshold2 /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseSensitivity /t REG_SZ /d 10 /f | Out-Null

    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardDelay /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" `
    /v SystemResponsiveness /t REG_DWORD /d 0 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" `
    /v NetworkThrottlingIndex /t REG_DWORD /d 4294967295 /f | Out-Null

    RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters
}

# ==================================================
# MOVEMENT BOOST
# ==================================================

function Movement-Boost {

    # KEYBOARD
    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardDelay /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null

    # MOUSE
    reg add "HKCU\Control Panel\Mouse" `
    /v MouseSpeed /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseThreshold1 /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseThreshold2 /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseSensitivity /t REG_SZ /d 10 /f | Out-Null

    # LOW INPUT LAG
    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" `
    /v SystemResponsiveness /t REG_DWORD /d 0 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" `
    /v NetworkThrottlingIndex /t REG_DWORD /d 4294967295 /f | Out-Null

    # GAME PRIORITY
    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games" `
    /v "GPU Priority" /t REG_DWORD /d 8 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games" `
    /v "Priority" /t REG_DWORD /d 6 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games" `
    /v "Scheduling Category" /t REG_SZ /d High /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games" `
    /v "SFIO Priority" /t REG_SZ /d High /f | Out-Null

    # TIMER / FRAME STABILITY
    bcdedit /set useplatformtick yes | Out-Null
    bcdedit /set disabledynamictick yes | Out-Null
    bcdedit /deletevalue useplatformclock | Out-Null

    RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters
}

# ==================================================
# NVIDIA
# ==================================================

# KING

function Nvidia-King {

    .\Profiler.exe `
    -importProfile ".\Base Profile (1).nip"
}

# RACHA

function Nvidia-Racha {

    .\Profiler.exe `
    -importProfile ".\Base Profile racha.nip"
}

# PRO

function Nvidia-Pro {

    .\Profiler.exe `
    -setBaseProfile "\
    0x000000F5=0x00000001;\
    0x00000070=0x00000001;\
    0x0000005F=0x00000001;\
    0x00000028=0x00000001;\
    0x00000031=0x00000001"
}

# BEAST X RP LITE

function Nvidia-BeastLite {

    .\Profiler.exe `
    -setBaseProfile "\
    0x000000F5=0x00000001;\
    0x00000070=0x00000001;\
    0x0000005F=0x00000001;\
    0x00000028=0x00000001;\
    0x00000031=0x00000001;\
    0x00A879CF=0x00000001;\
    0x0094C537=0x00000001;\
    0x0064F7F5=0x00000001"
}

# ==================================================
# FIVEM
# ==================================================

function CitizenFX-Normal {

    $cfgPath = "$env:LOCALAPPDATA\FiveM\FiveM.app\citizenfx.ini"

@"
[Game]
DisableLauncher=true

[Renderer]
ForceRenderAheadLimit=1
FrameQueueLimit=1
EnablePresentationOptimizations=true

[Streaming]
CacheSize=2048
PhysicalMemoryLimit=4096
"@ | Set-Content $cfgPath -Force
}

function CitizenFX-Pro {

    $cfgPath = "$env:LOCALAPPDATA\FiveM\FiveM.app\citizenfx.ini"

@"
[Game]
DisableLauncher=true

[Renderer]
ForceRenderAheadLimit=1
FrameQueueLimit=1
EnablePresentationOptimizations=true
DisableLoadingScreenMouse=true

[Streaming]
CacheSize=3072
PhysicalMemoryLimit=4096
"@ | Set-Content $cfgPath -Force
}

# ==================================================
# GTA
# ==================================================

function GTA {

    Copy-Item ".\gta5_settings.xml" `
    "$env:USERPROFILE\Documents\Rockstar Games\GTA V\settings.xml" -Force
}

# ==================================================
# MENU
# ==================================================

function Menu {

    Clear-Host

    Write-Host ""
    Write-Host "================================="
    Write-Host "            NONGPED"
    Write-Host "================================="
    Write-Host ""

    Write-Host "1 = KING"
    Write-Host "2 = RACHA"
    Write-Host "3 = PRO"
    Write-Host "4 = BEAST X RP LITE"
    Write-Host "5 = EXIT"
    Write-Host ""
}

# ==================================================
# START
# ==================================================

Show-UI
Login

do {

    Menu

    $s = Read-Host "Select"

    switch ($s) {

        # ==================================================
        # KING
        # ==================================================

        "1" {

            reg import ".\Mouse king.reg" | Out-Null
            reg import ".\Keyboard king.reg" | Out-Null

            Priority
            Input-Boost

            GTA
            CitizenFX-Normal
            Nvidia-King

            Write-Host ""
            Write-Host "KING DONE" -ForegroundColor Green

            Restart-Safe
        }

        # ==================================================
        # RACHA
        # ==================================================

        "2" {

            reg import ".\Mouse racha.reg" | Out-Null
            reg import ".\Keyboard racha.reg" | Out-Null

            Priority
            Input-Boost

            GTA
            CitizenFX-Normal
            Nvidia-Racha

            Write-Host ""
            Write-Host "RACHA DONE" -ForegroundColor Yellow

            Restart-Safe
        }

        # ==================================================
        # PRO
        # ==================================================

        "3" {

            reg import ".\Mouse racha.reg" | Out-Null
            reg import ".\Keyboard racha.reg" | Out-Null

            Priority
            Input-Boost
            Movement-Boost

            GTA
            CitizenFX-Pro
            Nvidia-Pro

            Write-Host ""
            Write-Host "PRO DONE" -ForegroundColor Cyan

            Restart-Safe
        }

        # ==================================================
        # BEAST X RP LITE
        # ==================================================

        "4" {

            reg import ".\Mouse racha.reg" | Out-Null
            reg import ".\Keyboard racha.reg" | Out-Null

            Priority
            Input-Boost
            Movement-Boost

            GTA
            CitizenFX-Pro
            Nvidia-BeastLite

            Write-Host ""
            Write-Host "BEAST X RP LITE DONE" -ForegroundColor Red

            Restart-Safe
        }

        # ==================================================
        # EXIT
        # ==================================================

        "5" {

            break
        }
    }

} while ($true)
