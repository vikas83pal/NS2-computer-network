# NS2-computer-network

# To work with NS2 (Network Simulator 2) for the tasks you've outlined, you'll need to follow a series of steps to set up simulations, run them, and analyze the results. Below are the steps and example scripts for each of the tasks you mentioned.

- NS2 Simulator - Introduction

NS2 is a discrete event simulator targeted at networking research. It provides a simulation environment for various protocols and network scenarios. 
The main components of NS2 include:

    - Simulation Scripts: Written in TCL (Tool Command Language).
    - Network Protocols: Supports various protocols like TCP, UDP, etc.
    - Graphical Output: Uses tools like AWK and MATLAB for data analysis and visualization.
    
    
# Simulate to Find the Number of Packets Dropped

```
# Create a simulator object
set ns [new Simulator]

# Create nodes
set n1 [$ns node]
set n2 [$ns node]

# Create a link with a limited bandwidth and buffer size
$ns duplex-link $n1 $n2 1Mb 10ms DropTail

# Create a traffic generator (UDP)
set udp [new Agent/UDP]
$ns attach-agent $n1 $udp

# Create a sink to receive packets
set sink [new Agent/Null]
$ns attach-agent $n2 $sink

# Connect the UDP agent to the sink
$ns connect $udp $sink

# Start sending packets
$udp send 1000 0

# Run the simulation
$ns run

```

# Simulate to Find the Number of Packets Dropped by TCP/UDP

```
# Similar to the previous script but using UDP
# Add a counter for dropped packets

```

- For TCP:
```
# Create a TCP agent
set tcp [new Agent/TCP]
$ns attach-agent $n1 $tcp

# Create a sink to receive packets
set sink [new Agent/Null]
$ns attach-agent $n2 $sink

# Connect the TCP agent to the sink
$ns connect $tcp $sink

# Start sending packets
$tcp send 1000 0

# Run the simulation
$ns run

```

# Simulate to Find the Number of Packets Dropped due to Congestion
- You can modify the buffer size in the link to simulate congestion. For example:
```
# Create a link with a smaller buffer size
$ns duplex-link $n1 $n2 1Mb 10ms 50

```


# Simulate to Compare Data Rate & Throughput
- you can measure throughput by calculating the amount of data successfully received over time. Use the following code snippet to log the data:

```

# After the simulation, log the number of bytes received
set bytes_received 0
proc log_bytes {bytes} {
    global bytes_received
    set bytes_received [expr {$bytes_received + $bytes}]
}

# Connect the sink to log the received bytes
$ns at 0.1 "log_bytes [expr {$sink set bytes}];"

$ns run
puts "Throughput: [expr {$bytes_received / 10.0}] bytes/sec"

```

# Simulate to Plot Congestion for Different Source/Destination

- You can create multiple source-destination pairs and plot the congestion by varying the traffic load. Use a loop to create multiple nodes and links.

# Simulate to Determine the Performance with respect to Transmission of Packets

- you can track the end-to-end delay and packet delivery ratio by adding more logging in your script.
```

# Track delays and packet delivery
proc track_delay {src dst} {
    # Logic to track delays
}

# Set up your simulation to include tracking
$ns at 0.1 "track_delay $n1 $n2"
```

# Running the Simulation

- To run any of these scripts:

    - Save the script as a .tcl file, e.g., simulation.tcl.
    - Open a terminal and navigate to the directory containing the script.
    - Run the simulation using the command:
    
    ```
    ns simulation.tcl
    
    ```
