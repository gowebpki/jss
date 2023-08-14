# JSON Signature Scheme (JSS)

## Abstract

This document carries the proposed 1st revision of the baseline text for X.jss:
JSON Signature Scheme (JSS).

X.jss defines a method called JSS (JSON Signature Scheme) which enables JSON
objects to be signed and/or countersigned while leaving the original JSON
objects themselves in JSON format. This process enables a consistent data
format that simplifies the use, documentation, debugging, and logging of the
JSON data while still allowing it to be digitally signed. Further, with this
method, signed JSON objects can be used and processed just like standard JSON
objects which simplifies their use for application developers and systems.


## Introduction

This document introduces a method for digitally signing data expressed in the
JSON [IETF RFC 8259] notation. For interoperability and security reasons this
specification requires JSON objects to be in the I-JSON [IETF RFC 7493] subset
and uses the JSON Canonicalization Scheme (JCS) [IETF RFC 8785] for
canonicalization. This method enables signed JSON objects to be kept in JSON
format and is referred to as JSON Signature Scheme (JSS).

The primary motivations for keeping signed JSON objects in JSON format include
simplified use, documentation, debugging, and logging, as well as for
maintaining a consistent message structure. This will greatly improve and
simplify their use in applications and systems. Further, this will also allow
objects to be signed after the fact, by third parties, and even counter
signed.

Another use case is HTTP-based signature schemes that currently utilize HTTP
header values for holding detached signatures. By using the method described
herein, signed JSON-formatted HTTP requests and responses may be self-contained
and thus be serializable. The latter facilitates such data to be:

 - stored in databases
 - passed through intermediaries
 - embedded in other JSON objects
 - countersigned

without losing the ability (at any time) to verify signatures.


# 1 Scope

This document proposes a Recommendation that can be used throughout the modern
Internet to enable JSON encoded data to be digitally signed thus providing
authenticity and verifiability of the data. This Recommendation would be
applicable to many sectors, organizations, and products such as signing
financial transactions, real estate transactions, electronic contracts, threat
intelligence data, and vendor API calls.

# 2 References

## The following references are in ITU-T format 

**[IETF RFC 2119]** IETF RFC 2119 (1997), Key words for use in RFCs to Indicate Requirement Levels.

**[IETF RFC 2818]** IETF RFC 2818 (2000), HTTP Over TLS.

**[IETF RFC 3339]** IETF RFC 3339 (2002), Date and Time on the Internet: Timestamps.

**[IETF RFC 3986]** IETF RFC 3986 (2005), Uniform Resource Identifier (URI): Generic Syntax.

**[IETF RFC 4122]** IETF RFC 4122 (2005), A Universally Unique IDentifier (UUID) URN Namespace.

**[IETF RFC 4648]** IETF RFC 4648 (2006), The Base16, Base32, and Base64 Data Encodings.

**[IETF RFC 4945]** IETF 4945 (2007), The Internet IP Security PKI Profile of IKEv1/ISAKMP, IKEv2, and PKIX.

**[IETF RFC 5246]** IETF 5246 (2008), The Transport Layer Security (TLS) Protocol Version 1.2.

**[IETF RFC 5280]** IETF 5280 (2008), Internet X.509 Public Key Infrastructure Certificate and  Certificate Revocation List (CRL) Profile.

**[IETF RFC 6125]** IETF 6126 (2011), Representation and Verification of Domain-Based Application Service Identity within Internet Public Key Infrastructure Using X.509 (PKIX) Certificates in the Context of Transport Layer Security (TLS).

**[IETF RFC 7493]** IETF RFC 7493 (2015), The I-JSON Message Format.

**[IETF RFC 7515]** IETF RFC 7515 (2015), JSON Web Signature (JWS).

**[IETF RFC 7517]** IETF RFC 7517 (2015), JSON Web Key (JWK).

**[IETF RFC 7518]** IETF RFC 7518 (2015), JSON Web Algorithms (JWA).

**[IETF RFC 8032]** IETF RFC 8032 (2017), Edwards-Curve Digital Signature Algorithm (EdDSA).

**[IETF RFC 8037]** IETF 8037 (2017), CFRG Elliptic Curve Diffie-Hellman (ECDH) and Signatures in JSON Object Signing and Encryption (JOSE).

**[IETF RFC 8174]** IETF RFC 8174 (2017), Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words.

**[IETF RFC 8259]** IETF RFC 8259 (2017), The JavaScript Object Notation (JSON) Data Interchange Format.

**[IETF RFC 8391]** IETF RFC 8391 (2018), XMSS: eXtended Merkle Signature Scheme.

**[IETF RFC 8554]** IETF RFC 8554 (2019), Leighton-Micali Hash-Based Signatures.

**[IETF RFC 8785]** IETF RFC 8785 (2020), JSON Canonicalization Scheme (JCS).

**[ISO/IEC 10646]** ISO/IEC 10646 (2014), Information technology -- Universal Coded Character Set (UCS).

**[UNICODE TR15]** Unicode® Standard Annex #15(2016), UNICODE NORMALIZATION FORMS.

