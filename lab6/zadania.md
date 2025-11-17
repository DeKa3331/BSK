tworzenie klucza:

deka@SKH-KUBUNTU:~$ gpg --full-generate-key
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 1024
Requested keysize is 1024 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: jakub
Email address: jakub@test.pl
Comment: none
You selected this USER-ID:
    "jakub (none) <jakub@test.pl>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: /home/deka/.gnupg/trustdb.gpg: trustdb created
gpg: directory '/home/deka/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/deka/.gnupg/openpgp-revocs.d/C1993C8FFA793A91B21B5B36067FBC2603B2D56B.rev'
public and secret key created and signed.

pub   rsa1024 2025-11-17 [SC]
      C1993C8FFA793A91B21B5B36067FBC2603B2D56B
uid                      jakub (none) <jakub@test.pl>
sub   rsa1024 2025-11-17 [E]


hasla mozna nie wpisywac zadziala

zeby wyswietlic:
deka@SKH-KUBUNTU:~$ gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
/home/deka/.gnupg/pubring.kbx
-----------------------------
pub   rsa1024 2025-11-17 [SC]
      C1993C8FFA793A91B21B5B36067FBC2603B2D56B
uid           [ultimate] jakub (none) <jakub@test.pl>
sub   rsa1024 2025-11-17 [E]



gpg --armor --export jakub@test.pl >pub key



deka@SKH-KUBUNTU:~$ gpg --armor --export-secret-key jakub@test.pl >pub key
deka@SKH-KUBUNTU:~$ cat key
1fbcf99a5131a6a0094c2a40a1a0b8dddeka@SKH-KUBUNTU:~$ cat pub key
-----BEGIN PGP PRIVATE KEY BLOCK-----

lQHYBGka6zkBBADIyhgF45BZVPwyrN2SkEEHArxJsMzCB2u8jJRKaxme9XW6EDX5
ahq0tXaO2dVMD1GRhNCMwFNEAxCV0aduRnRqPyzwWMl1gOiTe5iyUDF3MDmlHptq
BEEwpVbRqKHvHu4NVE1tF/sJEFYt8mDB0zuCfvBIaXvP9AyjOhpQw1D2TwARAQAB
AAP/Y+sVu1B8E8hT3E/jzzyT744v7qfZrTCOL3zxinrzfAQAOsA4a86eTZED16CV
IU16NOUX9wL6LJ0t0rBLFnhfE2JUcOs4B1KLd4EK8vUF5oOAYy5JYZ8RPRW0DGe1
V+X+L+/04Ux1PAKlKT7sVhUw+esgS/0d2t5FXchpgWq6o+kCANlBJUSNiEqgqSja
4e2CguCIKt9EozqTI+RFCechIIjclWGYwdpge5aM9GA7RjJlwIfvOLVyxKUzpmeP
lRPMEiUCAOyZOpn192l8V7YvU9ftNqEyXvbz/1tIpahXkgz0ra+OKRTqdd5ME4JV
O1QbMSeY0/aYImndiqjPdSy5XH3GimMCAJOIHfkciCJZCxzhaHkMermGe4kKaMTv
lb2v90sqd7XXr/VS33qeGG4HPdUAfbM5sYB2se0lX9ctaONfM4+246ugybQcamFr
dWIgKG5vbmUpIDxqYWt1YkB0ZXN0LnBsPojOBBMBCgA4FiEEwZk8j/p5OpGyG1s2
Bn+8JgOy1WsFAmka6zkCGwMFCwkIBwIGFQoJCAsCBBYCAwECHgECF4AACgkQBn+8
JgOy1WvnPgQAsiB9iqnqD1jBW/A86LrGpMLhL34iLWma+9e8julL1cEOC3JZGihG
9R4rYNGuDZ7/+5riicUH0upO4RE/H3mXQGuUUGR1Mu430WcRwvEOmZtCqRxvM2o2
Js0UX8XE957EM2yDBzhqGYO7x5BrP9ulZaC3drMuigX1eaHu6ra1RgqdAdgEaRrr
OQEEAMN/+Ogqls1eKKi7paHZkfFR/440pDavcKesBqV/SU/FJX+GelggS3GaTwij
OJLJkUeNS22DgojiPpD1o5U9qhYckW31CSfSXW11WWOq1LwtGLONHHPwfeTn2iPX
wnXgchfZBcQcMhTtQkIZHlEOqNNY1Y/gzmtLoRwCZ6kAxemPABEBAAEAA/9c8bru
+cx/L5xJ+AhbZbpWTgMe4xUNMKRw+r6gMN80TwiwU8lXm2byyAd6FktfsffhWiH5
m1PUayeOuFHAsrPpAUHZ+f88pAenCPR63vhB14dQBfp9HA9RuR//INLcIyI8S0EL
FzuoGpKkBCHV+rQv+4/UocdYjPnSXfm/dUa/6QIA1EScvQX3Wfh1IYsF975SoIZ5
/Y2CRx00l7Ai8UGFfjpf1HDsim/moXXrDYLYAp8PGBoo+hqghHSx6Bo1cwaRqQIA
68b6zYb2KCjd+xk2yZhYw9IQstjtV/NPjMx4kHqYqHbRD7MOBENjT1yxGzYZVbRN
kwQS3znDxFC1Db4yPv8UdwIA6EyuZCGEnfIceXVeROhBVQSMc0opiuvIHowNtfZe
f/MA3fL+KP7cvwcTN0Ezwsf8nbYYhipZOQKuKkLxlLjZiKFaiLYEGAEKACAWIQTB
mTyP+nk6kbIbWzYGf7wmA7LVawUCaRrrOQIbDAAKCRAGf7wmA7LVawTaBACwMK5Y
t5KMGN/p3j7wkFKJoELcLRpQ896z/9N+i+WmNtpXsKrs5Gw5HYjobWSbXXF62u9B
Zpysy6Xz6IE6vIojI4DAIwcPck4eSe9cldKNaVsXUHWs3SRXby3BTyfSs8GxiBV2
TTx3GkRAZLJUIM7Rh3yb4TuYCo5iSufiEWnPrw==
=KjE/
-----END PGP PRIVATE KEY BLOCK-----
1fbcf99a5131a6a0094c2a40a1a0b8dddeka@SKH-KUBUNTU:~$ 


