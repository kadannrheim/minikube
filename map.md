#Map

1. Road
HOST ssh > st1 (linux); ansible managed clients to ssh > st2 and st3 and st4
2. Hosts
* t430 - users host (physical machine)
    * st1 - main for ansible (VM, virtualbox), vagrant\docker machine:
        * st2 - cluster kubernetes nod #1 ()
        * st3 - cluster kubernetes nod #2 ()
        * st4 - cluster kubernetes nod #3 reserve ()