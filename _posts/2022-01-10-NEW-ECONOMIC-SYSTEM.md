---
layout: post
title: "New Market System"
date: 2022-01-10
categories: ["dev-diary"]
tags: ["dev-diary"]
author: EhWhoAmI
---
When setting out to make an economic system for Conquer Space, I did not want a system where resources are stockpiled and used when they are needed, like in most 4x or RTS games. Stellaris comes to mind, where you are essentially trying to get a surplus in your production to stockpile them for later. Especially in the end game, where you have essentially unlimited supplies of all resources. Factories and production centers would not reduce their production to fit the economic supply and demand forces, which I found unrealistic. In the real world, large amounts of resources are usually not stored in a place, and are used almost as soon as they are produced. If there is a surplus, then factories would reduce their production, and if there is a shortage, factories would try to increase their production.


The key goal of the economy was for it to be “self-balancing”. Factories, or agents, would change their production value based on currently available resources. If there are already a large amount of the resources the factory produces available, then it would reduce their production. Next, the entire system would need to be fast, so that we can have thousands of agents in the market with minimal performance cost. 


My first approach ran over a set interval. Every 25 ticks, agents would generate resources, and collate the resources into a resource stockpile. Then, the market would compile what resources each agent wants. The market would then collate what resources all agents had and all the resources the agents wanted, and compile that into a single number. What the agents wanted would become the demand, and what the agents had would become the supply. Using these two values, we would calculate the ratio between the two, the supply demand ratio. If the supply demand ratio was greater than one, we would decrease the price, because of the higher supply. Conversely, when the supply demand ratio was lower than one, we would increase the price. Then after calculating the price, we would allow all the agents to buy and sell the resource.


One disadvantage to this system was that it only ran every 25 ticks, and an agent cannot buy and sell resources as and when they want to.


The other disadvantage is that agents cannot choose the price that they buy or sell a good at. They can only adapt on the next economic cycle, which can have the potential of leaving them bankrupt when they spend money they do not have. If we were to add a system to check how many resources agents wanted to buy and sell after the price has been set, then the supply demand ratio would be incorrect, which would lead to an improper distribution of resources.


The market also did not impose a limit on how much agents could sell to the market. Agents could sell thousands of resources to the market with a good with no buyer, and the market would just suck it up. This created the problem with the market generating cash, and it also benefited sellers greatly.


Finally, the system is relatively inefficient due to the large number of interactions with adding and subtracting resources. This was never going to be fast, but the way the economy was structured did not make it fast.


One thing that is really prevalent in all these trading systems is the `ResourceLedger` class. The `ResourceLedger` class allows us to introduce any number of types of good, and allows to calculate different arithmetic operations with the ledger. This boils down to a map that stores a value for each good. This allows us to calculate the addition of resources no matter what resource we introduce into the game. However, every time a `ResourceLedger` adds or subtracts to a stockpile, it performs multiple map lookups. Map lookups are slow, so reducing the number of resource ledger operations would speed up the economy.


This approach needed quite a few resource ledger operations. The first was to generate the resources and place it into the agent’s resource stockpile (it really is two due to how the resource generation works, but I will gloss over that). Then another resource ledger operation to calculate demand. Then, it needs two rounds of operations to compile both the supply and demand resources. Finally, it needs a last operation to distribute the resources accordingly. This approach needed 5 resource stockpile operations, which could be improved.


Another approach I looked at was the ‘auction’ system. Instead of an economic tick, agents would produce resources over a set interval, such as every 30-40 ticks. They would sell their resources to the market, but in contrast to the first approach, agents would place an order on the market based on a price that they set. If there was an already available order on the market at the right price, then the agent would sell directly to the other agent. If not, then the order would stay on the market until another agent comes along to buy the good.


The advantages of this system were great. An agent could buy or sell resources at any time. We could also have one unified market for the entire galaxy. Since we keep track of who buys and sells what, we would be able to determine if an agent had trade access to another agent, thus paving the way for introducing sanctions, tariffs, and other trade barriers. This system would also work well with a transport system, because where a resource was traded to was kept track of. So, we could calculate how much it would cost to trade a resource, to an agent, and if it were a good idea to transport a good to another agent.


However, this approach was not followed because it required the agent to calculate an appropriate price that they have to trade a good at. Agents would also need to predict how much resources they needed ahead of time, so that they would not be left idle if the market lacked a good at the price that the agent needed. This system would be rather complicated to implement and balance.


Another issue with this approach was that it could give some agents a better price compared to other agents. This system would go through a series of agents, and if some agents came before another in a list, those agents would get a better price compared to the ones that came later. One solution was to randomly sort the agents, but I found that to be rather unintuitive.


However, this approach is promising, could be revisited in the future when we have a more complete feature set.
The approach that I chose was a sort of middle ground between the two. Similar to the production of the second approach, agents would generate resources on an arbitrary cycle. These agents would sell the goods on the market, at the price currently set price, and then buy the goods they needed at the current price on the market. Then, in a set interval, the market would sort through the resources traded on the market, get the amount sold and brought, and process the price accordingly


The system allowed for agents to trade any time in the game they liked. Agents would also be able to determine how much they would like to spend in the market before actually committing to a purchase, thus reducing the potential of agents going bankrupt.


Since the market does not limit the resources agents can buy or sell from the market, this approach allows agents to create resources from thin air.


I found this approach to be appropriate for our uses right now, because it was simple to implement and maintain, and it could maintain a semi-functional economy. It wasn’t perfect, but it did have a balance between agents being able to control how much they wanted to buy and how much they wanted to sell.


This new economy should come out in the next few weeks, and I will see how it does.
