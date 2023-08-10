import random, math


# MRT is Miller-Rabin Primality Test, returns true if input value is prime, false if composite
def MRT(input_value):
    if input_value % 2 == 0 or input_value < 2: # Checks to see if input value is even, if so returns false
        return False 

    n = input_value - 1 # To find n-1 = 2^k * m      n is input_value-1 in this case
    k = 0
    while n % 2 == 0:
        # Keep dividing n by two until it is odd (i.e until we get a non int number) (and use k
        # to determine the value of the exponent)
        n = n // 2
        k += 1
        print(k)

    for tests in range(10): # Test to see if number is prime 10 times.
        a = random.randrange(2, input_value - 1)  # generate a random number "a" in range 2 < a < n-1
        v = pow(a, n, input_value) # a^input_value - 1 mod input_value , fermat's little theorem
        if v != 1: # If v == 1 then the number is prime
            i = 0
            while v != (input_value - 1):
                if i == k - 1:
                    return False
                else:
                    i = i + 1
                    v = (v ** 2) % input_value
    return True

         

def EA(x, y):
 # Return the GCD of a and b using Euclid's algorithm:
 while x != 0:
    x, y = y % x, x # assigns value of y mod x to x and a value of x to y
 return y
    



def EEA(x1, y1):
    r_last, r = abs(x1), abs(y1) # abs function converts negative numbers to positive, input validation
    x, lastx, y, lasty = 0, 1, 1, 0
    while r:
        r_last, (quotient, r) = r, divmod(r_last, r) # divmod function returns quotient and remainder
        x, lastx = lastx - quotient*x, x
        y, lasty = lasty - quotient*y, y

    g = r_last
    x = lastx * (-1 if x1 < 0 else 1)
    y = lasty * (-1 if y1 < 0 else 1)
    if g != 1:
	    print ("GCD not 1")
    return x % y1





def powmod_sm(a, b, p) :
    result = 1     

    # Update a if a >= p
    
    a = a % p
     
    if (a == 0) :
        return 0
 
    while (b > 0) :
         
        # If b is odd, multiply
        # x with result
        if ((b & 1) == 1) : # bitwise & operator
            result = (result * a) % p
 
        # b must be even now
        b = b >> 1      # b = b/2 , bitshift right by 1 divides number by two
        a = (a * a) % p
         
    return result



def RandomNumberGenerator(keysize):
    # Return a random number that is keysize bits in size:
    while True:
        value = random.randrange(2**(keysize-1), 2**(keysize))
        return value





# RSA Key Generation
 
def main():

    keysize = 512
    p = RandomNumberGenerator(keysize)
    q = RandomNumberGenerator(keysize)

    # if generated numbers are not prime, keep generating until prime numbers are found

    while MRT(p) != True:
        p = RandomNumberGenerator(keysize)
        
    while MRT(q) != True:
        q = RandomNumberGenerator(keysize)

    print ("Value of prime number p is: ", p, "\n")
    print ("Value of prime number q is: ", q, "\n")

    n = p * q
    print("Value of n is: ", n, "\n")

    phi = (p-1) * (q-1)

    print("Value of phi is: ", phi, "\n")

    # choose a random public exponent e from the range of 1 to phi -1 

    e = random.randrange(1, phi - 1)

    gcd_value = EA(e,phi)

    while gcd_value != 1:   # Keep choosing a new e until GCD is 1     
        e = random.randrange(1, phi - 1)
        # program might take a while to calculate this value
        # if taking too long to calculate, restart program 


    print("Value of e is: ", e, "\n")

    gcd_of_phi_n = EA(e, phi)

    print("GCD of phi and n is: ", gcd_of_phi_n, "\n")

    # calculate private exponent d by calculating modular inverse of e and phi (e^-1 mod phi )
    #d = modinv (e,phi)
    d = EEA (e,phi)
    
   
    print("Decryption exponent d is: ", d, "\n")


    print("The public key (n,e) is: ","(" ,n ,",", e, ")","\n")
    print("The private key d is ", d,"\n")


    print("------------------------------------------", "\n")


    print("RSA Encryption with input:", "\n")
    
    # pick a random number from 1 to 26
    plaintext_x = random.randrange(1,26)
    print("The random plaintext is: ", plaintext_x, "\n")

    # raise plaintext to public exponent e and mod n    (plaintext^e mod n)
    # encrypted plaintext results in cipher text
    cipher_text = powmod_sm(plaintext_x,e,n)

    print("Resulting ciphertext is:", cipher_text, "\n")


    print("------------------------------------------", "\n")


    print("RSA Decryption with input:", "\n")

    # raise ciphertext to private exponent d and mod n   (ciphertext^d mod n)
    # decrypted ciphertext results in original plaintext
    decrypted_txt = powmod_sm(cipher_text,d,n)
    print("Decrypted ciphertext is", decrypted_txt, "\n")

    print("------------------------------------------", "\n")

main()
