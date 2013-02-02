A design for secure networking
==============================

See design.md for the actual design.


Motivation
----------

You don't have to be a nuclear weapons lab, as in [this Reuters article on LANL][Reuters], to worry
about network equipment security these days. The possibilities provided by hardware and firmware
backdoors have long been understood to be a genuine source of security worries.

While the Reuters article is about U.S. suspicion towards Chinese-made networking equipment,
there is no particular reason to trust any specific vendor or country over another.

Excerpt from [the Reuters article on LANL][Reuters]:

> Exclusive: U.S. nuclear lab removes Chinese tech over security fears
> 
> Mon, Jan 7 2013
>
> By Steve Stecklow
>
> LONDON (Reuters) - A leading U.S. nuclear weapons laboratory recently discovered its computer systems contained some Chinese-made network switches and replaced at least two components because of national security concerns, a document shows.
>
> [...]

[Reuters]: http://www.reuters.com/article/2013/01/07/us-huawei-alamos-idUSBRE90608B20130107 "Exclusive: U.S. nuclear lab removes Chinese tech over security fears"


Premise
-------

Perhaps the design premise is easiest to understand from an abstract philosophical viewpoint.

The claim being made is that you can't possibly know, without resorting to desctructive inspection
of the hardware, what the true functionality is that is implemented in your low-level
networking hardware, that is, the components dealing with the physical layer.

Therefore, you can't prove the components are secure.

Therefore, it must be made irrelevant whether the components are secure or not, so that
you don't need to trust that they are secure.

Therefore, the design goal is to make it irrelevant whether your low-level networking hardware
components are secure or not.
