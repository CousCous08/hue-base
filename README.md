# Hue: The Decentralized Music Streamer 
# Repository Links:
[frontend](https://github.com/CousCous08/hue-frontend) 

[backend](https://github.com/CousCous08/hue-backend) 

[smart contract](https://github.com/CousCous08/hue-smart-contract)

Take a look at hue.pdf for motivation, design overview, and results!

# Motivation:
	
What is the point of a music distributor? To think seriously, in todays’ age of digital distribution, the need for any middle-man distributor has been long erased. Back when CDs and vinyls were the primary means of distributing music, music distributors were valuable for providing artists’ the benefits of scale. Yet, for unexplainable reasons beyond profit and industry tradition, they still exist and thrive to this day. If you aim to become a publishing artist and access streaming platforms with the majority of market share such as Spotify or Apple Music, you still need to go through a distributor. What do they do? They standardize the data, manage publication submission, and ensure royalty payment. The first two are easily manageable by any competent person or algorithm, and already have alternative solutions that do not require publishers (SoundCloud, Bandcamp, etc.). However, the lattermost is the concern of this project, as transparency of streaming numbers and the associated royalty payments is very poor within the industry. My proposed solution: a music streamer with a blockchain-based backend, allowing for full transparency on streaming counts and royalty payments. This, and an otherwise centralized application for a similar user experience to current market standards combine to make up Hue.


In the highest level overview, Hue is made up of two parts: a regular frontend, and a backend that encapsulates connections to Walrus, a decentralized file storage system, Sui, a Directed Acylic Graph (augmentation of blockchain), as well as a regular SQL connection for caching and efficiency. Whenever an artist wants to publish their audio file, it is formatted with various metadata and sent to Hue’s own backend point which is an Express.js server. This server then goes through 3 different connections. First, it connects to a Walrus publisher, which will store the blob and return an ID that can be used to retrieve the data. Then, the server stores this ID along with other metadata within an on-chain representation of the track object, which will keep track of stream count and store the royalty payments. After, all of the data for this track is stored in a centralized SQL so each user doesn’t need to send a read operation to the blockchain/DAG for track information. Finally, the backend sends back a successful upload message to the artist as well as the address of the track object on the blockchain, so they can independently verify information. The listener flow is relatively similar. Except, instead of using a Walrus publisher, they connect to a Walrus aggregator which fetches blob data based off of ID which is then fed to the client for playability. 

 
Similarly to NFS and RPC, the distributed aspect of this system is abstracted away from the user. This mantra drives the design behind Hue. No listener on Hue should feel the effects of the blockchain, but at the same time they should all be able to independently verify each stream/transaction. Essentially, it should feel like every other music streamer, except with accessibility to transparency that empowers artists and users alike. 
