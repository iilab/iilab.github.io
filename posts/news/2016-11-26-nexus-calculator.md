Today, in an Estate near London Bridge in the UK, a community of inhabitants from an estate used our prototype Nexus Calculator to discuss various design options for food sharing, food growing, collecting rainwater or composting on the estate. This is the second time our team meets this community, as part of the Engineering Comes Home project in partnership with University College London and [Open Lab](https://openlab.ncl.ac.uk) at Newcastle University we [blogged about a few months ago](/blog/communities-codesigning-infrastructure).

<!--more-->

Based on the inputs from the first workshop and building on an LCA assessment spreadsheet developed by one of the project's researchers, iilab developed a prototype which aims at supporting decision making of communities when it comes to infrastructure design. The project's key deliverable is a toolkit for infrastructure designers, which will outline different approaches to engage communities on infrastructure.

<center>
<div class="iframeWrapper">
<iframe width="100%" height="*" src="https://www.youtube-nocookie.com/embed/JcF1VU5aCw0?showinfo=0" frameborder="0" allowfullscreen></iframe>
</div>
</center>
<br>

# In the Workshop

We presented the five ideas, providing participants with fact sheets about each one and showing them how to use the LCA calculator to assess different design criteria. The calculator had a scenario for each technology with adjustable input parameters such as volume of food waste, quantity and scale of technologies. These changed the volume of food that could be grown, or amount of CO2 savings realised. Residents explored each scenario in pairs adjusting the calculator according to their assessment of what was appropriate for the estate. These context sensitive adjustments included:

 - **Levels community involvement:** For example, Clare, who’d been involved in other community projects on the estate made an assessment that only 50% of households would participate and went on to limit inputs to this proportion of engagement for all scenarios. By contrast Penny decided the technologies could be designed to increase engagement in some cases. For the waste compactor, she opted to put small manual compactors at each of the  stairwells on the basis that residents would then regularly see them and be encouraged to use them.

 - **Aesthetics and layout of the estate:** Participants used their knowledge of the estate, and of the ways communal space was used by different members of the community. This was particularly the case in the gardening scenarios. Participants anchored their designs in which parts of the estate gardens they would be happy to see turned into food growing areas.

 - **Utility of outputs:** Although the LCA calculator was designed to show the resulting CO2 emissions reductions, these savings were not a very meaningful currency for the group. Instead the designs were more often shaped according to whether the outputs could be used. For example, when assessing the options for the wormeries, Mary was interested in how much fertiliser could be produced and whether the TRA would be able to sell or exchange this amongst other local gardening groups.

After participants had explored each scenario we regrouped and discussed the design options each pair had chosen. This allowed the group to share the different priorities and assessments that had informed their adjustments of the LCA calculator parameters.  After the groups had explored all five ideas we held a vote to pick a single design option to move forward with. The discussion prior to the vote gave space for participants to raise other context specific values and knowledge they felt should be factored into the group’s selection of a design. Governance proved to be a key concern, in particular how much management any design would require, and also how exposed the system would be to tampering from ‘uninitiated outsiders’. For example waste compacting was seen as potentially dangerous if people didn’t know how to use the compactor properly, likewise food sharing was felt to be open to mismanagement.  All participants had a first and second vote and rainwater harvesting won the most votes.

![](/images/news/ech_workshop2_votes.png)

# Functional core

With regards to the technology, our team decided to go with a functional core using Purescript (a Haskell derivative which is well adapted to the frontend) in order to benefit from static types to assist in having correct calculations for the modeled processes. We iterated a few times on the data model and settled on a static representation of each scenarios, to avoid the complexity of a completely modular system where the user can pick and choose freely from a set of Processes.

We also decided to go for an "double-entry accounting model" of material flows, with an approach close to Event Sourcing ([which we're using in Open Integrity as well](https://openintegrity.org/blog/)), where each Process debits upstream processes for the amount of supply they need, credit themselves of this amount, then possibly draw down on the amount on their accounts to transform it into another material which can in turn be drawn from by other downstream processes. This lightweight model seemed adequate for giving broad indications on quantities and wrapping the information in the LCA spreadsheet in an accessible way. Each Process is also a pure function which takes a "ledger" of all material transactions and returns an updated ledger. Although we haven't tested it quite yet, this should allow loops to occur in the graph, for instance when food produced by a Food Garden is diminishing the needed supply of shopped food.

# Research

Engineering Comes Home demonstrated that residents were willing and able to play a meaningful role in the design of neighbourhood scale infrastructure. We started the co-design workshops with a blank sheet in terms of what form our WEF nexus intervention might take and ended with a rainwater tank and hose providing water for the TRA’s flower beds.  This specific design solution evolved from the participants’ broad concern with wastefulness and the value of pioneering water stewardship.

The co-design process was iterative and responsive to the context. Through it we have found:

 - A willingness to engage in the co-design process
 - That people are motivated by the idea of saving WEF resources beyond rational choice models of motivation
 - We could generate a set of shared values to create a design brief
 - It was possible to build technical literacy amongst participants

The pilot has allowed us to test the process and learn from this first case-study. Following the principles of co-design, the lessons learnt have been distilled into a set of co-design method statements which are freely available for others to use and build on.  This first case-study provides an encouraging example of how residents can be included in the technical work of creating less resource intense, more liveable cities.