**[NIST FIPS 180-4]** National Institute of Standards and Technology (NIST) FIPS180-4 (2015), Secure Hash Standard (SHS).

## The following references are in OASIS format 

### Normative References
**[RFC2119]** Bradner, S., "Key words for use in RFCs to Indicate Requirement
  Levels", BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997,
  https://www.rfc-editor.org/info/rfc2119.

**[RFC2818]** Rescorla, E., "HTTP Over TLS", RFC 2818, DOI 10.17487/RFC2818, May
  2000, https://www.rfc-editor.org/info/rfc2818.

**[RFC3339]** Klyne, G. and C. Newman, "Date and Time on the Internet:
  Timestamps", RFC 3339, DOI 10.17487/RFC3339, July 2002,
  https://www.rfc-editor.org/info/rfc3339.

**[RFC3986]** Berners-Lee, T., Fielding, R., and L. Masinter, "Uniform Resource
  Identifier (URI): Generic Syntax", STD 66, RFC 3986, DOI 10.17487/RFC3986,
  January 2005, https://www.rfc-editor.org/info/rfc3986.

**[RFC4122]** Leach, P., Mealling, M., and R. Salz, "A Universally Unique
  IDentifier (UUID) URN Namespace", RFC 4122, DOI 10.17487/RFC4122, July 2005,
  https://www.rfc-editor.org/info/rfc4122.

**[RFC4648]** Josefsson, S., "The Base16, Base32, and Base64 Data Encodings",
  RFC 4648, DOI 10.17487/RFC4648, October 2006,
  https://www.rfc-editor.org/info/rfc4648.

**[RFC4945]** Korver, B., "The Internet IP Security PKI Profile of IKEv1/ISAKMP,
  IKEv2, and PKIX", RFC 4945, DOI 10.17487/RFC4945, August 2007,
  https://www.rfc-editor.org/info/rfc4945.

**[RFC5246]** Dierks, T. and E. Rescorla, "The Transport Layer Security
  (TLS) Protocol Version 1.2", RFC 5246, DOI 10.17487/RFC5246, August 2008,
  https://www.rfc-editor.org/info/rfc5246.

**[RFC5280]** Cooper, D., Santesson, S., Farrell, S., Boeyen, S., Housley, R.,
  and W. Polk, "Internet X.509 Public Key Infrastructure Certificate and
  Certificate Revocation List (CRL) Profile", RFC 5280, DOI 10.17487/RFC5280,
  May 2008, https://www.rfc-editor.org/info/rfc5280.

**[RFC6125]** Saint-Andre, P. and J. Hodges, "Representation and Verification of
  Domain-Based Application Service Identity within Internet Public Key
  Infrastructure Using X.509 (PKIX) Certificates in the Context of Transport
  Layer Security (TLS)", RFC 6125, DOI 10.17487/RFC6125, March 2011,
  https://www.rfc-editor.org/info/rfc6125.

**[RFC7493]** Bray, T., Ed., "The I-JSON Message Format", RFC 7493, DOI
  10.17487/RFC7493, March 2015, https://www.rfc-editor.org/info/rfc7493.

**[RFC7515]** Jones, M., Bradley, J., and N. Sakimura, "JSON Web Signature
  (JWS)", RFC 7515, DOI 10.17487/RFC7515, May 2015,
  https://www.rfc-editor.org/info/rfc7515.

**[RFC 7517]** Jones, M., "JSON Web Key (JWK)", RFC 7517, DOI 10.17487/RFC7517,
  May 2015, https://www.rfc-editor.org/info/rfc7517.

**[RFC7518]** Jones, M., "JSON Web Algorithms (JWA)", RFC 7518, DOI
  10.17487/RFC7518, May 2015, https://www.rfc-editor.org/info/rfc7518.

**[RFC8032]** Josefsson, S. and I. Liusvaara, "Edwards-Curve Digital Signature
  Algorithm (EdDSA)", RFC 8032, DOI 10.17487/RFC8032, January 2017,
  https://www.rfc-editor.org/info/rfc8032.

**[RFC8037]** Liusvaara, I., "CFRG Elliptic Curve Diffie-Hellman (ECDH) and
  Signatures in JSON Object Signing and Encryption (JOSE)", RFC 8037, DOI
  10.17487/RFC8037, January 2017, https://www.rfc-editor.org/info/rfc8037.

**[RFC8174]** Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC 2119 Key
  Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174, May 2017,
  https://www.rfc-editor.org/info/rfc8174.

**[RFC8259]** Bray, T., Ed., "The JavaScript Object Notation (JSON) Data
  Interchange Format", STD 90, RFC 8259, DOI 10.17487/RFC8259, December 2017,
  https://www.rfc-editor.org/info/rfc8259.

**[RFC8785]** Rundgren, A., Jordan, B., and S. Erdtman, "JSON Canonicalization
  Scheme (JCS)", RFC 8785, DOI 10.17487/RFC8785, June 2020,
  https://www.rfc-editor.org/info/rfc8785.

**[UNICODE]** The Unicode Consortium, "The Unicode Standard",
  https://www.unicode.org/versions/latest/.

### Informative References

