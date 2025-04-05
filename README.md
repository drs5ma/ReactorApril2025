#  Multi-Agent System for Smart Traffic Management 

## Pitch

Have you ever wanted to run a red light or stop sign when no other cars are around—safely? Well, now your autonomous car can. Instead of a world where traffic signals that alternate between red and green 🚦 they now spend most of their time yellow - a go ahead signal for autonomous vehicles to rely on local communication with other AVs to safely navigate through intersections and reduce traffic.


## Approach
[![Traffic intersection without signals](https://img.youtube.com/vi/SQ3rxwVYs5c/0.jpg)](https://www.youtube.com/watch?v=SQ3rxwVYs5c)

Inspired by the organically evolved cities of the global south where intersections are navigated by human negotiation and informal coordination, we're developing we’re developing a hybrid traffic control system that reaps the best of both worlds using dynamic mode switching. Grid-oriented city plans overlayed with a matrix of traffic control signals offer a simple way for cities to override autonomous vehicle negotiation and revert to famililar red/yellow/green during specific situations like ambulance emergencies and large event planning. Local coordination and negotiation allows the system to be forgiving and flexibile enough to handle the pain points with top-down traffic control:
- Empty intersections at 2AM
- Dense pedestrian zones
- Unexpected obstacles

## Deisgn

We introduce a common protocol that Autonomous Vehicles Manufactorors implement against a common interface. Implementations are rigosurly tested in extensive simulations by the National Highway Traffic Safety Administration (NHTSA) before being approved for general use.

The interface is based on a distrbuted version of the Apache Mesos. Agents both make offers ("I'll go first and you go second") and submit bids in response ("ok you go"), then choose from the offers received. Such a  model facilitates decentralized coordiantion.

```
public interface NegotiationAgent {

    // Offer a proposal to nearby agents 
    Offer createOffer();

    // Receive a Bid responses
    void receiveBid(Bid bid);

    // Choose winning bid
    void finalizeNegotiation();
}
```

### Features
1. Fusion Platooning -  two or more AVs temporarily merge into a single coordinated unit to become a "bus" acting as one agent. These AVs synchronize breaking and accleration only maintaining a few inches of space from bumper to bumper. Taking up less space, more cars can pass through an intersection in a given time window improving overall throughput.
2. Destination Optimization - AVs traveling in the same direction can share their final route and decide whether to change route based on online traffic predictions
3. 


### Backwards compatibility
There will exist an extended period of time when both humans and autonomous vehicles co-exist on the road. To support this reality the implementations must handle and defer to human drivers. Humans are predictable to a certain degree, AVs will be able to detect with cameras and behavioral analytics using eye tracking to infer intention and attention and distracted driver recognition. AVs by default will defer to human-operated vehicles and laws will be passed to create negative incentives for "messing" with AVs (e.g. pulling in front of a Tesla to trigger it's automatic breaking). As AVs become more unibiquitous, the overall efficiency of the system will seamlessly improve without additional modifications. We also propose that metropolitan cities enforce zones where only AV's operate, similar to no-car zones in city centers across Europe.

## Security 

We can't ignore the reality of bad actors. To mitigate this threat, we rely on cryptographic protocols to make the system byzantine fault tolerant:

> The Byzantine allegory considers a number of generals who are attacking a fortress. The generals must decide as a group whether to attack or retreat; some may prefer to attack, while others prefer to retreat. The important thing is that all generals agree on a common decision, for a halfhearted attack by a few generals would become a rout, and would be worse than either a coordinated attack or a coordinated retreat.

To handle this, AVs communicate with error correcting codes and digital signatures. The signing keys registered with local governing bodies. AVs "gossip" with nearby AVs to identify bad actors and cheaters (game theory) and report the offending digial key and timestamped geolocated photo of the AV to law enforcement.

