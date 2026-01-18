# **Writeup: Chinese Cipher Challenge**  
**Category**: Cryptography  
**Points**: 45  
**Solves**: 3/5.  

## Approach
Since `e` is unusually large, Wiener's attack becomes a viable method to recover the private exponent `d`. After obtaining `d`, standard RSA decryption is performed to retrieve the flag.

## Solution Code
```python
from owiener import *
from Crypto.Util.number import *

# Given RSA parameters
n = 689061037339483636851744871564868379980061151991904073814057216873412583484720768694905841053416938972235588548525570270575285633894975913717130070544407480547826227398039831409929129742007101671851757453656032161443946817685708282221883187089692065998793742064551244403369599965441075497085384181772038720949
e = 98161001623245946455371459972270637048947096740867123960987426843075734419854169415217693040603943985614577854750928453684840929755254248201161248375350238628917413291201125030514500977409961838501076015838508082749034318410808298025858181711613372870289482890074072555265382600388541381732534018133370862587

# Perform Wiener's attack to recover d
d = attack(e, n)

# Decrypt the ciphertext
ct = bytes_to_long(open("ciphertext", "rb").read())
plaintext = pow(ct, d, n)

# Print the flag
print(long_to_bytes(plaintext))
```

## Flag
The decrypted flag is:  
**INTIGRITI{0r_n07_50_53cur3_m4yb3}**

## Notes
- Wiener's attack works when the private exponent `d` is small (typically when `d < (1/3) * n^(1/4)`).
- This exploit highlights the importance of proper RSA parameter selection to avoid vulnerabilities.
