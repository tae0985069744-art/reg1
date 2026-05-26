# ==================================================
#                     NONGPED
#                SAFE FINAL VERSION
# ==================================================

# SAFE:
# - ไม่แตะ Network Adapter
# - ไม่ปิด Service สำคัญ
# - ไม่แก้ TCP/IP
# - ไม่ใช้ค่า BCD อันตราย
# - ลดเสี่ยงเน็ตดับ / วินโดว์พัง

$Host.UI.RawUI.WindowTitle = "NONGPED"

# ==================================================
# UI IMAGE
# ==================================================

Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

function Show-UI {

    $form = New-Object System.Windows.Forms.Form
    $form.Text = "NONGPED"
    $form.Width = 900
    $form.Height = 900
    $form.StartPosition = "CenterScreen"
    $form.BackColor = "Black"

    # ==================================================
    # IMAGE
    # ==================================================

    $pictureBox = New-Object System.Windows.Forms.PictureBox
    $pictureBox.Width = 860
    $pictureBox.Height = 820
    $pictureBox.Location = New-Object System.Drawing.Point(10,10)
    $pictureBox.SizeMode = "StretchImage"

    # ใส่รูป
    $pictureBox.Image = [System.Drawing.Image]::FromFile(".\ui.jpg")

    $form.Controls.Add($pictureBox)

    # ==================================================
    # BUTTON
    # ==================================================

    $button = New-Object System.Windows.Forms.Button
    $button.Text = "ENTER NONGPED"
    $button.Width = 200
    $button.Height = 40
    $button.Location = New-Object System.Drawing.Point(330,780)

    $button.Add_Click({

        $form.Close()
    })

    $form.Controls.Add($button)

    $form.Topmost = $true

    [void]$form.ShowDialog()
}

# ==================================================
# SHOW UI
# ==================================================

Show-UI

# ==================================================
# LOGIN
# ==================================================

function Login {

    Clear-Host

    Write-Host "=== NONGPED LOGIN ==="

    $key = Read-Host "Enter Key"

    if ($key -ne "Nongped") {

        Write-Host ""
        Write-Host "INVALID KEY" -ForegroundColor Red

        Start-Sleep 2

        Login
    }
}

# ==================================================
# SAFE PRIORITY
# ==================================================

function Priority {

    reg add "HKCU\Control Panel\Desktop" `
    /v MenuShowDelay /t REG_SZ /d 0 /f | Out-Null
}

# ==================================================
# SAFE INPUT BOOST
# ==================================================

function Input-Boost {

    Write-Host ""
    Write-Host "[ SAFE INPUT BOOST ]"

    # ==================================================
    # MOUSE
    # ==================================================

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseSpeed /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseThreshold1 /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseThreshold2 /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Mouse" `
    /v MouseSensitivity /t REG_SZ /d 10 /f | Out-Null

    # ==================================================
    # KEYBOARD
    # ==================================================

    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardDelay /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null

    # ==================================================
    # SAFE SYSTEM RESPONSIVENESS
    # ==================================================

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" `
    /v SystemResponsiveness /t REG_DWORD /d 10 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" `
    /v NetworkThrottlingIndex /t REG_DWORD /d 10 /f | Out-Null

    # ==================================================
    # GAME PRIORITY
    # ==================================================

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games" `
    /v "GPU Priority" /t REG_DWORD /d 8 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games" `
    /v "Priority" /t REG_DWORD /d 6 /f | Out-Null

    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games" `
    /v "Scheduling Category" /t REG_SZ /d High /f | Out-Null
}

# ==================================================
# SAFE MOVEMENT BOOST
# ==================================================

function Movement-Boost {

    Write-Host ""
    Write-Host "[ SAFE MOVEMENT BOOST ]"

    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardDelay /t REG_SZ /d 0 /f | Out-Null

    reg add "HKCU\Control Panel\Keyboard" `
    /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null
}

# ==================================================
# NVIDIA KING
# ==================================================

function Nvidia-King {

    Write-Host ""
    Write-Host "[ NVIDIA KING ]"

    .\Profiler.exe `
    -setBaseProfile "\
    0x000000F5=0x00000001;\
    0x00000028=0x00000001;\
    0x00000070=0x00000001;\
    0x000000A9=0x00000000"
}

