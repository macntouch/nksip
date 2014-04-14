[![Build Status](https://travis-ci.org/kalta/nksip.png?branch=master)](https://travis-ci.org/kalta/nksip)

**IMPORTANT**: NkSIP is under very heavy development. Documentation is not currently updated. In the following weeks, version v0.4 will be released, and documentation will be updated with it.


## Introduction

NkSIP is an Erlang SIP framework or _application server_, which greatly facilitates the development of robust and scalable server-side SIP applications like proxy, registrar, redirect or outbound servers, [B2BUAs](http://en.wikipedia.org/wiki/Back-to-back_user_agent), load generators, etc. NkSIP takes care of much of the SIP complexity, while allowing full access to requests and responses. 

NkSIP can start any number of SIP Applications or _SipApps_, each one listening on a different set of transports, ips and ports. Each SipApp must provide a `callback module`, with functions that will be called when specific requests are received, dialogs are started, etc.

NkSIP also includes a powerful **plugin mechanism**, that can modify its behaviour without touching the core, and with virtually zero overhead.

NkSIP is currently **alpha quality**. It is **not yet production-ready**, but it is already very robust, thanks to its OTP design. Also thanks to its Erlang roots it can perform many actions while running: starting and stopping SipApps, hot code upgrades, configuration changes and even updating your application behavior and  function callbacks on the fly.

NkSIP scales automatically using all of the available cores on the machine. Using common hardware (4-core i7 MacMini), it is easy to get more than 3.000 call cycles (INVITE-ACK-BYE) or 10.000 stateless registrations per second. On the roadmap there is a **fully distributed version**, based on [Riak Core](https://github.com/basho/riak_core), that will allow you to add and remove nodes while running, scale as much as needed and offer a very high availability, all of it without changing your application.


## NkSIP main features are:
* Full support for all curently defined SIP methods: INVITE, ACK, REGISTER, OPTIONS, INFO, UPDATE, PRACK, SUBSCRIBE, NOTIFY, REFER, PUBLISH and MESSAGE, as UAC, UAS and Proxy.
* Can be used to develop any possible SIP application: endpoints, stateful proxies with serial and parallel forking, stateless proxies, B2BUAs, application servers, registrars, SBCs, load generators, etc. 
* UDP, TCP, TLS, SCTP, WS and WSS transports, capable of handling thousands of simultaneous sessions.
* Full SIP Event support.
* A written from scratch, fully typed 100% Erlang code with few external dependencies.
* Robust and highly scalable, using all available processor cores automatically.
* More than 150 tests covering nearly all of the functionality.
* Sophisticated plugin mechanism, that adds zero overhead to the core.
* Hot, on-the-fly core and application configuration and code upgrades.
* IPv6 support and IPv4 <-> IPv6 bridge.
* Full support for NAPTR and SRV location, including priority and weights.
* Dialog and SDP media start and stop detection.

## Included standard plugins:
* SIP Digest Authentication.
* SIP Registrar.
* SIP Event State Compositor.
* Reliable provisional responses.
* Automatic registrations and timed pings.
* Outbound and GRUU support.


# Documentation

[Main Documetation](doc/README.md)


# Quick Start

NkSIP has been tested on OSX and Linux, using Erlang R15B y R16B

```
> git clone https://github.com/kalta/nksip
> cd nksip
> make
> make tests
```

Now you can start a simple SipApp using the included [default callback module](src/nksip_sipapp.erl):
```erlang
> make shell
1> nksip:start(test1, nksip_sipapp, [], []).
ok
2> nksip_uac:options(test1, "sip:sip2sip.info", []).
{ok, 200, []}
```
 
From this point you can read the [tutorial](doc/TUTORIAL.md) or start hacking with the included [nksip_pbx](http://kalta.github.io/nksip/docs/v0.1.0/nksip_pbx/index.html) application:
```erlang
> make pbx
1> nksip_pbx:start().
```

You could also perform a heavy-load test using the included application [nksip_loadtest](http://kalta.github.io/nksip/docs/v0.1.0/nksip_loadtest/index.html):
```erlang
> make loadtest
1> nksip_loadtest:full().
```

# Contributing

Please contribute with code, bug fixes, documentation fixes, testing with SIP devices or any other form. Use 
GitHub Issues and Pull Requests, forking this repository.


[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/eaae4b01a225feae6da3b7142c17d8c0 "githalytics.com")](http://githalytics.com/kalta/nksip)