**[SHS]** NIST, "Secure Hash Standard (SHS)", FIPS PUB 180-4, August 2015, <https://nvlpubs.nist.gov/nistpubs/FIPS/ NIST.FIPS.180-4.pdf>


# 4 Abbreviations and acronyms
This Recommendation uses the following abbreviations and acronyms:

`IETF` - Internet Engineering Task Force

`JSON` - JavaScript Object Notation

`JSS` - JSON Signature Scheme

`JCS` - JSON Canonicalization Scheme

`PEM` - Privacy Enhanced Mail

`PKCS` - Public Key Cryptography Standards

`RSA` - Rivest-Shamir-Adleman

`RFC` - Request for Comment (IETF work product)

# 5 Conventions

## Terminology

The key words "**MUST**", "**MUST NOT**", "**REQUIRED**", "**SHALL**", "**SHALL
NOT**", "**SHOULD**", "**SHOULD NOT**", "**RECOMMENDED**", "**NOT
RECOMMENDED**", "**MAY**", and "**OPTIONAL**" in this document are to be
interpreted as described in BCP 14 [RFC2119] [RFC8174] when, and only when,
they appear in all capitals, as shown here.

The following color, font and font style conventions are used in this document:

 - The Consolas font is used for all type names and property names.
   - type names are in red with a light red background – `string`
   - property names are in bold style – **algorithm**
 - All examples in this document are expressed in JSON. They are in Consolas
   9-point font, with straight quotes, black text, and using 2-space
   indentation. JSON examples in this document are representations of JSON
   objects [IETF RFC 8259]. They should not be interpreted as string literals.
   The ordering of keys is insignificant. Whitespace before or after JSON
   structural characters in the examples are insignificant [IETF RFC 8259].
 - Parts of the example may be omitted for conciseness and clarity. These
   omitted parts are denoted with the ellipses (...) or inside of double
   dashes (-- some data --).

# 6 Signature Object

Each JSON object that is digitally signed based on this specification can have
one or more signatures validating the JSON object. These signatures can be
either attached or detached from the original JSON object. Each digital
signature along with its meta-data **MUST** be contained within a unique JSS
Signature object. This section defines the JSS Signature object.

The JSS Signature object defined in this section captures basic meta-data about
the signature, the hashing and signing algorithms used, and the actual digital
signature (the hash of the complete JSON object encrypted with a private key)
and uses the JSON object type [IETF RFC 8259] for serialization. The official
properties for the JSS Signature object can be found in section 6.2. In
addition to the official properties, section 6.3 lists out some additional
meta-data properties for the JSS Signature object that some implementations may
find useful. Any additional meta-data properties are implementation and use
case specific and are not limited to those found in section 6.3.

A conformant JSS system **MUST** use the signature object defined in this
specification. Each digital signature **MUST** pertain to the JSON object that
it is attached to. Implementations **SHOULD** store the signature object in a
property called "**signatures**". The property that holds the signature **MUST** be
a JSON list property and **MUST** be located at the top-level of the original
JSON object. If "signatures" is not used then the chosen property name **MUST
NOT** clash with any other top-level property names. 


## 6.1 Data Types

This section contains the details for various data types used in the properties
defined in section 6.2 and section 6.3.

The `boolean` data type is a literal unquoted value of either true or false and
uses the JSON true and false values [IETF RFC 8259] for serialization.

The `identifier` data type represents an RFC 4122-compliant UUID [IETF RFC 4122]
and uses the JSON string type [IETF RFC 8259] for serialization.

The `string` data type represents a finite-length string of valid characters
from the Unicode coded character set [ISO/IEC 10646] and uses the JSON string
type [IETF RFC 8259] for serialization.

The `timestamp` data type represents dates and times and uses the JSON string
type [IETF RFC 8259] for serialization. The timestamp data **MUST** be a valid
RFC 3339-formatted timestamp [IETF RFC 3339] using the format
yyyy-mm-ddThh:mm:ss[.s+]Z where the "s+" represents 1 or more sub-second
values. The brackets denote that sub-second precision is optional, and that if
no digits are provided, the decimal place **MUST NOT** be present. The
timestamp **MUST** be represented in the UTC+0 timezone and **MUST** use
the "Z" designation to indicate this. Additional requirements may be defined
where this data type is used.


## 6.2 JSS Signature Object Properties

This section contains a list of properties that define the JSS signature object
along with any normative rules or requirements for their use. Implementers of
this specification **MAY** add additional properties to satisfy the meta-data
requirements for their application (see 6.3 for notional examples).

### 6.2.1 Properties

`hash_algorithm` (required) `string` This property identifies the hashing
algorithm, as defined by IANA, that was used to hash the JCS version of the
full JSON object (JSON Object + JSS Signature) and is a case-sensitive ASCII
string. Implementations **MAY** use any current and widely accepted hashing
algorithm (e.g., sha-256, sha-512) that is defined in the IANA registry. The
actual signing process, defined in the **algorithm** property, sometimes uses an
internal hashing algorithm inside the signing process itself, this
property **MAY** identify the same hashing algorithm as the signing process
or **MAY** identify a different hashing algorithm.

