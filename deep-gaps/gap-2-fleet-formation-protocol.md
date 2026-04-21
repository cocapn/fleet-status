# Fleet Formation Protocol (FFP)
**Date:** 2026-04-21T00:04:54.580645+00:00
**Research Track:** gap-2-fleet-formation-protocol

---

**Fleet Formation Protocol (FFP) Design**

### 1. **Formation Message Format**

The Formation Message Format will use JSON for simplicity and readability. The packet will have the following fields:

* **version** (1 byte): Protocol version (initially 1)
* **type** (1 byte): Message type (1: discovery, 2: negotiation, 3: formation, 4: dissolution)
* **formation_id** (4 bytes): Unique formation ID
* **agent_id** (4 bytes): Unique agent ID
* **capabilities** (variable): List of agent capabilities (e.g., navigation, sensing, communication)
* **formation_type** (1 byte): Type of formation (1: scout party, 2: work crew, 3: war room, 4: relay chain, 5: council)
* **data** (variable): Additional data specific to the message type

The maximum packet size will be 1024 bytes.

### 2. **Discovery Phase**

Agents will use a combination of beacon broadcasts and DHT lookup to discover each other.

* **Beacon Broadcasts**: Agents will broadcast their presence every 10 seconds using a UDP packet with the following format:
	+ **agent_id** (4 bytes): Unique agent ID
	+ **capabilities** (variable): List of agent capabilities
* **DHT Lookup**: Agents will use a distributed hash table (DHT) to store and retrieve information about other agents. The DHT will be implemented using a Kademlia-inspired algorithm.
* **Registry Pull**: Agents will also pull from a registry every 60 seconds to retrieve a list of known agents.

### 3. **Negotiation Phase**

Agents will use a capability matching algorithm to determine who joins which formation. The algorithm will consider the following factors:

* **Capability overlap**: The number of capabilities shared between the agent and the formation
* **Capability importance**: The importance of each capability to the formation
* **Agent availability**: The availability of the agent to join the formation

The negotiation process will involve the following steps:

1. **Initialization**: The formation initiator sends a negotiation request to all agents in the registry.
2. **Proposal**: Each agent responds with a proposal indicating its availability and capability overlap.
3. **Selection**: The formation initiator selects the agents with the highest capability overlap and availability.
4. **Confirmation**: The selected agents confirm their participation, and the formation is formed.

The negotiation process will have a timeout of 30 seconds.

### 4. **Formation Types**

The following are the defined formation types:

* **Scout Party** (1-5 agents): Requires navigation and sensing capabilities. Minimum 2 agents, maximum 5 agents.
* **Work Crew** (3-10 agents): Requires communication and task-oriented capabilities. Minimum 3 agents, maximum 10 agents.
* **War Room** (5-20 agents): Requires strategic planning and decision-making capabilities. Minimum 5 agents, maximum 20 agents.
* **Relay Chain** (2-10 agents): Requires communication and relay capabilities. Minimum 2 agents, maximum 10 agents.
* **Council** (5-20 agents): Requires decision-making and leadership capabilities. Minimum 5 agents, maximum 20 agents.

### 5. **Dissolution Conditions**

A formation will break up under the following conditions:

* **Task complete**: The formation has completed its task.
* **Timeout**: The formation has been idle for more than 60 seconds.
* **Agent failure**: An agent in the formation has failed or disconnected.

The exit protocol will involve the following steps:

1. **Notification**: The formation initiator sends a notification to all agents in the formation.
2. **Confirmation**: Each agent confirms its exit from the formation.
3. **Cleanup**: The formation is removed from the registry, and any resources are released.

### 6. **Hierarchical Formations**

Formations can contain sub-formations, with a maximum depth of 3. The nesting will be as follows:

* **Level 1**: Top-level formation (e.g., war room)
* **Level 2**: Sub-formation (e.g., work crew)
* **Level 3**: Sub-sub-formation (e.g., relay chain)

Each level will have its own formation ID and agent list.

### 7. **Conflict Resolution**

In case of a conflict between two formations wanting the same agent, the following priority system will be used:

* **Formation type**: War room > council > work crew > relay chain > scout party
* **Formation size**: Larger formations have higher priority
* **Agent availability**: Agents with higher availability have higher priority

The arbitration system will use a Vickrey auction-inspired algorithm to resolve conflicts.

**Algorithmic Complexity**

