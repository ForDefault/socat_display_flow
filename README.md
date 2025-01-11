# socat_display_flow
just testing some ideas do not use




## Layer 2 Syntax Context and Construct for Substitute Command Aggregations
Example command:
```
socat TCP4-LISTEN:9999,fork EXEC:/bin/cat
```
Layer2
```
[[{((connection_type[variation])connection(port)}utility] [,option] [{(utility[action])endpoint}]]
```
Example Applied
```
[[{((TCP4[LISTEN])connection(9999))utility}] [,fork] [{(utility[EXEC])('/bin/cat')}]]
```
```
socat
└── _option_list_
    ├── [,reuseaddr]
    └── [FILE]

[,option]
|
└── [dependent_option]
|   └── [,reuseaddr]
|
└── [utility]
      ├── [connection] (LISTEN)
      │   ├── [connection_type]
      │   │   ├── TCP
      │   │   ├── UDP
      │   │   └── [variation]
      │   │       ├── 4
      │   │       └── 6
      │   └── [port] (9999)
      ├── [action] (EXEC)
      │   └── [endpoint] (/bin/cat)

====================breakdown of logic ===================


[{((connection_type[variation])connection(port)}utility]
|                                                                    ## {..connection(port)}utility  ##
└── [Utility]                                                           [utility]
    ├── [connection] (LISTEN)                                           {((connection_type[variation])connection}
    │   ├── [connection_type]                                           {connection_type[variation]}  
    │   │   ├── TCP
    │   │   ├── UDP                                                     
    │   │   └── [variation]
    │   │       ├── 4
    │   │       └── 6
    ├── [port] (9999)                                                   (port)

[utility{action(endpoint)}]
|                                                                    ## utility{action(endpoint)} ##
└── [Utility]                                                           {utility}
    ├── [Action] (EXEC)                                                 {action(endpoint)}
    │   └── [Endpoint] (/bin/cat)                                       (endpoint)



```
