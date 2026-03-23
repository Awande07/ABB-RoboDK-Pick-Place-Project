# ABB-RoboDK-Pick-Place-Project
Complete industrial pick &amp; place simulation for ABB IRB 1200 using RoboDK. Includes TCP calibration, conveyor logic, Python counter, and manual RAPID export for real ABB robots.
---------------------------------------------------------------------------------------------------------------------------
# ABB IRB 1200 Pick & Place Simulation

## Project Overview
Complete industrial automation simulation built in **RoboDK** (free version) demonstrating a full pick-and-place workcell with an ABB IRB 1200 robot. The system includes:
- Input conveyor with part detection
- Machining station with process simulation
- Output conveyor with finished parts
- TCP-calibrated vacuum gripper
- Production counter with Python
- Manual RAPID code export for real ABB robots

**Note:** Built with RoboDK Free Version - all features limited but functional.


## Skills Demonstrated
| Skill | Implementation |
|-------|----------------|
| Robot Programming | ABB RAPID, RoboDK Python API |
| TCP Calibration | 4-point method verified by rotation test |
| Work Objects | Conveyor A, Conveyor B, Machine Station |
| I/O Simulation | Event Manager (Attach/Detach objects) |
| Error Handling | Wait loops, retry logic structure |
| Production Tracking | Python counter with screen display |
| Code Export | Manual RAPID .mod file for ABB IRC5 |


## Repository Structure

ABB-RoboDK-Pick-Place-Project/
├── README.md # This file
├── RoboDK_Station/
├── RAPID_Code/ # ABB robot ready code
├── Python_Scripts/ # Counter logic
├── Documentation/ # Project notes
├── Media/ # Video & screenshots
└── References/ # Learning resources



## Important Note: RoboDK Free Version Limitations

This project was built using **RoboDK Free Version**, which has the following restrictions:

| Feature | Status | Workaround |
|---------|--------|------------|
| Save .rdk files | One file only | Could not save final project |
| Open saved files | Blocked | Project completed in single session |
| Export RAPID | Blocked | Manual code mapping (provided) |

### What's Included as Proof of Completion:

| Evidence | File/Link |
|----------|-----------|
| **Demo Video** | `Media/Demo_Video.mp4` - Full simulation run with counter |
| **Screenshots** | `Media/Screenshots/` - Cell layout, TCP calibration, program running |
| **Python Counter** | `Python_Scripts/update_counter.py` - Working production counter |
| **RAPID Code** | `RAPID_Code/PickPlace_Project.mod` - Manually mapped ABB code |

### How to View the Simulation

The `.rdk` file could not be saved due to free version limits. However, the **video demonstration** shows:
- Full pick & place cycle
- TCP calibration verification
- Python counter updating on screen
- Complete automation logic

To rebuild the project, follow the step-by-step documentation in this repository. All targets, programs, and logic are documented in the `Documentation/` folder.

**Skills demonstrated are visible in the video and code files, not dependent on a saved simulation file.**


##  What the Robot Does

START
↓
Wait 2s (simulate part arrival)
↓
Move to Pick Position
↓
Close Gripper (Attach part)
↓
Move to Machine Station
↓
Open Gripper (Release part)
↓
Wait 3s (Machining process)
↓
Pick from Machine
↓
Move to Conveyor B
↓
Release Part
↓
Counter +1 → Display on screen
↓
RETURN TO START


## TCP Calibration Process

**Method:** 4-point calibration with reference point

**Test:** Rotated Joint 6 (wrist) 90°, 180°, -90°
- **Result:** Z-axis (blue arrow) remained fixed
- **X/Y axes** rotated correctly around TCP

**Accuracy:** Verified no drift during rotation

**Calibration Values:**
| Axis | Offset (mm) |
|------|-------------|
| X | 0 |
| Y | 0 |
| Z | 150 |

---

## Python Counter Script

**File:** `Python_Scripts/update_counter.py`

python

from robodk import robolink

RDK = robolink.Robolink()

# Get current count
count = RDK.getParam('parts_processed')
if count is None:
    count = 0
else:
    count = int(count)

# Increment
count += 1
RDK.setParam('parts_processed', count)

# Display on screen
RDK.ShowMessage(f"Total Parts Processed: {count}", False)

This script runs as a Program Call in the main sequence and updates the 3D view counter.


Learning Outcomes

    Industrial Robot Programming - ABB RAPID syntax, movement types (MoveJ/MoveL)

    TCP Calibration - Critical skill for precision operations

    Work Object Definition - Coordinate systems for conveyors/machines

    I/O Simulation - Event Manager for gripper and process logic

    Production Tracking - Python counter with screen feedback

    Free Version Workarounds - Problem-solving with limited tools

    Documentation - Professional GitHub portfolio structure


Limitations (RoboDK Free Version)

Feature  	        Status
Save/Open station	Works
Add robots/tools	Works
TCP calibration	        Works
Python scripts	        Works
Generate RAPID code     Blocked
Export to robot	        Blocked

Workaround: Manual RAPID code mapping from simulation targets.
Author

Awande Gcabashe

    Applied Mathematics & Computer Science, UNISA

    1-Year Gantry Robotics Experience

    Building robotics portfolio for industrial automation

Contact: awandelindani07@gmail.com

 Acknowledgments

    ABB Robotics for industry standards

    RoboDK for accessible simulation tools
    
    Google Search


 License

Educational use only. RoboDK Free Version used. All code and documentation are original.

Project Completed: 22 March 2026
Tools Used: RoboDK, Python, Notepad
Target Robot: ABB IRB 1200 (IRC5 Controller)
