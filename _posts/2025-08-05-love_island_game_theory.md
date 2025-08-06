---
layout: post
title: Game Theory explained through Love Island
date: 2025-08-05 00:32:13
description: An explanation of how game theory influences the drama of Love Island's "Casa Amor".
tags: fun education
tabs: false
pretty_table: true
---

# Game Theory explained through Love Island
This summer, when my friends roped me in to watching Love Island USA S7 I was expecting mindless drama, not economic strategy. I was wrong.

Underneath the tears and tans, it's pure game theory. For the more strategic — and let’s be honest, dishonest — players (*cough cough* Ace), every “loyal connection,” every flirty chat, every recoupling is a calculated bet under uncertainty. The goal? Make it to the final four with a connection that looks strong enough to win..

And no twist captures this better than Casa Amor.

## Casa Amor
Consider the event of Casa Amor, a crucial inflection point in a season of Love Island. This recurring dramatic event has the singular goal of testing the strength of the islanders' connections (as well as providing the audience with some messy drama to be entertained by). 

In the traditional rules of the Casa Amor twist, the men are whisked away to Casa Amor while the women remain in the villa. New single contestants are brought to both locations to tempt and test the connections that have been built up until this point. The islanders then spend three days with the new contestants, without knowing what their partner is up to. At the end of the three days, the islanders must decide to either bring a new contestant or come alone to the villa.

From a game theory perspective, Casa Amor works as a simultaneous-move game where each islander involved must independently decide whether to stay loyal to their previous partner or to "recouple" with a new contestant. This results in a classic coordination game where each player is blind to what the other will do, but hopes to land on the same outcome as each other. 

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/blog_images/casa_amor.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The Casa Amor villa in [Love Island USA Season 7](https://www.hollywoodreporter.com/tv/tv-news/love-island-usa-casa-amor-bombshells-season-7-1236297727/)
</div>

In this coordination game, the best outcome would be for both islanders to stay loyal, as they keep their strong connection and avoid any reputation fallout from betraying their previous love. Another positive outcome, but less desirable, is for both islanders to recouple with the Casa Amor contestants. In this event, both islanders are able to come back to the villa coupled up, but with a seemingly less strong connection. The **worst** scenario occurs when one islander chooses to stay loyal when their previous partner chooses to recouple. This results in the loyal islander now single and vulnerable, while the recoupled islander suffers from reputation fallout and guilt.

## The Happiness Score

We can quantify the outcome of this game by creating a "happiness" score to represent how happy the islanders are after the events of Casa Amor. This "happiness" score is typically called a "payoff" in game theory. A score of 9-10 means an islander is incredibly happy while a score of 0-1 means an islander is incredibly sad. 

To illustrate how the players would feel in different outcomes, we can imagine a scenario with two islanders: Noah and Stephanie. Both Noah and Stephanie have the option of either staying loyal to each other or recoupling. If both Noah and Stephanie stay loyal, they are both *very happy* at 8/10. If both Noah and Stephanie decide to recouple, they are both equally *okay* at 5/10. However, if Noah decides to stay loyal while Stephanie decides to recouple, Noah is *extremely sad* and has a happiness score of 1/10 while Stephanie is *content* with a score of 6/10. This game is symmetric, which means that Noah and Stephanie like each other the same amount. Looking at the payoff matrix below, we can organize the happiness scores of the islanders based on their decisions.

|                    | Stephanie: Loyal    | Stephanie: Recouple   |
|--------------------|---------------------|-----------------------|
| **Noah: Loyal**    | (8, 8)              | (1, 6)                |
| **Noah: Recouple** | (6, 1)              | (5, 5)                |

