# Food Warehouse Automation with Robotic Arm

This project uses a **simple robotic arm** to move food items from **storage** to the **picking zone**.
It shows how the robot works, its parts, the area it can reach, and step-by-step instructions to operate it.

---

## 1. Warehouse Zones
- **Storage Zone:** Where food items are kept.  
- **Picking Zone:** Where items are collected for delivery.  
- **Packing Zone:** Where items are packed into boxes.  

---

## 2. Robot Description
- **Robot Type:** Simple 3-DOF robotic arm (base, shoulder, elbow/gripper).  
- **Motors:** 3 servo motors:  
  1. Servo 1 → Base rotation (left/right).  
  2. Servo 2 → Arm up/down (shoulder).  
  3. Servo 3 → Gripper open/close (elbow).  
- **Controller:** Arduino Uno board.  
- **Input:** 3 push buttons (each button controls one motor).  
- **Output:** 3 LEDs (show motor activity).  
- **Power:** Battery pack (5V).  

---

## 3. Working Area
- **Working Envelope:** Maximum physical space the arm can reach (semi-circle radius 20 cm from base).  
- **Operating Area:** Safe task region (table surface 15 × 15 cm).  
- **Dead Zone:** Restricted area near base (inner circle radius 5 cm).  

ASCII Diagram:
```text
     Dead Zone (5cm)
       ________
      /        \
     /          \
    |            |  <- Operating Area (15x15cm)
     \          /
      \________/
        ^
    Base / Working Envelope (radius 20cm)
```

---

## 4. Algorithm Steps (How the Robot Works)

1. **Initialization:**  
   - Power on Arduino.  
   - Set all motors to default position (arm straight forward).  
   - Turn all LEDs OFF.  

2. **Wait for Input:**  
   - The robot listens for button presses.  
   - Each button is mapped to one motor:  
     - Button 1 → Base rotation (left/right).  
     - Button 2 → Arm up/down (shoulder).  
     - Button 3 → Open/close gripper.  

3. **Movement Execution:**  
   - When a button is pressed:  
     - Rotate the corresponding motor in small steps.  
     - Turn ON the corresponding LED.  
   - Release button → motor stops and LED turns OFF.  

4. **Working Area Check:**  
   - Before moving, check if new position is inside **working envelope** → allow motion.  
   - If outside envelope → block motion, blink LED 3 times (error).  
   - If inside **dead zone** → gripper motion is blocked.  

5. **Gripper Operation:**  
   - Press Button 3 → if open → close; if closed → open.  
   - Only allow gripper to work inside **operating area**.  

6. **Loop:**  
   - Repeat steps 2–5 continuously until power off.

---

## 5. Example Scenario
- Press Button 1 → base rotates right 10°.  
- Press Button 2 → arm lowers toward table.  
- Robot checks position → inside operating area → continue.  
- Press Button 3 → gripper closes on object.  
- Press Button 1 → robot rotates to move object.  
- Press Button 3 → gripper opens → object placed.  
- Return arm to **Home Position**.

---

## 6. Summary
- The robot uses **3 servo motors** and Arduino for control.  
- **Working area** is clearly divided:  
  - **Working Envelope:** max reach of the arm.  
  - **Operating Area:** safe task area.  
  - **Dead Zone:** restricted area near the base.  
- The algorithm ensures the robot operates safely and completes pick-and-place tasks step by step.