`algorithm` (required) `string` This property identifies the algorithm that was
used to sign the JSON data and is a case-sensitive ASCII string. The value for
this property **SHOULD** come from the signature-algorithm-type-ov vocabulary
(see section 6.2.2) and **SHOULD** be a current and widely accepted quantum
safe algorithm, but **MAY** use any currently accepted safe algorithm.

`public_key` (optional*) `string` This property contains a PEM encoded public
key without the header and footer for the algorithm selected in
the **algorithm** property.

`public_cert_chain` (optional*) `list` of `string` This property contains a
public key certificate for the algorithm selected in the **algorithm** property
and **MUST** follow the requirements defined in section 4.7 of [IETF RFC 7517]
as quoted here. This property "contains a chain (X.509 certificate chain) of
one or more PKIX certificates [IETF RFC 5280]. The certificate chain is
represented as a JSON array of certificate value strings. Each string in the
array is a base64-encoded (Section 4 of [IETF RFC 4648] -- not
base64URL.encoded) DER [ITU.X690.1994] PKIX certificate value. The PKIX
certificate containing the key value **MUST** be the first certificate.
This **MAY** be followed by additional certificates, with each subsequent
certificate being the one used to certify the previous one. The key in the
first certificate **MUST** match the public key." This property is called "x5c"
in section 4.7 of [IETF RFC 7517].

`cert_url` (optional*) `string` This property contains a URI [IETF RFC 3986]
that refers to a resource for an X.509 public key certificate or certificate
chain [IETF RFC 5280] for the algorithm selected in the **algorithm** property
and **MUST** follow the requirements defined in section 4.6 of [IETF RFC 7517]
as quoted here. "The identified resource **MUST** provide a representation of
the certificate or certificate chain that conforms to RFC 5280 [IETF RFC 5280]
in PEM-encoded form, with each certificate delimited as specified in section
6.1 of RFC 4945 [IETF RFC 4945]. The key in the first certificate **MUST**
match the public key. The protocol used to acquire the resource **MUST**
provide integrity protection; an HTTP GET request to retrieve the
certificate **MUST** use TLS [IETF RFC 2818] [IETF RFC 5246]; the identity of
the server **MUST** be validated, as per section 6 of RFC 6125 [IETF RFC
6125]." This property is called "x5u" in section 4.6 of [IETF RFC 7517].

`thumbprint` (optional*) `string` This property contains a fingerprint of a
public key or public key certificate for the algorithm selected in the
**algorithm** property and **MUST** follow the requirements defined in section 4.9
of [IETF RFC 7517] as quoted here. This property "is a base64URL.encoded
SHA-256 thumbprint (a.k.a. digest, X.509 certificate SHA-256 thumbprint) of the
DER encoding of an X.509 certificate [IETF RFC 5280]. Note that certificate
thumbprints are also sometimes known as certificate fingerprints. The key in
the certificate **MUST** match the public key." This property is
called "x5t#S256" in section 4.9 of [IETF RFC 7517].

`value` (required) `string` A base64URL.encoded signature that was created using
the signature algorithm defined in the **algorithm** property and a key. In pseudo
code it is defined as: `base64URL.encode(sign(algorithm, key, hash(jcs
(<JSONObject with Signature Object>))))`.

`signature` (optional) `JSS Signature object` This property enables a signature
to be countersigned, meaning a signature can be signed by another signature.


One of the following properties **MUST** be populated, **public_key**,
**public_cert_chain**, **cert_url**, or **thumbprint**.

#### Single Signature Example

```
{
  "statement": "Hello signed world!",
  "otherProperties": ["home", "food"],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- a digital signature --"
    }
  ]
}
```

#### Multiple Signatures Example

```
{
  "statement": "Hello signed world!",
  "otherProperties": ["home", "food"],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- public key 1 --",
      "value": "-- digital signature 1 --"
    },
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some other public key 2 --",
      "value": "-- some other digital signature 2 --"
    }
  ]
}
```

#### Countersigned Signature Example

```
{
  "statement": "Hello signed world!",
  "otherProperties": ["home", "food"],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- a digital signature --",
      "signature": {
        "hash_algorithm": "-- some hashing algorithm --",
        "algorithm": "-- some signing algorithm --",
        "public_key": "-- some other public key 2 --",
        "value": "-- some other digital signature 2 --"
      }
    }
  ]
}
```

### 6.2.2 Signature Algorithm Type Vocabulary

Vocabulary Name: `signature-algorithm-type-ov`

Note: at the time of this writing quantum safe algorithms could come from those
defined in XMSS [IETF RFC 8391] section 5.3 or LMS [IETF RFC 8554] section 5.1
and other algorithms could come from those defined in JWA [IETF RFC 7518]
section 3.1 or [IETF RFC 8037] section 3.1 (see the table below for a list of
values from those RFCs).

While JWA [IETF RFC 7518] section 3.1 defines the following symmetric
algorithms: HS256, HS384, and HS512, these algorithms **SHOULD NOT** be used.
If one of these three symmetric algorithms is used, the sharing and
transmission of those keys is out of scope for this specification.

