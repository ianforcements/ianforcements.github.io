---
layout: single
title: "NFTs are worse than a broom closet"
date: 2021-11-14 01:00:00 +100
last_modified_at:
categories:
tags: nft cryptocurrency mona_lisa broom_closet
---
I'm assuming for this article that you've heard of NFTs, because it's 2021 and we've all been starved of the outside world for some time.

A lot has been made of NFTs as the future of art, or something. A lot else has been made of them being an absurd scam. If you haven't read it already, this tongue-in-cheek primer is originally attributed to a user on Tumblr called 'QueerSamus', in a post I can't find anymore (admittedly I didn't look too hard):

>Imagine you go up to where the Mona Lisa is and say “I’d like to own this” and someone walking around says “give me $65 million and I’ll burn an unspecified amount of Amazon rainforest to give you this bill of sale”. So you pay him and he says “here’s your receipt, thank you for your purchase”. And right away he goes to an unmarked supply closet in the back of the museum and keeps a handmade label there, behind the brooms, that says “the smooth monkey is currently the property of Jacobgalapagos”. So if someone wants to know whose it is, they would have to find this specific cabinet in this specific hallway and look behind the right brooms.
>
>Then you say “can I take the Mona Lisa home now?” and he replies “oh god no, are you stupid, you only bought the receipt that says you own it, you didn’t buy the Mona Lisa itself, you can’t take the actual plain monkey, you idiot. But you can take this.” And he gives you a replica printed on a cardboard tube of the kind sold in the gift store. Also, the person selling you the sales receipt has never owned the Mona Lisa.
>
>Unfortunately, if this doesn’t seem to make sense nor does it seem like any logical person would be satisfied with this exchange, then you’ve got it exactly right.

Of course, there's also an NFT project that'll gladly sell you links to procedurally generated mona lisas, [because why not.](https://www.monasnft.com/)

Satisfying as it is to read, I wanted to verify this for myself. Follow along if you like!

### We set sail on the OpenSeas

Our adventure starts at the OpenSea search bar. I suppose it's possible that readers in the far future may not know what OpenSea is, but in 2021 it's the largest marketplace for NFTs in the world.

[Here is a link](https://opensea.io/assets?search[query]=steve%20aoki%20fighting%20gravity) to the search results for the terms 'steve aoki fighting gravity', I know NFTs are forever but I'll include a screenshot here just in case this blog entry happens to last more forever.
![broomcloset_1](../assets/images/broomcloset_1.png)
The first thing you might notice is that there's several of the same thing listed. Several dozens actually, if you click through and scroll through the results. They just keep going! Steve Aoki is a prolific artist[^1]. 

![broomcloset_2](../assets/images/broomcloset_2.png)

This highlights the first problem with NFTs, you don't have any protection against the same thing being minted arbitrarily many times, even on the same platform! This same piece could be minted on superrare, hic et nunc[^2], et cetera, etc. &c. There is **NO GUARANTEE OF UNIQUENESS**. This actually isn't what I'm driving at with this piece, it's just a happy coincidence.

If we click on one of these pieces, let's sayyy [this one](https://opensea.io/assets/0x01ba93514e5eb642ec63e95ef7787b0edd403add/755), we'll be taken to the OpenSea listing for that NFT. This page will show the piece along with various metadata.

![broomcloset_3](../assets/images/broomcloset_3.png)

Scroll down to check out the transaction history. There's links you can click to check out the transaction on-chain

The most recent transaction, as of this writing, is linked [here](https://etherscan.io/tx/0x421ec12f989a227677ebdf2997e35e7f4eb96533a4013b3bf878b9281fcf9312)

![broomcloset_4](../assets/images/broomcloset_4.png)

This is the transaction data as recorded on the ethereum blockchain. We are now in the broom closet. We can dig further.

Scroll down until you see the 'transaction action' section. The token ID (755) identifies this particular NFT with respect to the smart contract that controls it.

![broomcloset_5](../assets/images/broomcloset_5.png)

Click the 'token ID' [link](https://etherscan.io/token/0x01ba93514e5eb642ec63e95ef7787b0edd403add?a=755) to go to the token itself. We've now found the label behind the brooms in the broom closet. We can see the address of the current owner, and the transaction history shows the previous owners.

Nice, but what does the owner actually _own?_ We can dig further. Click on the 'Contract' tab.

![broomcloset_6](../assets/images/broomcloset_6.png)

There is a lot here, but `TokenURI` is of interest to us. If you click on it you're confronted with an input field. What to input?  This is basically a query of the data held by the smart contract, and it has multiple tokens. The token ID in this case is 755, and that's what we need to enter.

![broomcloset_7](../assets/images/broomcloset_7.png)

The query returns a URI pointing to a server on the [normie boomer internet.](https://client-metadata.ether.cards/api/aoki/FightingGravity/48)

Click through and you'll see a JSON response containing various data. One of those is `Original_Art_Url`, which is an URL to yet another [boomer internet server](https://ether-cards.mypinata.cloud/ipfs/QmQeHy7fqx38m3fvNu1DeVhfvzN2rLygg3NzwhL5XWnFJ9/10/10_Fighting_Gravity.mp4).

![broomcloset_8](../assets/images/broomcloset_8.png)

In summary, what the purchaser has purchased is a link to a JSON which links to a .mp4.

![broomcloset_9](../assets/images/broomcloset_9.png)

Remember the dozens of identical listings in the search results up top? If you care to click any of those and follow the breadcrumbs, this is where all of them end up. 

So to summarize what we've learned:
1. Yes, you are just buying a note on a registry somewhere. The Broom closet analogy is good so far.
2. Nothing is stopping the artist from selling the same exact note multiple times! To extend the broom closet analogy, the salesman might have an entire wall of labels, each of them proudly stating that someone uniquely and canonically owns the mona lisa.
3. All of this depends on boomer internet infrastructure. If either of the two normiespace hops (ether.cards or mypinata.cloud) go down, then you cannot verify your NFT! To revisit the broom closet analogy again - you don't have a label that says you own the mona lisa - you have a label that points you to a second broom closet, that points you to another broom closet, that finally points you to the mona lisa. If either of those broom closets are locked, you're in trouble.
4. The last two hops aren't on the blockchain, so the blockchain promises don't apply. Specifically these are records that are very much mutable, and mutable by people who _aren't you_, the server admin of ether.cards can redirect your NFT to rick astley if they so chose, and you would have no recourse and no proof that your NFT had ever pointed to something different.

I started with the intention of clarifying whether QueerSamus' absurd summary was justified, and I'm left with the conclusion that it wasn't absurd enough.

### what about IPFS though

Some readers may be aware of IPFS storage, and there are some NFT projects using this! If you find a token URI with a link like so:

<ipfs://QmWh6HrDmgWQZaCzUckywNNJNdHa7uSgiNzYUrmc9xzfHz/9187>

![broomcloset_10](../assets/images/broomcloset_10.png)

then you're working with an asset stored on IPFS. At the time of writing browser integration with IPFS is patchy, but cloudflare have an interface you can use! Simply replace ipfs:// in the above URL with 

<https://cloudflare-ipfs.com/ipfs/>

as in, <https://cloudflare-ipfs.com/ipfs/QmWh6HrDmgWQZaCzUckywNNJNdHa7uSgiNzYUrmc9xzfHz/9187>

and then go from there.

IPFS has an advantage over the normie internet in that your file is distributed peer-to-peer, which will purportedly mitigate the risk that your file host goes down. Additionally IPFS files are meant to be immutable.

There are some observations to be made about IPFS storage:

Firstly, IPFS is not a blockchain, though it is peer-to-peer and it is often implemented adjacent to blockchains. This is important to keep in mind.

IPFS in practice is not as bulletproof or antifragile as you might expect. The twitter account @CheckMyNft was at one point performing random checks on the availability of IPFS-stored NFT assets. The results were bad.

<https://twitter.com/CheckMyNFT/status/1371960028765245440?s=20>

![broomcloset_11](../assets/images/broomcloset_11.png)

Will this get better? Maybe. IPFS makes no guarantee that your files will be available permanently. Files will decay according to the whims of the protocol. If you want your files to stay, you need to either pin them on your own IPFS node (be your own datacentre!) or pay someone else to do that on their node.

IPFS does not mitigate against your smart contract being edited without your knowledge. This happened to the 'Raccoon Secret Society', (a collection of raccoon avatars, naturally) which you can read about here: <https://metaversal.banklesshq.com/p/racoon-rugged-society>

In summary, what happened was that the smart contracts managing the NFT data were edited to change the URL that every NFT pointed to. Each raccoon avatar was replaced with a pile of ash and bones.

Some time later the whole thing was revealed to be a very avant-garde artistic stunt and now the raccoons have been reborn as zombies! Apparently this demonstration of the impermanence and mutability of NFTs is Good, Actually, and not a problem at all for the people who shelled out money for these things.

It's worth noting that a purported selling point of NFTs is their permanence and immutability, both 'secured by the blockchain'.

### ok but what about filecoin and arweave

Filecoin is built on IPFS, and purports to solve the IPFS decay problem by incentivising miners to keep files available. Arweave appears to be similar. Both are interesting projects although neither appear to be in use very much for NFTs.

Why not? My intuition is that spending money for storage is really not crucial to the NFT business model, regardless of what this means for buyers.

A proper dive into both requires a dedicated article, so I'll save that for another time. The TLDR is: I'm really, really skeptical that the economics of these systems are gonna result in permanent, cheap, extra-available storage for uninteresting artworks at the kind of scale that would make them meaningfully useful.

[^1]: _I'd never heard of Steve Aoki actually, some googling tells me he's a musician of some kind. His website links to a few NFT collections on NiftyGateway, but nothing on OpenSea? His OpenSea profile is 'verified' though? I'm sure it's all legit._
[^2]: _hic et nunc went offline sometime between the first draft of this article and publication, I have things to say about that but that also deserves a dedicated post, so that's for another time_

