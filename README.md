# arduino

## Dependencies
- [mise](https://mise.jdx.dev): installs arduino-cli and Python, and runs the project tasks
- xxd: converts sketch data files into C headers

## Setup

```
mise install
mise run setup
```

`setup` creates `.env` from `.env.example` and installs the Python packages the ESP32 upload tools need. Set `PORT` in `.env` to the board's serial port.

## Tasks

| Task | Purpose |
| --- | --- |
| `mise run arduino:compile <sketch>` | Compile a sketch into `.build/<sketch>` |
| `mise run arduino:upload <sketch> [--port <port>]` | Upload the compiled sketch |
| `mise run arduino:monitor [--port <port>] [--baudrate <baud>] [--describe]` | Open the serial monitor |
| `mise run arduino:run <sketch> [--port <port>]` | Compile, upload and monitor |
| `mise run arduino:spiffs <sketch> [--port <port>]` | Flash `<sketch>/data` as a SPIFFS image to an ESP32 |
| `mise run clean` | Remove build output and installed cores and libraries |

`--port` defaults to `PORT` from `.env`.

## Sketch profiles

Each sketch folder has a `sketch.yaml` whose default profile pins the board, the core and the libraries. `arduino-cli compile` installs them into `.arduino/` on first use.

To add a library to a sketch:

```
mise exec -- arduino-cli profile lib add '<Library>@<version>' --sketch-path <sketch>
```

Libraries in `library/` are shared through `- dir: ../library` in the profile.

## Sketches

| Sketch | Board |
| --- | --- |
| blecar | `esp32:esp32:esp32` |
| blejoystick | `esp32:esp32:esp32c3` |
| blink | `arduino:avr:nano` |
| immortanjoe | `esp32-bluepad32:esp32:esp32` |
| io2pwm | `digistump:avr:digispark-tiny` |
| lcd | `arduino:avr:nano` |
| nux | `arduino:avr:nano` |
| omnidirectional | `esp32-bluepad32:esp32:esp32` |
| servo | `arduino:avr:nano` |
| strandbeest | `arduino:avr:nano` |
| webspy | `esp32:esp32:esp32cam` |

thebulletfarmer has no profile: it includes `this_wheelchair.h`, which is not in the repository.
