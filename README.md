# Ansible Collection - relrod.allstarlink

An *opinionated* AllStarLink deployment.

Note also that this uses my [fork](https://github.com/AI5A/asl). Currently this
is hardcoded, though in the future I might make it an option.

I think eventually this will turn into something more general and maybe even
some modules for controlling/interacting with ASL. But for right now, it is
limited in scope in utility and most might not find it very useful yet.

In theory, right now you can do something like this:

```yaml
- name: Deploy AllStarLink
  hosts: myserver.local
  roles:
    - role: relrod.allstarlink.allstarlink
      tags:
        - allstarlink
      node_number: 12345
      rxchannel: dahdi/pseudo
      idrecording: ""
      idtalkover: ""
      reg_password: mySekritAllStarPass
      link_rx_courtesy_tone: "|t(800,0,30,1500)(0,0,30,0)(750,0,30,1500)"
      macros:
        - comment: Connect to some cool node
          macro: 10
          command: "*312346#"
        - comment: Disconnect from some cool node
          macro: 11
          command: "*112346#"
      scheduler:
        - comment: Connect to cool node for a net
          macro: 10
          when: 45 9 * * 6
          finish: 15 11 * * 6
          finish_macro: 11
```
