## Fuzzing vs. Brute-forcing
#### Fuzzing
- Fuzzingde girdi olarak:
	- Unexpected inputs 
	- Malformed data
	- Invalid Characters
	- Nonsensical Combinations(saçma kombinasyonlar)
- Amaç applicationun nasıl çalıştığını naısl tepkiler verdiğini incelemek
#### Brute-Forcing
- Brute force daha target yönelik yaklaşımı vardır.

bir analogy :
 Fuzzing would be like throwing everything you can find at the door - keys, screwdrivers, even a rubber duck - to see if anything unlocks it. Brute-forcing would be like trying every combination on a key ring until you find the one that opens the door.

# Fuzzing

Gizli Güvenlik Açıklarını Ortaya Çıkarma: fuzzing, kodda gizli kusurları ortaya çıkaran beklenmedik davranışları tetikleyebilir.

Wordlist : https://github.com/danielmiessler/SecLists
The most commonly used wordlists for fuzzing web directories and files from `SecLists` are:
- `Discovery/Web-Content/common.txt`:
- `Discovery/Web-Content/directory-list-2.3-medium.txt`:
- `Discovery/Web-Content/raft-large-directories.txt`: 
- `Discovery/Web-Content/big.txt`: directory and file names