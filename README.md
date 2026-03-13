# 🛡️ Network Security — TryHackMe Writeups

> Kumpulan writeup pengerjaan room TryHackMe untuk mata kuliah Keamanan Jaringan.  
> **Author:** Bizar Octo Givardi

---

## 📁 Struktur Repository

```
├── task-7-ad-basic-enumeration/
│   └── writeup_AD_BasicEnumeration_FULL.pdf
└── task-8-attacktive-directory/
    └── writeup_Attacktive_Directory.pdf
```

---

## 📋 Daftar Task

| Task | Pertemuan | Judul | Room | Difficulty | Status |
|------|-----------|-------|------|------------|--------|
| 7 | Pertemuan 7 | AD: Basic Enumeration | [adbasicenumeration](https://tryhackme.com/room/adbasicenumeration) | 🟢 Easy | ✅ Done |
| 8 | Pertemuan 8 | AD: Initial Access, Post-Exploitation & Lateral Movement | [attacktivedirectory](https://tryhackme.com/room/attacktivedirectory) | 🟡 Medium | ✅ Done |

---

## 📝 Task 7 — AD: Basic Enumeration

**Room:** https://tryhackme.com/room/adbasicenumeration  
**Difficulty:** Easy | **Estimated Time:** 60 menit

### Topik yang Dipelajari
- Network mapping dan host discovery dengan Nmap
- Enumerasi SMB shares secara anonim
- Domain enumeration via LDAP, RPC, dan enum4linux
- Password spraying dengan CrackMapExec

### Tools yang Digunakan
`nmap` `smbclient` `smbmap` `ldapsearch` `rpcclient` `enum4linux` `crackmapexec`

### Alur Serangan
```
Host Discovery (Nmap)
      ↓
Port Scan → Identifikasi Domain Controller (tryhackme.loc)
      ↓
SMB Enumeration → Flag ditemukan di share UserBackups
      ↓
LDAP + enum4linux → Daftar user domain
      ↓
Password Spraying (CrackMapExec) → Kredensial valid: rduke:Password1!
```

### Writeup
📄 [Lihat Writeup (PDF)](./task-7-ad-basic-enumeration/WriteUP_AD_Enum_Bizar.pdf)

---

## 📝 Task 8 — Attacktive Directory

**Room:** https://tryhackme.com/room/attacktivedirectory  
**Difficulty:** Medium | **Estimated Time:** 75 menit

### Topik yang Dipelajari
- Enumerasi user domain via Kerbrute
- ASREPRoasting untuk mendapatkan Kerberos hash
- Hash cracking dengan Hashcat
- SMB enumeration dengan kredensial
- DCSync Attack dengan Impacket secretsdump
- Pass-the-Hash dengan Evil-WinRM

### Tools yang Digunakan
`nmap` `kerbrute` `impacket` `hashcat` `smbclient` `evil-winrm`

### Alur Serangan
```
Nmap Scan → Identifikasi layanan AD (spookysec.local)
      ↓
Kerbrute → Enumerasi username valid (svc-admin, backup)
      ↓
ASREPRoasting (GetNPUsers) → Hash Kerberos svc-admin
      ↓
Hashcat (mode 18200) → Password: management2005
      ↓
SMB Enumeration → backup_credentials.txt → backup:backup2517860
      ↓
DCSync Attack (secretsdump) → NTLM hash seluruh domain
      ↓
Pass-the-Hash (Evil-WinRM) → Akses penuh sebagai Administrator
```

### Flag yang Ditemukan
| User | Flag |
|------|------|
| svc-admin | `TryHackMe{K3rb3r0s_Pr3_4uth}` |
| backup | `TryHackMe{B4ckM3UpSc0tty!}` |
| Administrator | `TryHackMe{4ctiveD1rectoryM4st3r}` |

### Writeup
📄 [Lihat Writeup (PDF)](./task-8-attacktive-directory/writeup_Attacktive_Directory_Task8_Bizar.pdf)

---

## 🔧 Environment

| Komponen | Detail |
|----------|--------|
| Platform | TryHackMe VPN |
| OS Attacker | Kali Linux |
| Target Task 7 | 10.211.11.0/24 — domain: tryhackme.loc |
| Target Task 8 | 10.48.165.31 — domain: spookysec.local |

---

<div align="center">
  <sub>Made with ☕ by Bizar Octo Givardi</sub>
</div>
