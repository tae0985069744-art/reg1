# ==================================================
#                    NONGPED
#     FINAL STABLE VERSION (FIXED + MERGED)
# ==================================================

$Host.UI.RawUI.WindowTitle = "NONGPED"

Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

# =========================
# ADMIN CHECK
# =========================
$isAdmin = ([Security.Principal.WindowsPrincipal] `
[Security.Principal.WindowsIdentity]::GetCurrent()
).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)

if (-not $isAdmin) {
    Write-Host "RUN AS ADMIN REQUIRED" -ForegroundColor Red
    Pause
    exit
}

# =========================
# UI
# =========================
function Show-UI {

    $form = New-Object System.Windows.Forms.Form
    $form.Text = "NONGPED"
    $form.Size = New-Object System.Drawing.Size(700,700)
    $form.StartPosition = "CenterScreen"
    $form.BackColor = "Black"

    $label = New-Object System.Windows.Forms.Label
    $label.Text = "🐤 NONGPED SYSTEM"
    $label.ForeColor = "White"
    $label.AutoSize = $true
    $label.Font = New-Object System.Drawing.Font("Arial",16,[System.Drawing.FontStyle]::Bold)
    $label.Location = New-Object System.Drawing.Point(230,200)

    $btn = New-Object System.Windows.Forms.Button
    $btn.Text = "ENTER"
    $btn.Size = New-Object System.Drawing.Size(200,50)
    $btn.Location = New-Object System.Drawing.Point(250,300)

    $form.Controls.Add($label)
    $form.Controls.Add($btn)

    $btn.Add_Click({ $form.Close() })

    [void]$form.ShowDialog()
}

# =========================
# LOGIN SAFE LOOP
# =========================
function Login {

    while ($true) {

        Clear-Host
        Write-Host "===== NONGPED LOGIN ====="
        $key = Read-Host "KEY"

        if ($key -eq "Nongped") {
            break
        }

        Write-Host "WRONG KEY" -ForegroundColor Red
        Start-Sleep 1
    }
}

# =========================
# SAFE REG FUNCTION
# =========================
function RegSafe($path,$name,$value) {
    try {
        reg add $path /v $name /t REG_SZ /d $value /f | Out-Null
    } catch {}
}

# =========================
# BOOST SYSTEM
# =========================
function Priority {
    RegSafe "HKCU\Control Panel\Desktop" "MenuShowDelay" "0"
}

function InputBoost {

    RegSafe "HKCU\Control Panel\Mouse" "MouseSpeed" "0"
    RegSafe "HKCU\Control Panel\Mouse" "MouseSensitivity" "10"

    RegSafe "HKCU\Control Panel\Keyboard" "KeyboardDelay" "0"
    RegSafe "HKCU\Control Panel\Keyboard" "KeyboardSpeed" "31"
}

# =========================
# GAME SUPPORT SAFE
# =========================
function GTA {
    try {
        $src = ".\gta5_settings.xml"
        $dst = "$env:USERPROFILE\Documents\Rockstar Games\GTA V\settings.xml"

        if (Test-Path $src) {
            Copy-Item $src $dst -Force
        }
    } catch {}
}

function FiveM {

    try {
        $path = "$env:LOCALAPPDATA\FiveM\FiveM.app"

        if (Test-Path $path) {
@"
[Game]
DisableLauncher=true
[Renderer]
FrameQueueLimit=1
"@ | Set-Content "$path\citizenfx.ini"
        }
    } catch {}
}

# =========================
# MENU
# =========================
function Menu {

    Clear-Host
    Write-Host "========================"
    Write-Host "        NONGPED"
    Write-Host "========================"
    Write-Host "1 KING"
    Write-Host "2 RACHA"
    Write-Host "3 PRO"
    Write-Host "4 BEAST"
    Write-Host "5 EXIT"
    Write-Host ""
}

# =========================
# APPLY ENGINE
# =========================
function ApplyBase {

    Priority
    InputBoost
    GTA
    FiveM
}

# =========================
# START
# =========================
Show-UI
Login

while ($true) {

    Menu
    $s = Read-Host "SELECT"

    switch ($s) {

        "1" {
            ApplyBase
            Write-Host "KING DONE" -ForegroundColor Green
            Pause
        }

        "2" {
            ApplyBase
            Write-Host "RACHA DONE" -ForegroundColor Yellow
            Pause
        }

        "3" {
            ApplyBase
            Write-Host "PRO DONE" -ForegroundColor Cyan
            Pause
        }

        "4" {
            ApplyBase
            Write-Host "BEAST DONE" -ForegroundColor Red
            Pause
        }

        "5" { break }
    }
}
