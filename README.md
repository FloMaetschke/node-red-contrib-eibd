node-red-contrib-eibd
==========================

KNX/eibd nodes for node-red. Uses the eibd binding for Node.JS (https://github.com/andreek/node-eibd). It will include:

'eibd-controller' : a unique CONFIG node that holds connection configuration for eibd and will acts as the encapsulator for KNX access. As a node-red 'config' node, it cannot be added to a graph, but it acts as a singleton object that gets created in the the background when you add an 'eibd' or 'eibd-device' node and configure it accordingly.

-- 'eibd-out' : KNX/EIB output node that can send KNX to arbitrary GA's and datatypes, so it can be used with function blocks.

-- 'eibd-in': KNX/EIB listener node, who emits flow messages based on activity on the KNX bus:

Both use the same message format, an example message follows:

{ "topic": "knx: write", "payload": { "srcphy": "1.1.100", "dstgad": "5/0/2", "dpt": "DPT1", "value": 0 } }

 -- topic is: *"knx: (telegram type)" where (telegram type) is 'read' (read requests), 'response' (to read requests) and 'write' (to update GA's)

 -- payload contains:

 --- srcphy: source physical address (the device that sent the KNX/EIB telegram) - this information is only emitted by eibd-in, and will be ignored by eibd-out (no address spoofing, you naughty haxx0r!)

 --- dstgad: destination group address (the function that this telegram refers to eg. front porch lights) - REQUIRED

 --- dpt: datapoint type (1 for booleans, 5 for 4-bit dimming setpoints etc) - defaults to 1 for boolean on/off GA's

 --- value: the destination group address's value conveyed in the telegram - REQUIRED
