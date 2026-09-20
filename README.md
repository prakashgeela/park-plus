# park-plus
Design an application that allows users to find and book available parking spots
in a multi-floor parking lot conveniently. The application should also support
secure and seamless online payments.

Scope:
To establish the scope: I’m assuming a multi-floor parking lot with multiple
concurrent entry and exit gates. We need to support diverse vehicle types (bikes, cars, trucks)
mapped to specific spot sizes. When a vehicle arrives at an entry gate, we allocate
the nearest available spot and issue a ticket with a timestamp and license plate.
If no spot is available, entry is rejected. At exit, the ticket is scanned, fees
are calculated using a pluggable pricing strategy (e.g., hourly rates), and upon
payment confirmation, the spot is freed atomically. Are there any specific
constraints around reservations, VIP spots, or EV charging stations we should include,
or should we focus on this core flow?

Requirements:

1. Parking lot and spots:
A. Multi story parking lot, with spots types (SMALL, MEDIUM, LARGE)
B. Spot to vehicle compatibility is strictly 1:1 (for MVP)

2. Entry and spot allocation:
A. At the time of entry scan the plat of the vehicle
B. Assign nearest available spot (if mote then one spot are at equal distance then 
assign prioritize one on lower floor)
C. Generate ticket when you assign a ticket (ticket holds details such as Vehicle number,
Spot number, floor details, entry time stamp)
D. If appropriate slot not available, reject the entry with a clear message

3. Exit and bill generation:
A. Scan ticket
B. Generate bill as per our pricing strategy

4. Payment and spot Release:
A. Support multiple payment methods (UPI, CARD, CASH)
B. Release the spot once payment is done

Non-Functional Requirements:
1. Concurrency & Thread safety:
A. Multiple entry and exit gates operate simultaneously across different threads.

2. Low Latency / High Performance:
A. Spot allocation must be optimized to avoid an exhaustive linear O(N) scan across
all spots on all floors. Lookup and assignment must complete in O(1) or O(log N) 
time.
B. Fine-grained locking

3. Extensibility & Modularity (SOLID Principles)
4. Data Integrity & Immutability
