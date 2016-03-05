# Building a trading system in Scala
Author: [@plarroy](http://twitter.com/plarroy)
<span class="badge-paypal"><a
href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=6SLKKT7NJUVM6"
title="Donate to this project using Paypal"><img
src="https://img.shields.io/badge/paypal-donate-yellow.svg" alt="PayPal donate button" /></a></span>


This will be the first post in a series of posts describing how I'm building an automated trading system mostly in Scala but with Python interoperability, either via the Jython interpreter or by using standard data formats that can be readily used from Python.

The source code of the framework will be open sourced on Github with a permissive MIT license which allow it to be used for commercial purposes.

We will touch diverse topics such as functional programming, databases, networking, time series analysis and machine learning.

### Why mostly Scala?

When building a nontrivial framework, there's an absolute need to have a typed language that makes the code robust and easier to refactor, plus it requires less testing than with a dynamic language given that the compiler which check the invariants and guarantees described by the type system. Scala is a type safe, concise language which combines object oriented programming with functional programming which gives a very high degree of flexibility and power.

Still Scala is yet not up to par with the amount of tooling available for Python for data analysis, plotting and for data science tasks. There are good frameworks and libraries such as Saddle, Breeze that are making things better. For these things we can use Python to bridge the gaps in the Scala/Java ecosystem.

On the other hand, leveraging the concurrency capabilities of the JVM, the Spark framework for distributed computation, and the plethora of available Java and Scala libraries makes using Scala a very good choice.

You can read more rationale in the following post: [Why I choose Scala for the Apache Spark
project](https://www.linkedin.com/pulse/why-i-choose-scala-apache-spark-project-lan-jiang)


## Automated trading systems

With more than 75% of the trading volume originating from automated trading systems, individual
investors and traders are at a disadvantage when trading against machines.


What's an automated trading system (ATS)?
In its most simplified form is just a stateful function that reacts to market data and produces orders that are sent to a broker.


```
                +---------------+
 Market data    |               |  Orders
                | Automated     |
+---------------> Trading       +---------->
                | System        |
                | (ATS)         |
                |               |
                +---------------+
```

Real ATSs are often much more complex, as there's a need for a lot of infrastructure around the algorithms that will react to market data and produce orders. Some of the things that we will need to build will also be helpful for other tasks such as portfolio optimization.

Some of the infrastructure needed around an ATS is:

* An historical data storage
* Back-testing capabilities, for training algorithms and verifying trading strategies
* Connection with the broker to submit orders and get the order book
* Risk analysis and safety systems to check market exposure and risk


Building an automated trading system is a lot of complex work. That alone puts the individual trader and investor at a big disadvantage given the amount of time or resources she would have to put on to build all the required infrastructure around an ATS.

There are hosted solutions such as Quantopian (python based) and Quantconnect (C# based), with partially open sourced components. Here I want to set the first stone in having a typesafe, permissive open source trading system framework to build automated trading strategies, optimize portfolios and analyze securities.

