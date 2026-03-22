
- 📸 **Screenshot 1: The Final LTspice Schematic.**  
	feedback capacitor is set to **22p** (which we calculated is perfect for our real-world MCP6001 chip).
    
- 📸 **Screenshot 2: Transient Response (Uncompensated).**  
    capacitor to 0.1p (basically zero), "Uncompensated TIA showing instability and ringing."
    
- 📸 **Screenshot 3: Transient Response (Compensated).**  
    capacitor back to 22p, beautiful, smooth, flat curve. "Properly compensated TIA using calculated 22pF feedback capacitor."
    
- 📸 **Screenshot 4: AC Frequency Response (Bode Plot).**  
    The graph  generated using the .ac command. "AC Analysis proving flat gain and calculating amplifier bandwidth."