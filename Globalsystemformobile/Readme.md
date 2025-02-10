# Call Flow in a GSM Network: From Caller to Receiver via Booster, BSC, and Core Network

This document provides a detailed explanation of how a call is processed in a GSM network, passing through various network components such as boosters, Base Station Controllers (BSC), the core network, and the backhaul.

## 1. Mobile Phone (Caller) Initiates a Call
- The caller dials a number, and their phone generates a **radio frequency (RF) signal**.
- This RF signal is transmitted to the nearest **cell tower (Base Transceiver Station - BTS)**.

## 2. Signal Passes Through a Booster (If Needed)
- If the caller is in a weak signal area, a **booster (repeater or signal amplifier)** enhances the signal strength.
- The booster **captures, amplifies, and retransmits** the RF signal to ensure better connectivity to the cell tower.

## 3. Base Transceiver Station (BTS) Receives the Signal
- The BTS handles the **radio link** with mobile phones.
- It converts the RF signal into a **digital signal** and forwards it to the Base Station Controller (BSC).

## 4. Base Station Controller (BSC) Manages the Call
- The BSC is responsible for:
  - Controlling multiple BTSs.
  - Assigning radio channels.
  - Managing handovers (switching calls between BTSs if the caller moves).
- The BSC forwards the call data to the Mobile Switching Center (MSC) in the **core network** via a **backhaul**.

## 5. Backhaul Transmits the Signal to the Core Network
- A **backhaul** is the communication link between the **BSC and the core network**.
- It can be wired (fiber optic, microwave) or wireless.
- The backhaul ensures efficient transmission of voice and data traffic to the Mobile Switching Center (MSC).

## 6. Core Network Processes and Routes the Call
- The **Mobile Switching Center (MSC)** verifies the caller's identity and determines the best route for the call.
- The MSC connects to the **Public Switched Telephone Network (PSTN)** or another mobile network to reach the recipient.

## 7. Call Reaches the Recipient’s Network
- If the recipient is on the same network:
  - The MSC routes the call directly to the appropriate BSC and BTS near the recipient.
- If the recipient is on a different network:
  - The call is sent through the **Interconnect Gateway** to the recipient’s network.

## 8. Recipient’s Mobile Phone Rings
- The BTS nearest to the recipient’s location transmits the signal.
- The recipient’s phone rings, and once answered, a dedicated channel is established.
- The conversation continues with real-time signal exchange between the caller and receiver through the network.

## Summary of Call Path
1. **Caller’s Phone → BTS → Booster (if needed) → BSC → Backhaul → MSC (Core Network)**  
2. **MSC routes call to recipient’s network → Backhaul → BSC → BTS → Recipient’s Phone Rings**  

This process ensures a **seamless and efficient communication experience**, leveraging network elements such as **boosters, BTS, BSC, core network, and backhaul** for connectivity and signal transmission.