| Vocabulary Value | Description |
|---|---|
| XMSS-SHA2_10_256 | See section 5.3 of XMSS [RFC 8391] for more information. |
| XMSS-SHA2_16_256 | See section 5.3 of XMSS [RFC 8391] for more information. |
| XMSS-SHA2_20_256 | See section 5.3 of XMSS [RFC 8391] for more information. |
| LMS_SHA256_M32_H5 | See section 5.1 of LBS [RFC 8554] for more information. |
| LMS_SHA256_M32_H10 | See section 5.1 of LBS [RFC 8554] for more information. |
| LMS_SHA256_M32_H15 | See section 5.1 of LBS [RFC 8554] for more information. |
| LMS_SHA256_M32_H20 | See section 5.1 of LBS [RFC 8554] for more information. |
| LMS_SHA256_M32_H25 | See section 5.1 of LBS [RFC 8554] for more information. |
| RS256 | RSASSA-PKCS1-v1_5 using SHA-256. See section 3.3 of JWA [RFC 7518] for more information. This method is recommended  per JWA [RFC7518]. |
| RS384 | RSASSA-PKCS1-v1_5 using SHA-384. See section 3.3 of JWA [RFC 7518] for more information. |
| RS512 | RSASSA-PKCS1-v1_5 using SHA-512. See section 3.3 of JWA [RFC 7518] for more information. | 
| ES256 | ECDSA using P-256 and SHA-256. See section 3.4 of JWA [RFC 7518] for more information. This method is recommended per JWA [RFC7518]. |
| ES384 | ECDSA using P-384 and SHA-384. See section 3.4 of JWA [RFC 7518] for more information. |
| ES512 | ECDSA using P-521 and SHA-512. See section 3.4 of JWA [RFC 7518] for more information. |
| PS256 | RSASSA-PSS using SHA-256 and MGF1 with SHA-256. See section 3.5 of JWA [RFC 7518] for more information. |
| PS384 | RSASSA-PSS using SHA-384 and MGF1 with SHA-384. See section 3.5 of JWA [RFC 7518] for more information. |
| PS512 | RSASSA-PSS using SHA-512 and MGF1 with SHA-512. See section 3.5 of JWA [RFC 7518] for more information. |
| Ed25519 | See [RFC 8037] and [RFC 8032] for more information. NOTE: Unlike RFC8037 [RFC8037] this specification requires explicit Ed* algorithm names (e.g. Ed25519) instead of generic versions like "EdDSA". |
| Ed448 | See [RFC 8037] and [RFC 8032] for more information. NOTE: Unlike RFC8037 [RFC8037] this specification requires explicit Ed* algorithm names (e.g. Ed448) instead of generic versions like "EdDSA". |


## 6.3 Examples of Additional Meta-Data Properties

This section contains a list of notional properties that implementations of this
specification **MAY** use. They are provided here for illustrative purposes but
are in no way exhaustive. The normative rules for their use are implementation
specific, but some guidance is included here.

### 6.3.1 Properties

`type` (required) `string` The value of this property **MUST** be jss.

`id` (required) `identifier` A value that uniquely identifies the signature. All
signatures with the same ID are considered different versions of the same
signature and the version of the signature is identified by its **modified**
property.

`related_to` (optional) `string` A value that can identify the original JSON
object that was signed with this signature. If the signature is detached from
the original JSON object this property **SHOULD** be populated.

`related_version` (optional) `string` A value that can identify the version of
the original JSON object that was signed with this signature. If the signature
is detached from the original JSON object this property **SHOULD** be
populated.

`created` (required) `timestamp` The time at which this signature was originally
created. The creator can use any time it deems most appropriate as the time the
signature was created, but it **MUST** be precise to the nearest millisecond
(exactly three digits after the decimal place in seconds). The **created**
property **MUST NOT** be changed when creating a new version of the signature.

`modified` (required) `timestamp` The time that this particular version of the
signature was last modified. The creator can use any time it deems most
appropriate as the time that this version of the signature was modified, but
it **MUST** be precise to the nearest millisecond (exactly three digits after
the decimal place in seconds). The **modified** property **MUST** be later than or
equal to the value of the **created** property. If the **created** and **modified**
properties are the same, then this is the first version of the signature.

`revoked` (optional) `boolean` A boolean that identifies if the signature
creator deems that this signature is no longer valid. The default value is
false.

`signee` (optional) `string` The name of the entity or organization that
produced this signature. This property is similar to the X.509 fields.

`valid_from` (optional) `timestamp` The time from which this signature is
considered valid. If omitted, the signature is valid at all times or until the
timestamp defined by valid_until. If the **revoked** property is true then this
property **MUST** be ignored.

`valid_until` (optional) `timestamp` The time at which this signature should no
longer be considered valid. If the **valid_until** property is omitted, then there
is no constraint on the latest time for which the signature is valid. This
property **MUST** be greater than the timestamp in the **valid_from** property if
the **valid_from** property is defined. If the **revoked** property is true then this
property **MUST** be ignored.


# 7 Detailed Signing Operation

This section describes the details related to signing JSON objects based on this
specification.

