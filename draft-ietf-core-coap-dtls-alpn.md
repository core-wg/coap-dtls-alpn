---
title: "ALPN ID Specification for CoAP over DTLS "
abbrev: "CoRE ALPN"
category: std

docname: draft-ietf-core-coap-dtls-alpn-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Web and Internet Transport"
workgroup: "Constrained RESTful Environments"
keyword:
 - CoRE
 - CoAP
 - SVCB
 - DTLS
 - ALPN
venue:
    group: "Constrained RESTful Environments"
    type: "Working Group"
    mail: "core@ietf.org"
    arch: "https://mailarchive.ietf.org/arch/browse/core/"
    github: "anr-bmbf-pivot/draft-ietf-core-coap-dtls-alpn"
    latest: "https://anr-bmbf-pivot.github.io/draft-ietf-core-coap-dtls-alpn/draft-ietf-core-coap-dtls-alpn.html"

author:
 -  fullname: Martine Sophie Lenders
    org: TUD Dresden University of Technology
    abbrev: TU Dresden
    street: Helmholtzstr. 10
    city: Dresden
    code: D-01069
    country: Germany
    email: martine.lenders@tu-dresden.de
 -  name: Christian Amsüss
    email: christian@amsuess.com
 -  fullname: Thomas C. Schmidt
    organization: HAW Hamburg
    street: Berliner Tor 7
    city: Hamburg
    code: D-20099
    country: Germany
    email: t.schmidt@haw-hamburg.de
 -  name: Matthias Wählisch
    org: TUD Dresden University of Technology & Barkhausen Institut
    abbrev: TU Dresden & Barkhausen Institut
    street: Helmholtzstr. 10
    city: Dresden
    code: D-01069
    country: Germany
    email: m.waehlisch@tu-dresden.de

normative:
  RFC7252: coap
  RFC7301: alpn
  RFC9460: svcb

informative:
  RFC8323: coap-tcp
  I-D.ietf-core-dns-over-coap: doc
  RFC4944: 6lo

--- abstract

This document specifies an Application-Layer Protocol Negotiation (ALPN) ID for
transport-layer-secured CoAP services.

--- middle

# Introduction

Application-Layer Protocol Negotiation (ALPN) enable communicating parties to agree on an application-layer protocol during a Transport Layer Security (TLS) handshake using an ALPN ID.
This ALPN ID can be discovered for services as part of Service Bindings (SVCB) via the DNS, using SVCB resource records with the "alpn" Service Parameter Keys.
As an example, this information can be obtained as part of the discovery of DNS over CoAP (DoC) servers (see {{-doc}}) that deploy TLS or DTLS to secure their messages.
This document specifies an ALPN ID for CoAP services that are secured by transport security using DTLS.
An ALPN ID for CoAP service secured by TLS has already been specified in {{-coap-tcp}}.

# Application-Layer Protocol Negotiation (ALPN) IDs

For CoAP over TLS an ALPN ID was defined as "coaps" in {{-coap-tcp}}.
As it is not advisable to re-use the same ALPN ID for a different transport layer, an ALPN for
CoAP over DTLS is registered in {{iana}}.

ALPN ID values have variable length.
Here, a short value ("co") is allocated for CoAP over DTLS, as this can avoid fragmentation of Client Hello and Server Hello messages in constrained networks with link-layer fragmentation, such as 6LoWPAN {{-6lo}}.

To discover CoAP services that secure their messages with TLS or DTLS, ALPN IDs "coaps" and "co" can be used respectively in
the same manner as for any other service secured with transport layer security, as
described in {{-svcb}}.
Other authentication mechanisms are currently out of scope.

# Security Considerations

Any security considerations on ALPN (see {{-alpn}}) and SVCB resource records (see {{-svcb}}), also
apply to this document.

# IANA Considerations {#iana}

## TLS ALPN for CoAP

The following entry has been added to the "TLS Application-Layer Protocol Negotiation (ALPN) Protocol IDs" registry, which is part of the "Transport Layer Security (TLS) Extensions" group.

* Protocol: CoAP (over DTLS)
* Identification sequence: 0x63 0x6f ("co")
* Reference: {{-coap}} and \[this document\]

Note that {{-coap}} does not define the use of the ALPN TLS extension during the DTLS connection handshake.
This document does not change this behavior, and thus does not establish any rules like those in {{Section 8.2 of -coap-tcp}}.


--- back

# Change Log


# Acknowledgments
{:unnumbered}

We like to thank Rich Salz for the expert review on the "co" ALPN ID allocation.
We also like to thank Mohamed Boucadair and Ben Schwartz for their early review before WG adoption
of this draft.
