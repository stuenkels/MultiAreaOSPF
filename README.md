┌────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                    │
│                      Router 3                                                      │
│                       ─ LO/0   10.1.1.1/24        2001:db8:1:1::1/64               |
|                         S0/0   30.0.0.1/30       2001:db8:3:0::1/64                │
│                      Router 4                                                      │
│                       ─ S0/0   30.0.0.2/30        2001:db8:3:0::2/64               │
│                         S0/1   10.0.0.2/30        2001:db8:0:0::2/64               │
│                      Router 1                                                      │
│                       ─ S0/1   10.0.0.1/30        2001:db8:0:0::1/64               │
│  ┌──────────────┐       S0/0   10.0.0.5/30  2001:db8:1:0::5/64  ┌──────────────┐   │
│  │    L0/0      │    Router 2                                   │    L0/1      │   │
│  │  ────┬────   │     ─ S0/0   10.0.0.6/30  2001:db8:1:0::6/64  │  ────┬────   │   │
│  │      │       │       G0/1   10.0.0.9/30  2001:db8:2:0::9/64  │      │       │   │
│  │ ┌────┴─────┐ │    Switch 1                                   │ ┌────┴─────┐ │   │
│  │ │          │ │     ─ f0/1   10.0.0.10/30 2001:db8:2:0::10/64 │ │          │ │   │
│  │ │ Router 3 │ │       f0/2   20.0.0.2/30  2001:db8:20:0::2/64 │ │ Router 5 │ │   │
│  │ │          │ │    Router 5                                   │ │          │ │   │
│  │ └────┬─────┘ │     ─ g0/1   20.0.0.1/30  2001:db8:20:0::1/64 │ └─────┬────┘ │   │
│  │ S0/0 │       │       LO/1   10.2.2.2/24  2001:db8:2:2::2/64  │   g0/1│      │   │
│  │      │ S0/0  │                                               │       │(VLAN 2)  │
│  │ ┌────┴─────┐ │                                               │   f0/2│      │   │
│  │ │          │ │                                               │ ┌─────┴────┐ │   │
│  │ │ Router 4 │ │                                               │ │ Layer  3 │ │   │
│  │ │          │ │      ┌─────────────────────────────────┐      │ │  Switch  │ │   │
│  │ └────┬─────┘ │      │ ┌──────────┐       ┌──────────┐ │      │ └─────┬────┘ │   │
│  │      │S0/1   │      │ │          │S0/0   │          │ │      │   f0/1│      │   │
│  │      └───────┼──────┼─┤ Router 1 ├───────┤ Router 2 ├─┼──────┼───────┘      │   │
│  │              │  S0/1│ │          │   S0/0│          │ │g0/1  │  (VLAN 1)    │   │
│  └──────────────┘      │ └──────────┘       └──────────┘ │      └──────────────┘   │
│           Area 1       └─────────────────────────────────┘               Area 2    │
│                                                    Area 0                          │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