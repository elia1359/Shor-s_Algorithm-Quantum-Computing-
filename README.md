# Shor's_Algorithm (Quantum-Computing)


from Crypto.Util.number import inverse, GCD
from qiskit_algorithms.factoring.shor import Shor
from qiskit.utils import QuantumInstance
from qiskit import Aer

# RSA setup with small primes
p = 11
q = 13
n = p * q             # 143
phi = (p - 1)*(q - 1)

e = 7
assert GCD(e, phi) == 1
d = inverse(e, phi)

# Encrypt a message
m = 42
c = pow(m, e, n)

print("🔐 Public key (n, e):", (n, e))
print("📤 Encrypted message:", c)
print("📥 Decrypted message:", pow(c, d, n))

# Break n using Shor's Algorithm
print("\n⚡ Factoring n =", n, "using Shor's Algorithm:")
shor = Shor()
backend = Aer.get_backend("aer_simulator")
qi = QuantumInstance(backend, shots=1024)
result = shor.factor(N=n, quantum_instance=qi)
print("💥 Factors:", result.factors)

# Verify the factors


