# Frequently Asked Questions

## Can I use this project for coursework?

Yes. You can use this project for learning and coursework if you provide clear attribution. Please review [LICENSE](LICENSE) and follow your institution policy on academic integrity.

## What is this project and what does it do?

This is a 4x4x4 NeoPixel LED cube project built with an Arduino Uno. I designed it to run multiple animation modes, react to ambient light with an LDR sensor and provide button-based interaction for power and mode changes.

## What hardware do I need to build the same setup?

I list the full component breakdown in [hardware/README.md](hardware/README.md). At minimum you need an Arduino Uno, 64 WS2812B LEDs, a stable 5V power supply, two buttons, an LDR, a buzzer and basic wiring materials.

## What power supply should I use?

Use a stable 5V supply with enough current headroom. The documentation recommends at least 2A for this setup and higher current capacity is safer when driving many LEDs at high brightness.

## Where can I see the build photos and demo media?

Use [media/Gallery.md](media/Gallery.md) for a visual walkthrough and embedded demo video. You can also browse file details in [media/README.md](media/README.md).

## Where can I see all build photos?

Open the full gallery: [media/Gallery.md](media/Gallery.md).

## Where is the Arduino code?

The main sketch is here: [software/neopixel_cube/neopixel_cube.ino](software/neopixel_cube/neopixel_cube.ino).

## Where is the software explanation?

See [software/README.md](software/README.md) for architecture and function details.

## How do I upload and run the code on my board?

Open the sketch in Arduino IDE, select Arduino Uno, select the correct COM port, compile and upload. I summarized this in [software/README.md](software/README.md).

## Which Arduino library is required?

The project depends on the Adafruit NeoPixel library. Install it from Arduino Library Manager before compiling.

## Which LED patterns are included right now?

The current build includes Colour Wipe, Smooth RGB Fade, Fire Effect and Rainbow Cycle.

## How does brightness control work?

The LDR sensor reads ambient light and the firmware maps that value to LED brightness. In the current setup, brighter surroundings reduce LED intensity and darker surroundings increase it.

## What do the buttons do?

One button toggles system power and one button cycles patterns. The firmware uses edge detection with debounce handling to avoid repeated accidental triggers.

## Can I monitor values while the cube is running?

Yes. I print runtime diagnostics over serial at 9600 baud, including power state, selected pattern and mapped brightness values.

## What baud rate should I use in Serial Monitor?

Use 9600 baud to match the firmware configuration.

## The LEDs are not lighting correctly. What should I check first?

Check power wiring first, then verify shared ground between Arduino and LED power, then confirm the data line from Arduino to the first LED. Also confirm your LED order, solder joints and orientation.

## The buttons are not responding consistently. What should I check?

Check button wiring, pull-up or pull-down configuration and physical switch quality. If needed, increase debounce delay slightly in the code.

## Can I use this code with a different LED count or cube size?

Yes. Update the LED count constants, test current draw and validate each pattern with the new geometry.

## Why is my cube dimmer than expected?

Brightness is intentionally adaptive. The LDR can reduce LED output when ambient light is high. Check sensor placement and mapping values if you want a brighter default.

## Why do animations sometimes look slow?

Pattern speed is controlled by delay values and timing logic in each effect. Reducing delay values can make transitions faster, but too little delay can reduce visual smoothness.

## Where is the hardware documentation?

See [hardware/README.md](hardware/README.md) for components and wiring details.

## Can I adapt this for a 5x5x5 cube?

Yes. Update the LED count, revise power planning and adjust pattern logic for the larger matrix.

## Can I add more LED patterns?

Yes. Add a new pattern function and include it in the mode switch in the main loop.

## Can I contribute improvements?

Yes. I welcome improvements through issues and pull requests. Include a clear summary, test notes and screenshots or video when the change affects visuals.

## Which branch workflow should contributors follow?

Use a topic branch from main, use clear type-prefixed commit messages and open a PR with summary, changes and test steps.

## Where can I find a full project overview in one place?

Start with [README.md](README.md), then use the section links for software, hardware, media and FAQ.

## How do I ask questions that are not covered here?

Please open an issue in this repository with your setup details and question.

## Can I contact you directly?

Yes. Email me at eng@isaacadjei.me.

## Last Updated

May 2026
