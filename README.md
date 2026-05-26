# ==================================================
#                 NONGPED SYSTEM (CLI VERSION)
# ==================================================

# 1. ตั้งชื่อหน้าต่าง
$Host.UI.RawUI.WindowTitle="NONGPED SYSTEM"

# 2. ล็อกสีพื้นหลังให้เป็นสีดำ และสีตัวหนังสือเริ่มต้นเป็นสีขาว
[console]::BackgroundColor = "Black"
[console]::ForegroundColor = "White"
cls

# ==================================================
# LOGIN SYSTEM
# ==================================================
Write-Host "+==============================================================+" -ForegroundColor Cyan
Write-Host "|                                                              |" -ForegroundColor Cyan
Write-Host "|                  P R E M I U M   S Y S T E M                 |" -ForegroundColor Gray
Write-Host "|                                                              |" -ForegroundColor Cyan
Write-Host "+==============================================================+" -ForegroundColor Cyan
Write-Host ""

# รับค่ารหัสผ่าน
$key = Read-Host "A C C E S S   K E Y"

# เช็ครหัสผ่าน
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

# เริ่มทำงานตามโหมดที่เลือก
switch ($m) {
    "1" {
        reg add "HKCU\Control Panel\Mouse" /v MouseSpeed /t REG_SZ /d 1 /f | Out-Null
        Write-Host "`n[+] KING MODE APPLIED" -ForegroundColor Green
    }
    "2" {
        reg add "HKCU\Control Panel\Keyboard" /v KeyboardSpeed /t REG_SZ /d 28 /f | Out-Null
        reg add "HKCU\Control Panel\Desktop" /v MenuShowDelay /t REG_SZ /d 0 /f | Out-Null
        Write-Host "`n[+] RACHA MODE APPLIED" -ForegroundColor Green
    }
    "3" {
        reg add "HKCU\Control Panel\Keyboard" /v KeyboardSpeed /t REG_SZ /d 31 /f | Out-Null
        reg add "HKCU\Control Panel\Keyboard" /v KeyboardDelay /t REG_SZ /d 0 /f | Out-Null
        Write-Host "`n[+] PRO MODE APPLIED" -ForegroundColor Green
    }
    "4" {
        Write-Host "`n[*] LOADING BEAST MODE..." -ForegroundColor Yellow
        Start-Process powershell -WindowStyle Hidden -ArgumentList @"
reg add `"HKCU\Control Panel\Mouse`" /v MouseSpeed /t REG_SZ /d 0 /f
reg add `"HKCU\Control Panel\Mouse`" /v MouseThreshold1 /t REG_SZ /d 0 /f
reg add `"HKCU\Control Panel\Mouse`" /v MouseThreshold2 /t REG_SZ /d 0 /f
reg add `"HKCU\Control Panel\Keyboard`" /v KeyboardSpeed /t REG_SZ /d 31 /f
reg add `"HKCU\Control Panel\Keyboard`" /v KeyboardDelay /t REG_SZ /d 0 /f
reg add `"HKCU\Control Panel\Desktop`" /v MenuShowDelay /t REG_SZ /d 0 /f
reg add `"HKCU\System\GameConfigStore`" /v GameDVR_Enabled /t REG_DWORD /d 0 /f
powercfg -setactive SCHEME_MIN
exit
"@
        Start-Sleep -Milliseconds 700
        Write-Host "[+] BEAST MODE APPLIED" -ForegroundColor Green
    }
    "5" {
        Write-Host "`n[!] Exiting..." -ForegroundColor Red
        Exit
    }
    default {
        Write-Host "`n[x] INVALID MODE" -ForegroundColor Red
    }
}

# หยุดหน้าจอให้ผู้ใช้เห็นผลลัพธ์ก่อนปิด
Write-Host "`nPress any key to continue..." -ForegroundColor Gray
$null = $Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