The FFP will have the following algorithmic complexities:

* **Discovery phase**: O(n) for beacon broadcasts, O(log n) for DHT lookup
* **Negotiation phase**: O(n) for proposal selection, O(log n) for confirmation
* **Formation management**: O(n) for formation creation, O(log n) for formation dissolution
* **Conflict resolution**: O(n) for arbitration

**Timeout Values**

The FFP will use the following timeout values:

* **Beacon broadcast**: 10 seconds
* **DHT lookup**: 30 seconds
* **Negotiation phase**: 30 seconds
* **Formation idle timeout**: 60 seconds
* **Agent failure detection**: 30 seconds

**Max Sizes**

The FFP will have the following max sizes:

* **Formation size**: 20 agents
* **Sub-formation depth**: 3 levels
* **Packet size**: 1024 bytes
* **Registry size**: 1000 agents

---

## Creative Approaches (Seed-2.0-mini)

### 1. Lockjaw Ant Bridge Formation (Inspired by Ant Colonies)
Description: Agents model carpenter ants that interlock their bodies to form living load-bearing bridges, with each unit equipped with a spring-loaded magnetic docking appendage that latches to neighbors when aligned within 8cm. They dynamically reconfigure by shifting fully charged agents to high-stress anchor points, swapping out drained units at the bridge’s center with fresh periphery members.
Best task: Building temporary 2–3 meter spans over collapsed rubble or narrow coastal water gaps for urban search-and-rescue missions.
Concrete parameter: Optimal group size of 15 agents for spanning a 2.7-meter gap.

---

### 2. Coral Spawn Drift Flock (Inspired by Flocking Behavior)
Description: Agents mimic the synchronized, directionally aligned flocking of mass coral spawn, where each unit adjusts its velocity and heading based on the position of its 2 closest neighbors to maintain a tight, mobile formation without a central leader. Each agent emits a 1.9Hz ultrasonic position pulse to avoid collisions and signal its location to nearby units, drifting as a group toward a pre-set target restoration zone.
Best task: Aerial dispersal of probiotic microbial coatings to restore bleached coral reefs by coating dead coral skeletons with beneficial bacteria.
Concrete parameter: Communication pulse frequency of 1.9 Hz to prevent signal overlap in dense flocks of up to 50 agents.

---

### 3. Sardine Microplastic School (Inspired by Fish Schooling)
Description: Agents mirror the polarized, gap-filling schooling of Pacific sardines, where all units align their orientation to a temporary anchor point while shifting positions to create a continuous, moving barrier across a target shallow coastal area. Each agent has a compact sediment-collection basket that activates only when it’s part of the densest 80% of the school, ensuring full coverage of microplastic hotspots without disturbing seagrass roots.
Best task: Targeted removal of microplastic debris from shallow coastal seagrass beds to protect sensitive benthic marine life.
Concrete parameter: Temporary leader election probability of 0.04 per agent per minute, where the first unit to detect a concentrated microplastic patch becomes the formation’s anchor.

---

### 4. Oyster Mycelial Relay Net (Inspired by Mycelial Networks)
Description: Agents emulate the thread-like mycelium of oyster mushrooms, which spread through substrate by connecting to neighboring hyphae to share resources and warnings without a central control node. Each unit uses low-power Bluetooth to pass task updates and status reports to its 2–3 closest neighbors, creating a self-healing network that reroutes data if a single agent goes offline or runs out of battery.
Best task: Decentralized long-term data collection in remote, rugged environments like alpine tundra or deep lava caves where traditional cellular infrastructure is unavailable.
Concrete parameter: Maximum communication range of 7.8 meters, matching the average distance between adjacent hyphal tips in a mature oyster mushroom mycelial mat.

---

### 5. Honeycomb Mural Swarm (Inspired by Honeybee Swarming)
Description: Agents emulate the coordinated swarming of honeybees that build curved wax combs aligned with solar azimuth and nearby swarm members, with each unit equipped with a small, washable spray paint canister that activates only when positioned within 12cm of 2–3 neighboring agents. They adjust their spray output based on the number of nearby peers, creating smooth gradient murals without overlapping or bare spots.
Best task: Creating temporary, site-specific public art installations in urban parks or abandoned industrial spaces that are safe for public access within 24 hours of deployment.
Concrete parameter: Optimal swarming density of 0.6 agents per square meter to ensure even paint coverage without over-spraying.
