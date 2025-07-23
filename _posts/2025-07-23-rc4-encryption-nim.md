---
layout: post
canonical_url: https://www.cheesydoodle.com
toc: true
title: "[Doc] Simple RC4 Encryption in Nim — Practical, Lightweight, and Still Useful"
date: 2025-07-23
categories: [Blog, Posts]
tags:
  [
    "Nim",
    "Encryption",
    "RC4",
    "Code Snippet",
    "Reverse Engineering",
    "Cheat Development",
  ]
excerpt: "A lightweight RC4 encryption and decryption implementation in Nim. Great for hiding runtime strings, internal commands, or obfuscating config data."
---

I originally wrote this RC4 implementation years ago in Delphi, back when I was working on game hacks for _Combat Arms_. One of the recurring challenges back then was keeping certain strings — especially internal console messages or debug output — **out of plain sight** in memory.

Any string like `"Aimbot Enabled"` sitting unencrypted is just asking to be flagged by an anti-cheat engine scanning memory. The solution was straightforward: **encrypt the strings**, and **only decrypt them at runtime** when needed. I used RC4 for that. Fast, easy to implement, and more than enough for the job.

Recently, I ported the same logic to **Nim**, mostly as an exercise — but also because the use cases for something like this haven’t gone away.

## The RC4 Implementation in Nim

RC4 is a stream cipher, and its strength lies in its simplicity. Here’s the Nim version of the full encryption and decryption logic:

### Key Scheduling Algorithm (KSA)

```nim
proc rc4KeyInit(Key: string): array[0..255, int] =
  var
    i, j, intChar: int = 0
    result: array[0..255, int]
  for i in 0..255:
    result[i] = i
  for i in 0..255:
    intChar = ord(char(Key[i mod Key.len]))
    j = (j + result[i] + intChar) mod 256
    swap(result[i], result[j])
  result
```

### Encryption and Decryption

```nim
proc rc4CryptDecrypt*(Key, Text: string, encrypt: bool ): string =
  ## Encrypts or decrypts the given `Text` using the RC4 algorithm with the provided `Key`.
  ## If `encrypt` is true, the function performs encryption; otherwise, it performs decryption.
  ## Returns the encrypted/decrypted string.

  if Key.len == 0:
    raise newException(ValueError, "Key cannot be empty")

  var
    i, j, y: int = 0
    arrKey: array[0..255, int]
    intChar: int
    strResult: string = ""

  arrKey = rc4KeyInit(Key)

  if encrypt:
    for y in 0..pred(Text.len):
      i = (succ(i)) mod 256
      j = (j + arrKey[i]) mod 256
      swap(arrKey[i], arrKey[j])
      intChar = ord(char(Text[y])) xor arrKey[(arrKey[i] + arrKey[j]) mod 256]
      strResult = strResult & toHex(intChar, 2)
  else:
    if Text.len mod 2 != 0 or Text.len == 0:
      raise newException(ValueError, "Encrypted text must be a non-empty hexadecimal string with an even length")

    while y < pred(Text.len):
      i = (succ(i)) mod 256
      j = (j + arrKey[i]) mod 256
      swap(arrKey[i], arrKey[j])
      intChar = fromHex[int](Text[y] & Text[succ(y)] ) xor arrKey[(arrKey[i] + arrKey[j]) mod 256]
      strResult = strResult & (intChar).char
      inc(y, 2)

  result = strResult

```

The function works in both directions. RC4 is a symmetric algorithm, so encryption and decryption use the same logic — the only difference here is how the data is handled.

- When `encrypt` is `true`, it takes the input string and returns a hex-encoded ciphertext.
- When `encrypt` is `false`, it expects a hex string and returns the original plaintext.

It includes basic error checking — for example, if a malformed hex string is passed during decryption, it raises a `ValueError`.

### Built-in Test Block

```nim
when isMainModule:
  block:
    let
      key = "MySecretKey"
      plaintext = "Hello, World!"
      ciphertext = rc4CryptDecrypt(key, plaintext, true)
      decrypted = rc4CryptDecrypt(key, ciphertext, false)
    doAssert decrypted == plaintext, "Encryption/Decryption failed"
    ...
```

## Why RC4?

RC4 isn’t cutting-edge anymore, and it’s definitely not suited for serious cryptographic applications today — that much is well-known. But it still has value in the right context:

- Hiding sensitive strings from static analysis or memory scanning
- Light obfuscation of config data or internal commands
- Simple runtime string protection in tools or utilities

It’s small, fast, and doesn’t need any external libraries.

## Real Use Case

In the _Combat Arms_ project I mentioned earlier, I used this to encrypt console command strings and internal messages. The encrypted values were stored inside the binary or loaded dynamically, and decrypted only in memory just before use.

Since then, I’ve reused this approach in a few different tools — some game-related, some not.

## Summary

- Clean RC4 implementation in Nim
- Great for lightweight runtime encryption
- Not suitable for secure cryptography
- Helpful for hiding strings and adding simple obfuscation

If you're interested in more code like this, feel free to explore the rest of the blog at [cheesydoodle.com](https://www.cheesydoodle.com).
