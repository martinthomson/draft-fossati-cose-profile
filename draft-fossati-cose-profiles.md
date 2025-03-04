---

title: "COSE Profiles"
abbrev: "COSE Profiles"
category: std

docname: draft-fossati-cose-profiles-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Security"
workgroup: "CBOR Object Signing and Encryption"
keyword:
 - COSE
 - profiling
venue:
  group: "CBOR Object Signing and Encryption"
  type: "Working Group"
  mail: "cose@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/cose/"
  github: "thomas-fossati/draft-fossati-cose-profile"
  latest: "https://thomas-fossati.github.io/draft-fossati-cose-profile/draft-fossati-cose-profiles.html"

author:
 -
    fullname: Thomas Fossati
    organization: Arm Limited
    email: thomas.fossati@arm.com
 -
    fullname: Henk Birkholz
    organization: Fraunhofer SIT
    email: henk.birkholz@sit.fraunhofer.de

normative:
  RFC8610: cddl
  STD66:
    -: uri
    =: RFC3986
  STD96:
    -: cose
    =: RFC9052
  I-D.ietf-core-href: cri
  RFC4122: uuid
  RFC9090: oid

informative:

entity:
  SELF: "RFCthis"

--- abstract

This document lays a set of rules for how to define COSE profiles.

--- middle

# Introduction

This document lays a set of rules for how to define COSE profiles.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Rules

A COSE profile:

* MUST be specified in a document
* MUST NOT change the syntax or semantics of any already defined
  header attribute
  * but does allow restricting their values
* MAY define new header attributes
  * if so, it MUST provide their definition in the same document
* MUST use CDDL {{-cddl}} to fully specify the syntax rules for the profile
* MUST use the `cose-profile` header attribute in the protected header
  * The value of `cose-profile` MUST be global unique via:
    * IANA registry
    * using an OID {{-oid}}, URI {{-uri}} or CRI {{-cri}}
    * using a UUID {{-uuid}}
  * The chosen value SHOULD be appropriate for the intended usage scope (e.g., a small value when used in constrained node environments)
* MAY define its own CBOR tag[^tag]
* SHOULD define its complementary media-type and content-format

[^tag]: -- get more specific here (in later iterations)

# COSE profile header parameter

~~~ cddl
COSE-profile = registered-profile / oid-profile / uri-profile
             / cri-profile / uuid-profile
registered-profile = int
oid-profile = oid ; tagged
uri-profile = ~uri ; unwrapped -- any tstr is a uri
cri-profile = cri
uuid-profile = uuid ; naked bstr is a UUID

uuid = bstr .size 16

; imported from RFC 9090
oid = #6.111(bstr)
; import from CRI spec when ready
cri = [*any]
~~~


# Security Considerations

TODO Security

# IANA Considerations
This document defines a header parameter "cose-profile" that needs to
be registered in the "COSE Header Parameters" registry.

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
