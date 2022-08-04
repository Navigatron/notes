[up](../index.md)

# Housekeeping



# DNS Delegation

There are 5 regional internet registries, responsible for different portions of the world.

Each manages the number resources within their region of the world.

IANA delegates resources to RIRs, who delegate to their customers - ISPs and organizations.

ICANN is also involved.

## Review of dns tree

Root servers point to top level domains. Top level domain servers provide referrals to second level domains. Second level domains may either make decisions or delegate further.

Delegation allows breaking single large servers into distributed, more powerful systems.

As of march 2017, there were 126.85 million second level domains under .com

## config

parent has NS record for child, and address record for child.

## The .arpa domain

*address and routing parameter area*

used to map IP addresses to domain names.
