Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

# =========================
# FORM
# =========================
$form = New-Object Windows.Forms.Form
$form.Text = "INSIDEX TOOLBOX V5 - ULTRA CLEAN UI"
$form.Size = New-Object Drawing.Size(700,500)
$form.StartPosition = "CenterScreen"
$form.BackColor = [System.Drawing.Color]::FromArgb(18,18,18)
$form.FormBorderStyle = "FixedSingle"
$form.MaximizeBox = $false

# =========================
# HEADER
# =========================
$header = New-Object Windows.Forms.Label
$header.Text = "INSIDEX TOOLBOX V5"
$header.Font = New-Object Drawing.Font("Segoe UI",16,[Drawing.FontStyle]::Bold)
$header.ForeColor = [System.Drawing.Color]::Cyan
$header.AutoSize = $true
$header.Location = New-Object Drawing.Point(20,15)
$form.Controls.Add($header)

# =========================
# STATUS CARD (TOP)
# =========================
$statusBox = New-Object Windows.Forms.TextBox
$statusBox.Multiline = $true
$statusBox.ReadOnly = $true
$statusBox.Size = New-Object Drawing.Size(650,80)
$statusBox.Location = New-Object Drawing.Point(20,55)
$statusBox.BackColor = [System.Drawing.Color]::FromArgb(30,30,30)
$statusBox.ForeColor = [System.Drawing.Color]::Lime
$statusBox.Font = New-Object Drawing.Font("Consolas",9)
$statusBox.Text = "STATUS: READY"
$form.Controls.Add($statusBox)

# =========================
# LEFT PANEL (OPTIONS)
# =========================
$leftPanel = New-Object Windows.Forms.Panel
$leftPanel.Size = New-Object Drawing.Size(320,250)
$leftPanel.Location = New-Object Drawing.Point(20,150)
$leftPanel.BackColor = [System.Drawing.Color]::FromArgb(30,30,30)
$form.Controls.Add($leftPanel)

$optTitle = New-Object Windows.Forms.Label
$optTitle.Text = "OPTIMIZATION OPTIONS"
$optTitle.ForeColor = [System.Drawing.Color]::White
$optTitle.Font = New-Object Drawing.Font("Segoe UI",10,[Drawing.FontStyle]::Bold)
$optTitle.Location = New-Object Drawing.Point(10,10)
$optTitle.AutoSize = $true
$leftPanel.Controls.Add($optTitle)

$ultraBox = New-Object Windows.Forms.CheckBox
$ultraBox.Text = "MODE 5 ULTRA BOOST"
$ultraBox.ForeColor = "White"
$ultraBox.Location = New-Object Drawing.Point(15,50)
$leftPanel.Controls.Add($ultraBox)

$cleanBox = New-Object Windows.Forms.CheckBox
$cleanBox.Text = "CLEAN JUNK FILES"
$cleanBox.ForeColor = "White"
$cleanBox.Location = New-Object Drawing.Point(15,85)
$leftPanel.Controls.Add($cleanBox)

# =========================
# RIGHT PANEL (SYSTEM INFO)
# =========================
$rightPanel = New-Object Windows.Forms.Panel
$rightPanel.Size = New-Object Drawing.Size(310,250)
$rightPanel.Location = New-Object Drawing.Point(360,150)
$rightPanel.BackColor = [System.Drawing.Color]::FromArgb(30,30,30)
$form.Controls.Add($rightPanel)

$sysTitle = New-Object Windows.Forms.Label
$sysTitle.Text = "SYSTEM INFO"
$sysTitle.ForeColor = [System.Drawing.Color]::White
$sysTitle.Font = New-Object Drawing.Font("Segoe UI",10,[Drawing.FontStyle]::Bold)
$sysTitle.Location = New-Object Drawing.Point(10,10)
$sysTitle.AutoSize = $true
$rightPanel.Controls.Add($sysTitle)

$diskLabel = New-Object Windows.Forms.Label
$diskLabel.ForeColor = [System.Drawing.Color]::Lime
$diskLabel.Font = New-Object Drawing.Font("Consolas",10)
$diskLabel.Location = New-Object Drawing.Point(10,50)
$diskLabel.Size = New-Object Drawing.Size(280,100)
$rightPanel.Controls.Add($diskLabel)

function Get-FreeSpace {
    $drive = Get-PSDrive C
    return [math]::Round($drive.Free / 1GB, 2)
}

function Update-Disk {
    $diskLabel.Text = "C Drive Free:`n$(Get-FreeSpace) GB"
}

# =========================
# BUTTON (BOTTOM)
# =========================
$btn = New-Object Windows.Forms.Button
$btn.Text = "APPLY OPTIMIZATION"
$btn.Size = New-Object Drawing.Size(650,40)
$btn.Location = New-Object Drawing.Point(20,420)
$btn.BackColor = [System.Drawing.Color]::FromArgb(0,120,215)
$btn.ForeColor = "White"
$btn.FlatStyle = "Flat"
$btn.Font = New-Object Drawing.Font("Segoe UI",10,[Drawing.FontStyle]::Bold)
$form.Controls.Add($btn)

# =========================
# FUNCTIONS (UNCHANGED LOGIC)
# =========================
function ULTRA {
    reg add "HKCU\Control Panel\Desktop" /v MenuShowDelay /t REG_SZ /d 0 /f | Out-Null
    reg add "HKCU\Control Panel\Mouse" /v MouseSpeed /t REG_SZ /d 0 /f | Out-Null
    reg add "HKCU\Control Panel\Keyboard" /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null
    reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile" `
    /v SystemResponsiveness /t REG_DWORD /d 10 /f | Out-Null
    powercfg -setactive SCHEME_MIN | Out-Null
    ipconfig /flushdns | Out-Null
}

function CLEAN {
    $before = Get-FreeSpace
    Remove-Item "$env:TEMP\*" -Recurse -Force -ErrorAction SilentlyContinue
    Remove-Item "$env:WINDIR\Temp\*" -Recurse -Force -ErrorAction SilentlyContinue
    try { Clear-RecycleBin -Force -ErrorAction SilentlyContinue } catch {}
    $after = Get-FreeSpace
    $saved = [math]::Round($after - $before, 2)
    return @{saved=$saved}
}

# =========================
# CLICK EVENT
# =========================
$btn.Add_Click({

    $statusBox.Text = "RUNNING..."

    Update-Disk

    if ($ultraBox.Checked) {
        ULTRA
        $statusBox.AppendText("`r`n✔ ULTRA MODE DONE")
    }

    if ($cleanBox.Checked) {
        $r = CLEAN
        $statusBox.AppendText("`r`n✔ CLEAN DONE")
        $statusBox.AppendText("`r`n✔ FREED: $($r.saved) GB")
    }

    Update-Disk

    $statusBox.AppendText("`r`n------------------")
    $statusBox.AppendText("`r`nDONE")
})

# =========================
# TIMER
# =========================
$timer = New-Object Windows.Forms.Timer
$timer.Interval = 1000
$timer.Add_Tick({ Update-Disk })
$timer.Start()

Update-Disk
[void]$form.ShowDialog()
