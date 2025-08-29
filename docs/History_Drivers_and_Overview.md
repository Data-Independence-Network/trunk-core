# DIN and BD

Overview of the Data Independence Network (DIN) server-side Trunk and Branch stack and of how it is combined with the [Beyond Decentralized](https://github.com/Beyond-Decentralized) (BD) client-side Leaf stack.

## The History of

### Beyond Decentralized

Beyond Decentralized (BD) stack evolved from a small ORM layer meant to run on Google Docs to host [family organizer data](https://github.com/Past-The-War-Earth/Hans_the_Organizator) without placing it on a central server.  As development continued the need for a full blown server running inside a client browser became clear.  It was needed to accommodate minimal server-side costs of sharing only the Repository transaction logs.
A Repository is a way of splitting relational data into Autonomous units that can still be Interconnected: Autonomous Interdependent Repositories (AIR).  It splits the common database Transaction Log into per-Repository Transaction Logs and shares them as Create, Update and Delete requests that are chronologically recorded for a given Repository.

Given the flat nature of the Transaction Logs the idea of using a simple shared file system naturally appeared.  Realizing that Google Docs is a commercial platform that doesn't fit the need of storing confidential family/group data a search across fitting (and grant providing) block chains was initiated.  A small grant was attained from Filecoin and for a period of time development continued with (at least to a certain degree) the eventual intent of running BD on top of NTFS.  However, towards the end of the grant funding it became clear that NTFS wasn't fast enough to serve user needs, mostly due to large blockchain limitations.  This is when the need for a custom server-side technology stack finally solidified.

### Data Independence Network

The idea for a Data Independence Network (DIN) was around as soon as the original Google Docs idea naturally gave way to more appropriate solutions.  It was envisioned to consist of per-metro area cooperative franchises that would independently operate a local network, maintaining data sovereignty (have physical control) over it's community data.  The idea of providing a free platform for storing the encrypted small family/group data was eventually accepted as a solution.  The ideas of running non-geographically rooted interest-based DIN cooperatives and even eventually allowing business interests to join the network with their own infrastructure slowly added to the mix.  This was acceptable since the data storage would still be segregated and only combined (and split back up for separate storage) on User devices.

The idea of making DIN economically feasible manifested itself in a proposed [turbase.org](https://github.com/Data-Independence-Network/turbase.org) platform that would split profits on anonymized profile + originating UI type based advertizing among the network providers and users.  It eventually became clear that any revenue tapping by the framework or any centralization would "defeat the purpose".  Micro-level revenue sharing between interdependent Apps and the shared UI still makes sense to promote further development.

DIN stack originally consisted of a performant distributed no-SQL database for transaction log storage and look-up, a distributed relational database for combined community Repository storage and reporting and a full text search database for lookups of community data.  The idea of a full text search database slowly gave way to the realization that public data could be indexed by large search engines. Since the commitment to a NLNM simulation the rest distributed storage ideas slowly gave way to simpler approaches that would run on small servers, co-hosting the simulation (one per opponent to keep separate the opponent-confidential command and control data), at the same time making the idea of running small/group servers more feasible.  Very recently, after dwindling down to only a distributed relational database (that could be substituted for a SQLite instance in small/family group servers) for the final breakthrough led to the below approach:

## Core Ideas

### Дерево, Очередь, Общая Связанность

Many of the below ideas have been identified and thought through previously but a cohesive approach along with several key new ideas arrived over the course of the last several days.  A key difference vs previous approaches is the final commitment to removal of load balancing third party software and fully focusing on core strength of the previously abstractly considered Tree approach, as well as addition of random-access per-node-dedicated Queues to substitute for a fast no-SQL database and a revival of the Mesh network approach.  The final divinely inspired idea of combining dedicated per-Branch queues with a dedicated per-Trunk queue stitched the entire stack together. 

### Where it fits

The newly arrived at server-side DIN technology stack is most needed for the NLNM simulation as it fulfils Branch access restriction requirements while providing real-time connectivity. In turn the BD stack contributes to data compartmentalization, as well as complete or localized NLNM simulation verification and replay, with and without restricted, per opponent and per-tactical unit data. The full-blown Leaf node server approach is most needed for Phase 3 of the NLNM simulation, when each Leaf node will be independently (and collaboratively across it's immediate and larger units) augmenting the behavior of the simulation participants to ensure rule-based enforcement of NLNM principles without compromising tactical goals.

### Core concepts

Data Independence Network code is the backend for Beyond Decentralized.  It's technology is based on 3 main concepts:

1.  Deploying servers in Trunk -> Branch -> Leaf node configuration (with Leaf technology provided by Beyond Decentralized).

2.  Utilizing dedicated per-Branch queues for read and write requests.  Utilizing a dedicated per-Trunk queue for cross-Trunk communication.  Continuously combining Trunk and Branch queues for final data verification and on-Trunk persistence.

3.  Offloading data synchronization between Leaves to a Leaf-to-Leaf peer-to-peer network, when the sharing strategy for the Repository allows it.

### Reasons

Traditional and primary targets for DIN deployments are single-binary, Trunk+Branch, small family/group servers that must run at minimal expense.  DIN is also intended for public-maintained metro-area wide networks, and needs to minimize hardware and maintenance expenses for (presumably non-profit) organizations that would voluntarily participate in such networks. The combination of the techniques above fits the Repository-based storage model utilized by the BD Leaf node technology stack and allows for optimal performance characteristics needed for DIN use cases.

## General overview

### Processing on Leaf nodes

Beyond Decentralized Leaf nodes are full-blown servers that run in-browser and communicate with each other via Transaction Logs that are shared between Leaves.  Thus, for either read or write operations no processing needs to happen on the server infrastructure, it simply needs to facilitate communication between Leaves.  Leaves exchange data directly between each other whenever possible.
The driver of processing all data on Leave nodes was ownership of data by users and resulting performance needs to minimize server costs to users.

### Leave mesh net

The idea of a mesh net of leaves was around since the invention of Repositories because it virtually eliminates data sharing costs between nodes but the technical limitations of having to maintain a dedicated lookup server prevented initial commitment to this approach.

### Leaves assigned to Branches

DIN Users (will) have per Trunk (the hub of a DIN network) accounts.  Each account is configured to connect to a single Branch node, though in eventual expansion beyond NLNM simulations will be transferrable to other Branches if needed for load balancing (or for more dense Branch data caching).  This allows to channel all requests for a given account via one Branch node and allows for stable and secure routing patterns.

The driver of a Tree topology with Leaves assigned to Branches was the Votecube application which needed efficient aggregation of poll results and back propagation of poll summaries to Leaf nodes (as well as the ability to prevent DDOS attacks during critical polls).  Sharing aggregated poll data within and between Trees is both very efficient and secure.
Subsequently a realization came that DIN and BD and a perfect fit for a hypothesized future outer-space security organization, which was envisioned to span multiple (and eventually all) governments and have data compartmentalization across Groups in the same governmental entity (for more common Solar System responsibilities, to begin with asteroid security, and separately more controlled for other tasks including research beyond the Solar System).

Assigning accounts to specific Trunks allows to physically isolate data for per-country Groups of users, and as is apparent now eventual assignment of accounts to intermediate Trunch+Branch nodes allows to physically isolate data between groups with different levels of data security.

Pure Branch nodes act as data sharing funnels and allow spreading of data synchronization load between multiple nodes.  Branch nodes also cache data (Transaction Log Entries) that is needed by their assigned accounts and maintain queues with recent data for fast lookup.

Trunk nodes aggregate the data from their Branches and communicate with other Trunks to synchronize data that spans multiple Trunks (where accounts from multiple networks participate in the same Repositories or interdependent Repository sets).

### Real time data feeds

It was the technical NLNM Simulation that drove the selection of real time data feeds from Branches to Leave nodes (to enable real time interaction between Leave nodes).  NLNM simulations are (being) designed to run between 3 dedicated Trunks (likely in a combined Trunk+single Branch configuration), with two trunks belonging to the opposing sides and one to the Arbiters.

The hierarchical data that is private between opposing-sides is shared within that Trunk only, while shared physical location data crosses Trunk boundaries.  Immediate location of participants and drone positioning data is shared in a Leaf mesh network across Trunk boundaries.

Importantly to the technical parameters of the tech stack, real time data feeds solved the problem of eventual synchronization where final synchronization of data was to be done eventually as Transaction Logs are verified on the server.  With real time Leave synchronization, Transaction Log order can be determined immediately upon receiving (by the Leaf that created them) the Timestamped and Signed Transaction Log entries  back from the Branch.  In turn this can is enabled by the concept of Cross-Trunk-verified Timestamp Stream.

With these Timestamps the bulk of the data can be efficiently synchronized for a Repository via a Leave Mesh network, without having to be multiplexed through a Branch and saving shared network resources.  All incoming new Repository Transaction Logs that cannot be synced via Mesh networking (due to Repository settings or network walling) will be real-time streamed from the local Brach and across Trunks.

The streaming will be done in real time with virtually only network-transition delays (implemented via on-network-card streaming). Because split is split at Trunks and Branches data sharing will not have server-bottlenecks (due to network's topological efficiency).

The asynchronous access to the Trunk Queue is only needed to validate and record transactions at each Trunk.  The access to the Branch queue by its Leaves is needed when a Leave needs to access a Repository that isn't locally cached and is pre-cached at the Branch due to frequent access (falling back to long-term on-Branch Transaction Log storage and finally to Trunk queue and storage if necessary).   

### Cross-Trunk Timestamp Stream

The idea for some sort of peer timestamp validation system has been thought of for a while and is known to have been solved in the Solana network.  It's most useful in DIN at validation/replay time of NLNM simulations to ensure that all actions affecting the simulation-real environment were done at the time the opposing sides claim - the idea for technical implementation concept once again arrived after the real NLNM simulation driven need gave the incentive to definitely provide a mechanism for provable chronological order.

The final solution to it (one of the last  two ideas to appear) arrived in the form of creating mutual Trunk heartbeat services and deriving cross Trunk latency on top of that.  The hypothesis is that this will allow for Trunks to agree on cross-Trunk verified timestamps that then can be passed to Branches for timestamping Transaction Log entries sent by Leaves.  This can be further reinforced by the latest NLNM simulation idea of co-located (in the same position in the simulated battlefield) Leaves of opposing side participants and UN observer drones recording (and signing) the Transaction Log entries they are receiving from the other Leaves of the parties in the same location (thus providing collective mutual verification at simulation replay time). 

### Data Storage

Repositories are interdependent with other Repositories - either depending on other Repositories or mutually depending on one another. Storing all Trunk and cross Trunk Repository dependencies is both not needed on Branches which serve a particular subset of accounts and requires excessive storage, driving up expenses.  The Branch only needs long term storage of Repositories that are accessed by it's Leaves.  This is most easily (initially) implemented in NLNM simulations with units being permanently assigned to a branch and operating at a distinct in-simulation-physical location.

The combined Trunk data is centralized on its Trunk.  Further development of [NLNM simulation](https://github.com/past-the-war-earth/sapoto.net) parameters to allow for physical limitation of access to battalion data-only by it's headquarters and upper command, creating a full Trunk at it's Branch drove the need for the previously abstract the idea of nested sub-Trunks, which would duplicate the local Branch data, without having access to all of Trunk data.  This can eventually be utilized in the hypothesized outer-space cross-governmental security organization with multiple-access-level Groups (previously only abstractly proposed) and may have applications beyond that.

### Dedicated per-node queues.

The idea to use dedicated per-Trunk and per-Branch queues arrived last.  Dedicated queues allow for highly performant, non-distributed data sharing between persistence-isolated nodes.  This eliminates chatter between Branch nodes and fully isolates them using framework, with data redundancy provided via Tree mechanisms.  Basically if a Leaf node needs to quickly load a Repository from its Branch it will grab it from the queue.  The Branch queue is also accessed by the Trunk for storage and synchronization of the transactions from that branch.

The trunk maintains a Queue of own (recent) Repository data and the data from other branches that it's Repositories depend on. (In the initial NLNM simulation implementation there may not be any sharable cross Trunk repositories beyond the initial parameter Repositories that are shared before the simulation, simplifying the initial implementation.)

Records in this Queue are combined with Transaction Log Queues from all local Branches in chronological order, to synchronize the order of modifications and provide for proper central verification (and if necessary conflict resolution) of data.  Processing is done asynchronously and does not have any back-pressure.  This can be accomplished because Leaves already share data for the Repositories they participate in either directly via a Mesh Network or via live (real-time) streams from their Branches and perform data synchronization locally based on Branch synchronization time stamps.

The combination of a "from other Trunks" queue with the polling of per-local Branch queues solved the issue of ensuring that all (including cross-Trunk) data is processed in order.

## Rough Implementation Timeframes

### Initial Implementation

To meet the 2031 Phase 1 NLNM simulation deadline, an initial naive implementation will allow for two Trunk+Branch servers with the Minimum Viable Stack, each directly synchronizing data with its Leaf Servers.  The mesh network of Leaves will also be necessarily present to allow for sharing of (in-simulation) physical data across by adjacent units across the opponent sides.

### Full compartmentalized Implementation

Phase 2 and Phase 3 of NLNM simulation will necessitate the development of the rest of the core stack.

### Load detection

Eventually, to ensure proper load balancing all Branches will track the load on their underlying hardware to maintain communication with the rest of the Branch nodes of the same Trunk. As is now apparent, this must be done after Phase 3 to only subsequently introduce the additional layer of complexity and let the professionals deal with that.

### For Votes

[Votecube](https://github.com/past-the-war-earth/votecube.com) drove requirement of quick total counts for poll outcomes.  To accomplish this incoming votes from Leaf nodes are pre-aggregated on Branch nodes.  These per-Branch aggregates are periodically forwarded to the Trunk node and are further aggregated and forwarded to peer Trunks (as needed, per cross-Trunk subscriptions).  Incoming vote aggregates are pushed back to Branch nodes, based on Leaf node subscriptions and are either delivered to Leaf nodes or stored for later delivery directly from the Branch nodes.
