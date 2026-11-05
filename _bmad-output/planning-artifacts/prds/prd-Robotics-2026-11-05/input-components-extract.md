# Candidate hardware-list source extract

Source: `D:/Uni/Projects/Robotics/Components -.pdf`, 3 pages. Candidate doctor hardware list; attribution, mandatory status, and application to this project remain unconfirmed by the user. Extracted with pdfplumber and visually checked against all three rendered pages. No source links were followed and prices were not verified.

| No. | Exact printed component name | QTY | PDF page |
| --- | --- | ---: | --- |
| 1 | Robot Car Chassis Kit 1 Layer (4WD) | 1 | 1 |
| 2 | ESP32-CAM OV2640ESP32-CAM OV2640 Camera CH340 | 1 | 1 |
| 3 | L298 Motor Driver Module | 1 | 1 |
| 4 | Servo Motor SG90 | 1 | 1 |
| 5 | Ultrasonic Sensor (HC-SR04) | 1 | 1 |
| 6 | Ultrasonic Sensor HC-SR04 Holder White | 1 | 1–2 (image continues on p. 2) |
| 7 | 18650 Rechargeable Li-ion Battery (3.7V , 1800mAh) Flat | 6 | 2 |
| 8 | Charger for 2x18650 Li-ion Battery | 1 | 2 |
| 9 | Battery Holder ( 3 x 18650 ) (3.7v) | 1 | 2 |
| 10 | LED Red Color (5mm) | 5 | 2 |
| 11 | Resistor (220 ohm , 1/4W) | 5 | 2 |
| 12 | Resistor (1 Kohm , 1/4W) | 5 | 2 |
| 13 | Breadboard Soldless 400 Tie-points | 1 | 2–3 (image continues on p. 3) |
| 14 | Breadboard Soldless 170 Tie-points SYB-170 | 1 | 3 |
| 15 | Male to Male Jumper Wire 1 Pin (20cm) | 30 | 3 |
| 16 | Male to Male Jumper Wire 1 Pin (10cm) | 10 | 3 |
| 17 | Male to Female Jumper Wire 1 Pin (20cm) | 20 | 3 |
| 18 | Female to Female Jumper Wire 1 Pin (20cm) | 10 | 3 |
| 19 | Micro USB Cable | 1 | 3 |

## Alternatives and obligation

The PDF is a component table with names, images, vendor links, prices, quantities, and totals. It contains no explicit mandatory/optional labels, substitution rules, alternatives, functional requirements, or explanation of component purpose. The final page lists additional vendor homepages; these are not component alternatives.

## Reconciliation needed against the pasted overview

- The PDF includes an HC-SR04 ultrasonic sensor and holder (p. 1), whereas the overview explicitly excludes ultrasonic obstacle detection. Component possession does not establish required use; ask which source governs scope.
- SG90 servo is listed (p. 1) without a stated function; the overview does not specify a servo-driven feature.
- Arduino Uno and HC-05, explicitly named in the overview, are absent from the PDF. Absence does not establish replacement or removal. Laptop/webcam and PlayStation controller are also absent.
- The PDF specifies a 4WD chassis and ESP32-CAM, consistent with the overview's four-wheel robot and example camera. The printed driver name is L298; the overview names L298N. No engineering equivalence is inferred here.
- Battery/charger/holder entries add component detail but define no approved power architecture or runtime acceptance criterion.

## Source quality and limits

- Row 14 (p. 3) prints unit price 10, QTY 1, total 25: internal arithmetic mismatch preserved, not corrected.
- No currency or document date is printed. The apparent duplicated wording of row 2 is printed in the source and preserved.
- Poppler reported missing display fonts (Symbol/ArialUnicode), but all component labels, quantities, and page layout were readable in the rendered pages and matched text extraction.
- This extraction makes no purchasing, compatibility, electrical-safety, or implementation recommendation.
