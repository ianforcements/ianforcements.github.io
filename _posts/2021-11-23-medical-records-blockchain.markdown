---
layout: single
title: "Some thoughts on the idea of blockchainized Medical Records"
date: 2022-03-14 01:00:00 +100
last_modified_at:
categories:
tags: cryptosnark medical-records blockchain privacy
---
I'm writing the first draft in a hospital waiting room. I was doomscrolling twitter and saw yet another post along the lines of "NFTs will be used for your medical records in future! It will be good!"

This won't happen and if it did it would not be good. Here's why.

There are certain requirements sensible people have for medical records and the systems which maintain them. These include, but are not limited to:
1. mutability
2. privacy

By 'mutability' I mean that an inaccurate diagnosis may need to be amended at a later date. It may not be enough to post an update to correct your status, it may in fact be desirable to expunge a record entirely. This is not possible under a blockchain system, and in fact the opposite is true - the inability to expunge a record is touted as a benefit of blockchain technologies.

By 'privacy' I mean the idea that if you have an embarrassing medical condition you do not want the entire internet and all of humanity, born and as yet unborn, from this day unto the last day, for all time, to know about it. No sensible person thinks that this is a good feature. If your medical records were hosted on the blockchain, this would be such a feature; it would be bad.

The medical condition does not need to be embarrassing for you to have a right to privacy with respect to it. People who are vulnerable to targeting by governments or powerful entities probably don't want their peanut allergy to be public knowledge. People do not want to be discriminated against by employers or insurers on the basis of medical history those employers or insurers have no right to know. The ostensible goal of cryptosystems is to protect the little guy against powerful interests, and having medical records be public works against this goal.

"But you don't understand!" the cryptobros might protest, "we're not keeping your entire record on the blockchain, just an identifier which can be used to tie you to your records, which are kept elsewhere!"

This ties into a similar blockchain fallacy, that of "blockchain solves identity", which deserves another post. For now let's assume blockchain does solve identity problems and work on the rest of this bad idea.

If your blockchain system is merely a pointer to a data store held elsewhere, then what is the point of your blockchain system? You haven't decentralised your system, because the centralised data store still exists. Your system is not less fragile, because it now contains another component in a chain of components, all of which must function in order for the system as a whole to work; if anything your system is now _more_ fragile. What has your blockchain added to the system?

The added feature of inserting a blockchain layer is that your system is open to multiple participants. You don't need to go to the Medical Authority to create a medical record - you can create one yourself! You don't need to go to the Medical Authority to read a medical record, you can read the blockchain yourself! Both of these are bad.

The latter - anyone can read the blockchain - is already addressed above when I wrote about privacy. It's a bad outcome.

The former - that you can create your own medical records - is also bad, actually. It's bad because if you can create your own medical record, than so can I. I can make your medical record too. I can put your name on it; I can put anything I like on it. I can say you have any disease I like.

My record won't be signed with your private key, but it will have your name on it and for a third party to evaluate which record belongs to the real you, they will need to establish which key belongs to the real you. This requires them to be in touch with someone who claims to be you, who can sign a message with the same key, **but all that will prove is that the same key signed the record and the confirmation message**.

Another example is if I have a medical record that I don't like. I might decide to create a new one, with a new key, full of all my medical history except the stuff I don't like. I have the key to this record, so I can confirm if if anyone asks. If anyone wants to know about that other account with the same name, I can just declare that it's a sybil record produced by someone who wants to discredit me. How would you prove me wrong?

Consider the rash of art theft and duplicate listings on NFT marketplaces as an example. The only solution is verfied collections by NFT marketplaces, making those marketplaces the authoritative source of truth in those ecosystems. Similarly for medical records you will ultimately need an authority to mediate the blockchain records to confirm that the records or keys are tied to who they claim to be. **You cannot have a blockchain that relates to real-world truths absent an arbiter of those truths.** 

There is one potential upside to this idea that I can think of. If your medical records are so readily and publicly available, you can easily take them with you when moving to a new doctor or moving to a new country. This is an advantage. It is however the **only** advantage, and you have to ask yourself if it's really worth the enormous downsides.

