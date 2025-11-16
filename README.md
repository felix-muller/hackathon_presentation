# 🎤 5-Minute Demo Script (Markdown Version)

## **0:00–0:20 — Introduction**
Hi everyone.
Many real-world missions — from battlefield intelligence to search-and-rescue or environmental monitoring — require guaranteeing full coverage of an area. Missing even a small region can mean missing critical information. Our system focuses on enabling a single operator to reliably achieve complete coverage of an area of interest using multiple fixed-wing UAVs through a simple web interface.

The two key things to watch for are:

1. The **realistic fixed-wing simulation** running in PX4 and Gazebo  
2. The **guaranteed coverage** achieved through real-time Voronoi partitioning

---

## **0:20–1:20 — Realistic Fixed-Wing Simulation**
Before we show the interface, here’s one of the aircraft itself flying in the baylands area. -> show follow the plane in gazebo

This is a fully simulated fixed-wing UAV running in **PX4 SITL** with **Gazebo**, meaning that this can be tested on a real drone without any more work. 
Unlike quadrotors, fixed-wings can’t hover, can’t pivot, and must maintain minimum airspeed and large turning radii. But they do have much better range and can cover big areas.

Everything we show today is constrained by real aerodynamics — so when we later assign a task, you’ll see PX4 fly **realistic, feasible trajectories** rather than simplified point-to-point motion.

---

## **1:20–2:40 — Overview of the Web Interface**
Now let’s switch to the operator interface.

Here you see:

- The map with the aircraft position  
- Each drone’s camera feed  

The idea is that the operator gives only **high-level intent** by choosing the outer points of the area that he or she wants to cover. 
The UAVs autonomously handle all low-level flying and voronoi coverage logic.  
This keeps operator workload low even as we scale the number of drones.

But we still wanted to leave the possibility for lover level control and thats why we kept QGC running in the background where the operator can get deep into the setting of each drone.

---

## **2:40–3:40 — Main Event: Guaranteed Coverage**
Let’s walk through an example.

Suppose the operator wants full coverage of this region.  
*(Select or draw the polygon in the interface.)*

As soon as I confirm, the system generates a **Voronoi partition** covering exactly the selected area.  
Each drone receives its own region, and together these regions **optimally guarantee gap-free, complete coverage**.

There are no blind spots and this is a **mathematical guarantee**, not a heuristic.  

---

## **3:40–4:20 — Showing Realistic Flight Execution**
Now these partitions are converted into realistic lawn mower, flyable coverage paths that obey fixed-wing dynamics.

Watch how the UAV flies the sweep pattern:

- Smooth continuous forward motion  
- Wide arcs  
- Banked turns that PX4’s controller can truly execute  

So the coverage is not just geometric — it's dynamically **feasible for a real fixed-wing aircraft**.

---

## **4:20–5:00 — Dynamic Reallocation + Closing**
To show robustness, I’ll adjust the coverage area.  
*(Resize or move the selected region.)*

You can see the Voronoi partitions update instantly, and the UAV replans in real time — still guaranteeing complete coverage.

This demonstrates the autonomy split:

- **The operator decides what should be covered**  
- **The UAV decides how to fly it safely and realistically**

And that’s the core contribution:

A scalable, RTS-style interface running on top of a **realistic fixed-wing PX4 simulation**, combined with a coverage planner that can **guarantee full coverage** of any user-selected area.

Mark focused on the front end, gazebo and the coverage control algorithms and Felix focused more on wiring the whole thing up with ROS2 and PX4. We built it all today.

**Thank you.**
