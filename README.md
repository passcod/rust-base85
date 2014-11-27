# Base85

Like [Base64], but encodes four bytes of binary into five characters of ASCII,
achieving a 25% increase instead of 33%. Unlike Base64, though, it doesn't have
a single most-used variant. This crate implements the four most common, plus a
variant suitable for use as filenames, and has an option for a custom character
set.

## Usage

The crate is designed following the Base64 implementation in the
[Standard Library]. Because it is outside the stdlib, though, it provides
methods on the `base85::Config` struct:

```rust
extern crate base85;

let codec = base85::Z85; // See below for variants, or construct your own:
let custom = base85::Config {
  char_set: base85::Filename,
  all_zero: None,
  line_length: Some(123)
};

let plain = "Hello world";
let encoded = codec.from_str(&plain_text);
let decoded = codec.to_str(&encoded);
assert_eq!(plain, decoded);
```

## Variants

- `ASCII85` - Adobe's variant for PostScript
- `BTOA` - Original by Paul E. Rutter
- `FILENAME` - Z85 variant for use in filenames
- `RFC1924` - Esoteric variant "for IPv6"
- `Z85` - Variant used in ZeroMQ

## Sources and specs

- [Wikipedia]
- [Adobe PostScript Reference]
- [Btoa] and [Atob] source code
- [Z85 specification]
- [RFC1924] - (Yes, this is an April Fools')
- [Javascript implementation]

## Etc

- Public Domain
- Pull requests welcome
- Say hi! :D

[Adobe PostScript Reference]: http://www.adobe.com/products/postscript/pdfs/PLRM.pdf
[Atob]: http://www.ibiblio.org/pub/packages/ccic/software/unix/utils/atob.c
[Base64]: http://en.wikipedia.org/wiki/Base64
[Btoa]: http://www.ibiblio.org/pub/packages/ccic/software/unix/utils/btoa.c
[Javascript implementation]: https://github.com/noseglid/base85
[RFC1924]: http://tools.ietf.org/html/rfc1924
[Standard Library]: http://doc.rust-lang.org/serialize/base64/index.html
[Wikipedia]: http://en.wikipedia.org/wiki/Ascii85
[Z85 specification]: http://rfc.zeromq.org/spec:32