curl -X POST http://127.0.0.1:5001/submit/private -F "file=@priv.key"


deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5001/submit/private -F "file=@priv.key"
{
  "algo": "1",
  "created": "1763371833",
  "expires": "Never",
  "fingerprint": "C1993C8FFA793A91B21B5B36067FBC2603B2D56B",
  "key_id": "067FBC2603B2D56B",
  "length": "1024",
  "trust": "-",
  "type": "private",
  "uids": [
    "jakub (none) <jakub@test.pl>"
  ]
}





zad2

deka@SKH-KUBUNTU:~$ gpg --full-generate-key
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 2
DSA keys may be between 1024 and 3072 bits long.
What keysize do you want? (2048) 1024
Requested keysize is 1024 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: Aki
Name must be at least 5 characters long
Real name: Akis
Name must be at least 5 characters long
Real name: Aakis
Email address: Aakis@test.pl
Comment: skip
You selected this USER-ID:
    "Aakis (skip) <Aakis@test.pl>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: revocation certificate stored as '/home/deka/.gnupg/openpgp-revocs.d/50230753DCA45B5838FAA8715B2D42C08D873620.rev'
public and secret key created and signed.

pub   dsa1024 2025-11-17 [SC]
      50230753DCA45B5838FAA8715B2D42C08D873620
uid                      Aakis (skip) <Aakis@test.pl>
sub   elg1024 2025-11-17 [E]


deka@SKH-KUBUNTU:~$ gpg --armor --export-secret-key Aakis@test.pl >priv.key
deka@SKH-KUBUNTU:~$ gpg --armor --export Aakis@test.pl >pub.key


deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5002/submit/public -F "file=@pub.key"
{
  "algorithm": "DSA",
  "created": "1763372357",
  "expires": "Never",
  "fingerprint": "50230753DCA45B5838FAA8715B2D42C08D873620",
  "format": "GPG/OpenPGP",
  "key_id": "5B2D42C08D873620",
  "key_size": 1024,
  "trust": "-",
  "type": "public",
  "uids": [
    "Aakis (skip) <Aakis@test.pl>"
  ]
}




deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5002/submit/private -F "file=@priv.key"
{
  "algorithm": "DSA",
  "created": "1763372357",
  "expires": "Never",
  "fingerprint": "50230753DCA45B5838FAA8715B2D42C08D873620",
  "format": "GPG/OpenPGP",
  "key_id": "5B2D42C08D873620",
  "key_size": 1024,
  "trust": "-",
  "type": "private",
  "uids": [
    "Aakis (skip) <Aakis@test.pl>"
  ]
}




zad5.3
deka@SKH-KUBUNTU:~$ gpg --full-generate-key
gpg (GnuPG) 2.2.40; Copyright (C) 2022 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 1024
Requested keysize is 1024 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) y
invalid value
Key is valid for? (0) 1y
Key expires at wto, 17 lis 2026, 10:49:25 CET
Is this correct? (y/N) y

GnuPG needs to construct a user ID to identify your key.

Real name: student
Email address: student@uczelnia.pl
Comment: none
You selected this USER-ID:
    "student (none) <student@uczelnia.pl>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: revocation certificate stored as '/home/deka/.gnupg/openpgp-revocs.d/70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA.rev'
public and secret key created and signed.

pub   rsa1024 2025-11-17 [SC] [expires: 2026-11-17]
      70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA
uid                      student (none) <student@uczelnia.pl>
sub   rsa1024 2025-11-17 [E] [expires: 2026-11-17]


deka@SKH-KUBUNTU:~$ gpg --armor --export student@uczelnia.pl >pub.key
deka@SKH-KUBUNTU:~$ gpg --armor --export-secret-key student@uczelnia.pl >priv.key

deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5003/submit/public -F "file=@pub.key"
{
  "algo": "1",
  "created": "1763372981",
  "expires": "1794908981",
  "fingerprint": "70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA",
  "key_id": "C6685D25EFE79CFA",
  "length": "1024",
  "trust": "-",
  "type": "public",
  "uids": [
    "student (none) <student@uczelnia.pl>"
  ],
  "validation": "passed"
}

deka@SKH-KUBUNTU:~$ curl -X POST http://127.0.0.1:5003/submit/private -F "file=@priv.key"
{
  "algo": "1",
  "created": "1763372981",
  "expires": "1794908981",
  "fingerprint": "70FD0D34955EDE90D76F4A2BC6685D25EFE79CFA",
  "key_id": "C6685D25EFE79CFA",
  "length": "1024",
  "trust": "-",
  "type": "private",
  "uids": [
    "student (none) <student@uczelnia.pl>"
  ],
  "validation": "passed"
}
