# ==================================================
# NVIDIA RACHA
# ==================================================

function Nvidia-Racha {

    Write-Host ""
    Write-Host "[ NVIDIA RACHA ]"

    .\Profiler.exe `
    -importProfile ".\Base Profile racha.nip"
}

# ==================================================
# NVIDIA PRO
# ==================================================

function Nvidia-Pro {

    Write-Host ""
    Write-Host "[ NVIDIA PRO SAFE ]"

    .\Profiler.exe `
    -setBaseProfile "\
    0x000000F5=0x00000001;\
    0x000000A9=0x00000000;\
    0x00000070=0x00000001;\
    0x0000005F=0x00000001;\
    0x00000031=0x00000001"
}

# ==================================================
# FIVEM NORMAL
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

# ==================================================
# FIVEM PRO
# ==================================================

function CitizenFX-Pro {

    $cfgPath = "$env:LOCALAPPDATA\FiveM\FiveM.app\citizenfx.ini"

@"
[Game]
DisableLauncher=true

[Renderer]
ForceRenderAheadLimit=1
FrameQueueLimit=1
EnablePresentationOptimizations=true

[Streaming]
CacheSize=3072
PhysicalMemoryLimit=4096
"@ | Set-Content $cfgPath -Force
}

# ==================================================
# GTA SETTINGS
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

    Write-Host "================================="
    Write-Host "        NONGPED SAFE"
    Write-Host "================================="
    Write-Host ""

    Write-Host "1 = KING"
    Write-Host "2 = RACHA"
    Write-Host "3 = PRO"
    Write-Host "4 = EXIT"

    Write-Host ""
}

# ==================================================
# START
# ==================================================

Login

do {

    Menu

    $s = Read-Host "Select"

    switch ($s) {

        # ==================================================
        # KING
        # ==================================================

        "1" {

            Write-Host ""
            Write-Host "[ APPLYING KING ]" -ForegroundColor Cyan

            reg import ".\Mouse king.reg" | Out-Null
            reg import ".\Keyboard king.reg" | Out-Null

            Priority
            Input-Boost

            GTA
            CitizenFX-Normal

            Nvidia-King

            Write-Host ""
            Write-Host "KING DONE" -ForegroundColor Green
            Write-Host ""
            Write-Host "SAFE + LIGHT"
            Write-Host "GOOD FPS"
            Write-Host "LOW INPUT LAG"

            Pause
        }

        # ==================================================
        # RACHA
        # ==================================================

        "2" {

            Write-Host ""
            Write-Host "[ APPLYING RACHA ]" -ForegroundColor Yellow

            reg import ".\Mouse racha.reg" | Out-Null
            reg import ".\Keyboard racha.reg" | Out-Null

            Priority
            Input-Boost

            GTA
            CitizenFX-Normal

            Nvidia-Racha

            Write-Host ""
            Write-Host "RACHA DONE" -ForegroundColor Yellow
            Write-Host ""
            Write-Host "BEST BALANCE"
            Write-Host "SMOOTH RP"
            Write-Host "GOOD LATENCY"

            Pause
        }

        # ==================================================
        # PRO
        # ==================================================

        "3" {

            Write-Host ""
            Write-Host "[ APPLYING PRO ]" -ForegroundColor Magenta

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
            Write-Host ""
            Write-Host "LOW INPUT LAG"
            Write-Host "SMOOTH MOVEMENT"
            Write-Host "RESPONSIVE MOUSE"
            Write-Host "FAST KEYBOARD"
            Write-Host "SAFE WINDOWS"

            Start-Sleep 3

            Restart-Computer -Force
        }

        # ==================================================
        # EXIT
        # ==================================================

        "4" {

            break
        }
    }

} while ($true)
