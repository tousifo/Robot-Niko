# Robot Niko

A life-size, 3D-printed humanoid assistant built in 2022 at the FabLab of the
Deputy Commissioner's Office, Cumilla. I co-developed Niko with Jewel Nath,
Shanjit Mondol, Md Mohiuddin Khan Mahin and Anik Chakraborty. It talks, knows
the people it has met, follows faces with its head, and moves 27 servos across
its head, eyes, jaw, arms and fingers — all from Python on a Raspberry Pi.

![Niko, finished, in November 2022](docs/media/robot-niko-2022-11-29-full-robot.jpg)

**Niko working, December 2022** (videos on YouTube, with sound):

| | |
|---|---|
| <a href="https://youtu.be/6iEj3AY1AlA"><img src="docs/media/robot-niko-2022-12-06-head-follows-face.gif" width="380" alt="Niko's head turning to follow a person"></a><br>[Its head follows a face](https://youtu.be/6iEj3AY1AlA) (53 s) | <a href="https://youtu.be/Iotg0E8AKoU"><img src="docs/media/robot-niko-2022-12-07-introducing-itself-poster.jpg" width="380" alt="Niko introducing itself"></a><br>[It introduces itself](https://youtu.be/Iotg0E8AKoU) (41 s) |

## What it does

- **Talks.** It wakes to "Hey Niko", a Porcupine wake word, and holds spoken
  conversations from 51 known questions in
  [`config/conversation.yaml`](config/conversation.yaml); its jaw moves as it
  speaks, and an online assistant answers what it doesn't know.
- **Knows faces.**
  [`src/vision/recognise_faces.py`](src/vision/recognise_faces.py) recognises
  the people it was trained on with `face_recognition` and a KNN classifier,
  and [`src/face_greeting.py`](src/face_greeting.py) greets each one by name
  and shakes their hand.
- **Follows a face.**
  [`src/vision/follow_face.py`](src/vision/follow_face.py) finds a face with
  OpenCV and turns the head toward it
  ([video](https://youtu.be/6iEj3AY1AlA)).
- **Moves.** 27 servos turn its head and eyes and move its jaw, shoulders,
  arms, wrists and fingers, driven by two Adafruit 16-channel servo drivers
  ([servo map](#servo-map)).
- **Starts by itself.** A systemd service starts it at boot.

## Technical report

**[Robot Niko: A Life-Size 3D-Printed Humanoid Assistant on a Raspberry Pi —
System Design and Build](docs/report/robot-niko-report.pdf)** (October 2026,
15 pages): the build, the electronics, the software, the motion, the voice and
the vision, with 13 diagrams. By Jewel Nath, Shanjit Mondol, Tousif Bin Parves,
Md Mohiuddin Khan Mahin and Anik Chakraborty; on Zenodo as
[doi:10.5281/zenodo.23719561](https://doi.org/10.5281/zenodo.23719561). The
report's source and diagrams are in [docs/report/](docs/report/README.md) and
[docs/diagrams/](docs/diagrams/README.md).

## The design

[Niko is based on InMoov](https://inmoov.fr/), Gaël Langevin's open-source,
life-size robot — Niko runs InMoov's head, torso, arms and hands on a stand,
driven by a Raspberry Pi with its own Python code instead of InMoov's usual
Arduino and MyRobotLab. The team's working 3D models for every printed part —
343 STL files, organized by body part — live in [cad/](cad/README.md).
Niko's 3D model, made from InMoov's parts in Blender:

| | | |
|---|---|---|
| <img src="docs/media/robot-niko-2022-08-model-front.jpg" height="220" alt="Niko's model from the front"> | <img src="docs/media/robot-niko-2022-08-model-side.jpg" height="220" alt="Niko's model from the side"> | <img src="docs/media/robot-niko-2022-08-model-back.jpg" height="220" alt="Niko's model from the back"> |

## Servo map

<a href="docs/diagrams/robot-niko-servo-map.pdf"><img src="docs/diagrams/robot-niko-servo-map.png" width="560" alt="The servo map on a front view of Niko"></a>

Each servo's channel and starting angle, as set in
[`config/servo-configuration.yaml`](config/servo-configuration.yaml), the file
[`src/move.py`](src/move.py) loads at start. Channels 0–15 sit on the first
PCA9685 board (0x40); channels 16–26 are the second board's (0x41) channels
0–10.

## Credits

Built by the team at the FabLab of the Deputy Commissioner's Office, Cumilla.
The full build log, electronics notes, printing notes and software
documentation live in the upstream repository,
**[jewel-nath/robot-niko](https://github.com/jewel-nath/robot-niko)** — this
fork is my copy of the project as a co-developer.
