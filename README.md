# Building ZMK for the Tidbit

Some general notes/commands for building standard Tidbit layouts from the assembly documentation.

## Standard "Non Dense" Build

```

west build -p --board nice_nano -d build/tidbit/default -- -DSHIELD=tidbit

```

## Dense "19 keys" Build

```

west build -p --board nice_nano -d build/tidbit/19_keys -- -DSHIELD=tidbit -DKEYMAP_FILE=${PWD}/boards/shields/tidbit/tidbit_19key.keymap

```

## Underglow / LEDs

If you built your tidbit without the underglow leds, you'll need to add the following to one of the above commands.

```

-DCONFIG_ZMK_RGB_UNDERGLOW=n -DCONFIG_WS2812_STRIP=n

```

## Encoder Notes

If you built your tidbit without encoders, you'll need to add the following to one of the above commands.

```

-DCONFIG_EC11=n -DCONFIG_EC11_TRIGGER_GLOBAL_THREAD=n

```

## OLED Builds

If using an OLED screen you'll need to include the following at the *end* of one of the above commands to build support for the OLED into the firmware.

```
-DZMK_DISPLAY=yes

```

You'll also need to add the following to your keymap file.

```

&pro_micro_i2c {
	status = "okay";
};

```

## Graphcs Library

If you'd like to use ```lvgl``` with an OLED please append *BOTH* the above OLED parameter and the below to one of the above commands.

```

-DLVGL=yes

```