The following characteristics are crucial to know for prospective JSS
implementers and users:

 - JSON data to be signed **MUST** be supplied as JSON objects. That is, direct
   signing of JSON arrays or JSON primitives is out of scope for this
   specification.
 - JSON data to be signed **MUST** be compliant with I-JSON [IETF RFC 7493] as JCS
   [IETF RFC 8785] requires JSON objects to be in the I-JSON [IETF RFC 7493]
   subset.

The examples in this section feature Ed25519 keys as defined in Appendix B.

NOTE: The following examples use the Ed25519 algorithm for illustrative
purposes. Implementations **SHOULD** use quantum safe options.

## 7.1 Signature Creation

The following subsections describe how JSON objects can be signed using one or
more signatures. These JSS Signature objects will be stored in a property
called **signatures** on the original JSON object but could also be detached and
stored or shared separately. If the signature will be detached, one **MUST** do
this at the very end, after the digital signature has been generated.

### 7.1.1 Create or parse the JSON object to be signed

This object has an existing signature, this is done to show how one would work
with existing signatures.

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- some existing digital signature --"
    }
  ]
}
```

### 7.1.2 Temporarily remove existing signature

If there is an existing signature then it will need to be temporarily removed.
If there is no existing signature on the object, then this step can be skipped.
When applied to the example in 7.1.1 the following JSON object should be
generated:

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ]
}
```

### 7.1.3 Create and add signature object

Create a JSS Signature object (see section 6.2) and add it to the **signatures**
property of the original JSON object. The public key in this example comes from
Appendix B.1. When applied to the example in 7.1.2 the following JSON object
should be generated:

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "sha-256",
      "algorithm": "Ed25519",
      "public_key": "MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU"
    }
  ]
}
```

### 7.1.4 Create JCS version of entire JSON object

Use the result of the previous step as input to the canonicalization process
described in JCS [IETF RFC 8785]. When applied to the example in 7.1.3, the
following JSON object should be generated:

```
{"otherProperties":["home","food"],"signatures":[{"algorithm":"Ed25519","hash_algorithm":"sha-256","public_key":"MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU"}],"statement":"Hello signed world!"}
```

### 7.1.5 Create hash of the JCS version

Using the hashing algorithm defined in the JSS Signature object hash the JCS
version of the full JSON object. When applied to the example in 7.1.4 and using
the sha-256 algorithm, the following hash (in hex) should be generated:

```
e005ae762a01723f3b58fa8edb2b2cc3b126ca087077189072cfd9a27e6079d5
```

### 7.1.6 Sign hash

Sign the hash from step 7.1.5 using the algorithm defined in the signature
object (Ed25519) and then base64URL.encode it. When applied to the example from
7.1.5, the signature value should look like:

```
F1Sj4VcZlSt5GO3Bcu4izpCklj9DbKDNvc2Trpdznfqgv9HMPUGVtefMsHfTqel-dN20lUXsdoeD8PpVr1ssCg
```

### 7.1.7 Assemble JSON object with signature

If there were existing signatures, add them back to the object at the start of
the list. Then append the new b64 digital signature from step 7.1.6 to the
signature value property. Based on the example, the object should look like:

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- some existing digital signature --"
    },
    {
      "hash_algorithm": "sha-256",
      "algorithm": "Ed25519",
      "public_key": "MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU",
      "value": "F1Sj4VcZlSt5GO3Bcu4izpCklj9DbKDNvc2Trpdznfqgv9HMPUGVtefMsHfTqel-dN20lUXsdoeD8PpVr1ssCg"
    }
  ]
}
```

## 7.2 Countersigned Signatures

The following subsections describe how JSON objects can be counter signed with a
countersigned signature. These JSS Signature objects will be stored in a
property called **signatures** on the original JSON object but could also be
detached and stored or shared separately. If the signature will be detached,
one **MUST** do this at the very end, after the digital signature has been
generated.

Appendix C gives an example of using the countersigned signatures as part of a
countersigned transaction.

### 7.2.1 Create or parse the JSON object to be signed

This object has an existing single signature that is also going to be
signed/countersigned in a chain. Unlike 7.1.2 the existing signature will not
be removed, since it will be signed as well as the original JSON data.

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- some existing digital signature --"
    }
  ]
}
```

### 7.2.2 Temporarily remove any existing signatures

If there are any other existing signatures then they will need to be temporarily
removed. If there are no other existing signatures on the object, then this
step can be skipped. Since there were no other existing signatures the
resulting JSON object will be the same as what is in 7.2.1. But it is included
again here for clarity.

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- some existing digital signature --"
    }
  ]
}
```

### 7.2.3 Create and add signature object

Create a JSS Signature object (see section 6.2) and add it to the **signature**
property of the existing JSS Signature object. The public key in this example
comes from Appendix B.1. When applied to the example in 7.2.2 the following
JSON object should be generated:

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- some existing digital signature --",
      "signature": {
        "hash_algorithm": "sha-256",
        "algorithm": "Ed25519",
        "public_key": "MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU"
      }
    }
  ]
}
```

### 7.2.4 Create JCS version of entire JSON object

Use the result of the previous step as input to the canonicalization process
described in JCS [IETF RFC 8785]. When applied to the example in 7.2.3, the
following JSON object should be generated:

```
{"otherProperties":["home","food"],"signatures":[{"algorithm":"-- some signing algorithm --","hash_algorithm":"-- some hashing algorithm --","public_key":"-- some public key --","signature":{"algorithm":"Ed25519","hash_algorithm":"sha-256","public_key":"MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU"},"value":"-- some existing digital signature --"}],"statement":"Hello signed world!"}
```

### 7.2.5 Create hash of the JCS version

Using the hashing algorithm defined in the JSS Signature object hash the JCS
version of the full JSON object. When applied to the example in 7.2.4 and using
the sha-256 algorithm, the following hash (in hex) should be generated:

```
d77acfa79aa675f22d4517f534df7919f2fdf9821b73f03e97140067abce9ab9
```

### 7.2.6 Sign hash

Sign the hash from step 7.2.5 using the algorithm defined in the signature
object (Ed25519) and then base64URL.encode it. When applied to the example from
7.2.5, the signature value should look like:

```
b_7Xu5qmpCGx7f0VneTUuFxGOcck3Fk5duNlRzDo-ifG1faoK3-xV_xc62DyHnPIgAGDbbSOlKf9kaxs_qAjBA
```

### 7.2.7 Assemble JSON object with signature

If there were existing signatures, add them back to the object at the start of
the list. Then append the new b64 digital signature from step 7.2.6 to the
signature value property of the nested/countersigned JSS Signature object.
Based on the example, the object should look like:

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "public_key": "-- some public key --",
      "value": "-- some existing digital signature --",
      "signature": {
        "hash_algorithm": "sha-256",
        "algorithm": "Ed25519",
        "public_key": "MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU",
        "value": "b_7Xu5qmpCGx7f0VneTUuFxGOcck3Fk5duNlRzDo-ifG1faoK3-xV_xc62DyHnPIgAGDbbSOlKf9kaxs_qAjBA"
      }
    }
  ]
}
```

# 8 Detailed Verification Operation

The examples in this section feature Ed25519 keys as defined in Appendix B.

NOTE: The following examples use the Ed25519 algorithm for illustrative purposes. Implementations **SHOULD** use quantum safe options.

## 8.1 Signature Validation

The following subsections describe how JSON objects signed according to the JSS
specification can be validated.

### 8.1.1 Parse the signed JSON object

Parse the JSON object that was signed by JSS. If the parsing is unsuccessful,
the operation **MUST** cause a compliant implementation to terminate processing
and return an error indication.

Note: JSON tools usually by default remove whitespace. In addition, the original
ordering of properties may not always be honored. However, none of this has
(due to the canonicalization performed by JCS), any impact on the result.

To illustrate the subsequent operations the signed JSON object featured in
section 7.1.7 is used as an example and copied here, but with only one of the
JSS Signature objects. If more than one JSS Signature object was found,
identify the signature that needs to be verified and remove and disregard the
others.

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "sha-256",
      "algorithm": "Ed25519",
      "public_key": "MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU",
      "value": "F1Sj4VcZlSt5GO3Bcu4izpCklj9DbKDNvc2Trpdznfqgv9HMPUGVtefMsHfTqel-dN20lUXsdoeD8PpVr1ssCg"
    }
  ]
}
```

### 8.1.2 Capture and remove the digital signature

After successfully parsing the JSON object, retrieve the digital signature from
the value property in the designated JSON top-level property holding the
signature object. If the property is missing or its argument is not a JSS
Signature object, the operation **MUST** cause a compliant implementation to
terminate processing and return an error indication. When applied to the
example in 8.1.1, the following Digital Signature should be found:

```
F1Sj4VcZlSt5GO3Bcu4izpCklj9DbKDNvc2Trpdznfqgv9HMPUGVtefMsHfTqel-dN20lUXsdoeD8PpVr1ssCg
```

This will leave the following object:

```
{
  "statement": "Hello signed world!",
  "otherProperties": [
    "home",
    "food"
  ],
  "signatures": [
    {
      "hash_algorithm": "sha-256",
      "algorithm": "Ed25519",
      "public_key": "MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU"
    }
  ]
}
```

### 8.1.3 Parse or fetch the public key

Parse the Public Key from 8.1.2 or fetch it from a trusted source. When applied
to the example in 8.1.2, the following public key should be generated:

```
[185 179 40 156 23 212 246 155 200 110 62 81 10 37 144 44 62 57 38 251 186 152 170 254 145 5 227 190 53 188 102 69]
```

In PEM form, this should look like the value found in **public_key** property
and in appendix B.1.

### 8.1.4 Canonicalize the JSON object

Use the resulting object from 8.1.2 as input to the canonicalization process
described in JCS [IETF RFC 8785]. When applied to the example in 8.1.2, the
following object should be generated:

```
{"otherProperties":["home","food"],"signatures":[{"algorithm":"Ed25519","hash_algorithm":"sha-256","public_key":"MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU"}],"statement":"Hello signed world!"}
```

### 8.1.5 Create hash of the JCS version

Using the hashing algorithm defined in the JSS Signature object hash the JCS
version of the full JSON object. When applied to the example in 8.1.4 and using
the sha-256 algorithm, the following hash (in hex) should be generated:

```
e005ae762a01723f3b58fa8edb2b2cc3b126ca087077189072cfd9a27e6079d5
```

### 8.1.6 Validate the digital signature

After parsing the public key and creating a hash of the JCS version of the JSON
object, the signature must be validated based on the defined signature
algorithm in the JSS Signature object. The actual validation procedure is not
specified here because it is covered by [IETF RFC 7515]. This process also
depends on application-specific policies like:

 - Accepted signature algorithms
 - Public key lookup methods

If the validation process for some reason fails, the operation **MUST** cause a
compliant implementation to terminate processing and return an error
indication.

# 9 Security Considerations

This specification inherits all the security considerations of JWS [IETF RFC
7515] and JCS [IETF RFC 8785]. Note that strict conformance to I-JSON [IETF RFC
7493] is **REQUIRED**.

In similarity to any other signature specification, it is crucial that
signatures are verified before acting on the signed payload.

However, poorly tested software components may also introduce security issues.
Consider the following JSON example:

```
{
  "fromAccount": "1234",
  "toAccount": "4567",
  "amount": {
    "value": 100,
    "currency":"USD"
  }
}
```

A non-compliant JCS implementation could return

```
{"amount":{},"fromAccount":"1234","toAccount":"4567"}
```

giving an attacker the ability to change "amount" to whatever it wants. Note
though that this attack presumes that the consumer and producer use
implementations broken in the same way, otherwise the signature would not
validate.

For usage in a wider community, the name of the designated signature property
becomes a critical factor that **MUST** be documented and communicated.

# Appendix A. Open-Source Implementations

Due to the simplicity of this specification, there is hardly a need for specific
support software. However, JCS which is (at the time of writing), a relatively
new design, may be fetched as a separate component for multiple platforms. The
following open-source implementations have been verified to be compatible with
JCS:

 - JavaScript: <https://www.npmjs.com/package/canonicalize>
 - Java: <https://mvnrepository.com/artifact/io.github.erdtman/java-json-canonicalization>
 - Go: <https://github.com/gowebpki/jcs>
 - .NET/C#: <https://github.com/cyberphone/json-canonicalization/tree/master/dotnet>
 - Python: <https://github.com/cyberphone/json-canonicalization/tree/master/python3>

# Appendix B. Ed25519 Keys for Examples

This appendix contains the public and private keys that are used in the various
examples in this specification and are included here to assist with
replication, testing, and verification.

NOTE: The following keys use the Ed25519 algorithm for illustrative purposes.
Implementations **SHOULD** use quantum safe options.

## B.1 Ed25519 Public Key

This is a PEM holding a Ed25519 public key.

```
-----BEGIN PUBLIC KEY-----
MCowBQYDK2VwAyEAubMonBfU9pvIbj5RCiWQLD45Jvu6mKr+kQXjvjW8ZkU=
-----END PUBLIC KEY-----
```

## B.2 Ed25519 Private Key

This is a PEM holding a Ed25519 private key.

```
-----BEGIN PRIVATE KEY-----
MC4CAQAwBQYDK2VwBCIEIDnZ5bPmXnB3OfU/5fNVfxfr7iRZtqH06AZ3b6c6liTL
-----END PRIVATE KEY-----
```

# Appendix C. JSS Application Notes

The following example shows how countersigned signatures can be used.

## C.1 Countersigned Signature Example

Using the countersigned signatures method as defined in 7.2 of this
specification organizations can countersign a JSON document that has a JSS
digital signature. Consider the following JSON object showing an imaginary real
estate business record.

```
{
  "gps": [38.89768255588178, -77.03658644893932],
  "object": {
    "type": "house",
    "price": "$635,000"
  },
  "role": "buyer",
  "name": "John Smith",
  "timeStamp": "2020-11-08T13:56:08Z",
  "signatures": [{ -- some JSS signature object -- }]
}
```

Adding a notary signature on top of this would be performed as follows:

```
{
  "attesting": {
    "gps": [38.89768255588178, -77.03658644893932],
    "object": {
      "type": "house",
      "price": "$635,000"
    },
  },
  "signatures": [
    {
      "role": "buyer",
      "name": "John Smith",
      "timeStamp": "2023-01-30T13:56:08Z",
      "hash_algorithm": "-- some hashing algorithm --",
      "algorithm": "-- some signing algorithm --",
      "value": "-- some digital signature –"
      "signature": {
        "role": "notary",
        "name": "Carol Lombardi-Jones",
        "timeStamp": "2023-01-30T13:58:42Z",
        "hash_algorithm": "-- some hashing algorithm --",
        "algorithm": "-- some signing algorithm --",
        "value": " -- The notary's digital signature -- "
      }
    }
  ]
}
```

The design of this method ensures that the notary's signature signs not only the
notary data, but the buyer's data and signature as well. In most cases this way
of adding signatures is advantageous since it maintains the actual order of
signing events which also cannot be tampered with without invalidating the
outermost signature. This method would also allow additional participants like
the city/county recorder to also sign this entire transaction forming a
signature chain.
