## Intruder types
- Sniper: The most popular attack type, this cycles through our selected positions, putting the next available payload (item from our wordlist) 
in each position in turn. This uses only one set of payloads (one wordlist).

- Battering Ram - Similar to Sniper, Battering Ram uses only one set of payloads. Unlike Sniper, Battering Ram puts every payload into every selected position. 
Think about how a battering ram makes contact across a large surface with a single surface, hence the name battering ram for this attack type.

- Pitchfork - The Pitchfork attack type allows us to use multiple payload sets (one per position selected) and iterate through both payload sets simultaneously.
For example, if we selected two positions (say a username field and a password field), we can provide a username and password payload list. 
Intruder will then cycle through the combinations of usernames and passwords, resulting in a total number of combinations equalling the smallest 
payload set provided. 

- Cluster Bomb - The Cluster Bomb attack type allows us to use multiple payload sets (one per position selected) and iterate through all combinations of the 
payload lists we provide. For example, if we selected two positions (say a username field and a password field), we can provide a username and password payload 
list. Intruder will then cycle through the combinations of usernames and passwords, resulting in a total number of combinations equalling usernames x passwords.
Do note, this can get pretty lengthy if you are using the community edition of Burp. 
