# Lost and Found — Supporting Context

## Source status

The user-supplied overview established the concept. Interview answers refine behavior/scope. The hardware list supplied in round 8 governs procurement. The workspace PDF was explicitly rejected as the prescribed list; its sensor/servo entries and prices are not requirements or purchasing authority.

## Software proposals from the overview

The overview proposes Python, OpenCV/MediaPipe gestures, YOLOE reference-image visual prompting, Pygame controller input, Arduino IDE, and local storage. The frontend is unspecified. These are candidate implementation choices, not validated compatibility claims or approved architecture. Select mechanisms during architecture within PRD constraints.

## Hardware detail

The authoritative list includes 4WD chassis, L298N, Arduino Uno R3, ESP32-CAM OV2640, HC-05, 18650 cells, holder/charger/BMS, 5V DC-DC regulator, switch, breadboard, wires, and Micro USB cable. Exact quantities/ranges are in the PRD. Exact battery configuration, power/wiring design, and communication arrangement remain unresolved; no configuration has been selected here.

The Windows laptop has a dedicated NVIDIA GPU; exact specifications remain to be supplied. Laptop webcam and PS4/PS5 controller support are required. Their model/availability remain dependencies. Component inclusion does not establish compliance with stop, latency, coverage, or endurance targets.

## Operational trade-offs

- Navigation remains manual. No autonomous navigation, obstacle avoidance, mapping, GPS, servo functions, or retrieval.
- Similarity alerts require human review and do not promise unique-item identity.
- Both control modes are required; switching requires ending the session.
- Wired demonstration is permitted only if fixed-desk connected-room operation is preserved.
- Registration-based expiry can delete recent search evidence attached to an older record. Searches do not extend retention. An active session may finish first, extending retention while that session remains active; no automatic session time limit exists.
- Another search for a Found belonging requires a new registration and independent retention lifetime.

## Contextual research

`research-context.md` records official teleoperation/visual-prompting sources. These establish context only, not this product's feasibility, accuracy, novelty, or acceptance performance.