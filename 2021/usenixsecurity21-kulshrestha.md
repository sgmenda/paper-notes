# Identifying Harmful Media in End-to-End Encrypted Communication: Efficient Private Membership Computation

> Anunay Kulshrestha and Jonathan Mayer. "Identifying Harmful Media in End-to-End Encrypted Communication: Efficient Private Membership Computation.". In 30th USENIX Security Symposium (USENIX Security 21). USENIX Association, 2021.

Link to paper: https://www.usenix.org/conference/usenixsecurity21/presentation/kulshrestha

**Disclaimer.** All mistakes are mine, not those of the authors.

I love this paper! It starts by taking on the thorny problem of formalizing CSAM matching and then presents and evaluates a bunch of candidate constructions, including a wonderful discussion of existing (open) fuzzy hashes.

First, the paper formalizes the problem of CSAM matching using two attributes:

* *client privacy*: we want to prevent the server from learning client's media or the fuzzy hash of client's media; and
* *server privacy*: we want to prevent the server from learning the fuzzy hash set it is comparing against.

They also identify the dichotomy about:

* *server-revealing*: where the server learns if the client's media was in the fuzzy hash set (revealing information about the fuzzy hash of client's media and client's media to the server); versus
* *client-revealing*: where the client learns if the client's media was in the fuzzy hash set (revealing information about the fuzzy hash set to the client).

Furthermore, they observe that both these cases can be useful. For instance, they point out that we might prefer server-revealing in the case of CSAM and client-revealing constructions in the case of disinformation.

Omg, they also mention ethical implications of deploying such tech by pointing out that, for instance, WeChat has used this tech for censorship as noticed by the Citizen Lab folks Knockel, Ruan, and Crete-Nishihata [at FOCI 2018](https://www.usenix.org/conference/foci18/presentation/knockel). I highly recommend checking out section "2.3 Limitations".

> We emphatically *do not* take a position on whether E2EE
> services should adopt the constructions we propose, especially
> given the significant risks to user privacy and security, the
> challenge for international human rights, and the feasibility of
> circumvention.

^😍

## Constructions

* First, they notice that existing constructions using fuzzy hashes aren't very accurate. I would like to see the histograms that they refer to in Section 4.2 but the supplementary data link seems broken (I emailed the first author with a link to the "let me in" meme so hopefully they fix that.)
* In Section 5, they discuss client-side matching and notice that "cuckoo filters" are practical.
* In Section 6, they throw moar crypto, PIR and MPC and HE, to hide the hash set from the client and letting the server know if there is a match.
* Sections 7-14 are relatively technical and I am not gonna try to summarize them (see the paper.)

## Conclusions

* Section 14 has a bunch of really cool directions, ones that really excite me include media disclosure (fuzzy hashes are fuzzy, so one needs to look at the plaintext to verify that the data is indeed violating the terms, how to do this?) and increasing trust (they mention using Merkle Trees (love 'em) to ensure that the server is not manipulating the set, one can think about more complicated protocols that incorporate this ethos).
* I feel like a good next step would be to create a e2ee messaging service harness and try out these ideas. All these ideas (the ones in this paper, the ones in the traceback paper, etc) seem implementable, so it should be plausible. More precisely, the output would be a spec and a reference implementation for a e2ee messaging service that incorporates a bunch of these ideas.
