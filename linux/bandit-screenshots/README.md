# OverTheWire: Bandit Completion Evidence

This directory contains visual proof and command execution logs for completing levels 0 through 20 of the [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) wargame.

Each screenshot captures the terminal state showing:
* The active SSH user and target host session.
* The exact command pipelines executed to solve the challenge.
* The successfully extracted password or retrieved authorization token for the subsequent level.

---

## Naming Convention

All screenshots follow the naming schema:

`bandit[number].png`

* **Example:** `bandit8.png` corresponds to solving Level 8 and extracting the password for Level 9.

---

## Evidence Index

| Screenshot | Challenge Focus | Key Utilities Demonstrated |
| :--- | :--- | :--- |
| `bandit0.png` | Standard I/O & SSH connection | `cat`, `ssh -p` |
| `bandit1.png` | Dash filenames & argument parsing | `cat ./-` |
| `bandit2.png` | Whitespace & special character escaping | Escaped quotes, `\` |
| `bandit3.png` | Hidden file discovery | `ls -la` |
| `bandit4.png` | Human-readable content discovery | `file ./*` |
| `bandit5.png` | Granular file property filtering | `find`, `-size`, `! -executable` |
| `bandit6.png` | System-wide search & error stream suppression | `find /`, `2>/dev/null`, `-user`, `-group` |
| `bandit7.png` | Pattern matching | `grep` |
| `bandit8.png` | Sorting & isolating non-duplicated lines | `sort`, `uniq -u`, Pipes (`\|`) |
| `bandit9.png` | Binary string extraction | `strings`, `grep` |
| `bandit10.png` | Base64 decoding | `base64 -d` |
| `bandit11.png` | Caesar/ROT13 cipher translation | `tr 'A-Za-z' 'N-ZA-Mn-za-m'` |
| `bandit12.png` | Reversing hexdumps & recursive decompression | `xxd -r`, `gzip`, `bzip2`, `tar` |
| `bandit13.png` | Key-based SSH authentication | `ssh -i` |
| `bandit14.png` | Raw network socket communication | `nc` (Netcat) |
| `bandit15.png` | SSL/TLS encrypted network communication | `openssl s_client` |
| `bandit16.png` | Port scanning & RSA key extraction | `nmap`, `chmod 600` |
| `bandit17.png` | Line-by-line file comparison | `diff` |
| `bandit18.png` | Shell rc bypass via non-interactive commands | Remote execution (`ssh <cmd>`) |
| `bandit19.png` | Privilege elevation via SUID binaries | `./bandit20-do`, file permissions |

---

*For detailed explanations, command breakdowns, and key takeaways for each challenge, refer to `bandit-writeups.md`.*
