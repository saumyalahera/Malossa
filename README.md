# Malossa

**Write shaders in a simple language and see them render instantly on your Mac.**

Malossa is a beginner-friendly shader language based on the research paper *"Malossa Programming Language"* by Saumya Lahera. This repository hosts the **Malossa app for macOS** as downloadable releases. The source code is not public.

## Download

1. Go to [**Releases**](../../releases) and download the latest `Malossa.dmg`.
2. Open the DMG and drag **Malossa** into **Applications**.
3. Launch Malossa from Applications.

**Requirements:** a Mac with Apple Silicon (M1 or later), running macOS 26.5 or later.

### If macOS says Malossa "can't be opened"

Malossa isn't signed with an Apple Developer ID yet, so the first time you open it, macOS blocks it. To allow it:

1. Try to open Malossa once, then click **Done** on the warning.
2. Open **System Settings → Privacy & Security**.
3. Scroll down to the message about Malossa and click **Open Anyway**.
4. Confirm with your password or Touch ID, then click **Open**.

You only need to do this once.

## What you can do

- Write a shader on the left and watch it render live on the right as you type.
- See errors underlined in your code, with plain explanations.
- Create projects, add files, and save your work. Projects autosave.
- Use `print` to inspect values at the pixel under your mouse.
- Switch between light and dark themes, and pick a code font in Settings (⌘,).

## A first shader

```
// animated rings
fc ring (float d)(float t)
    return 0.5 + 0.5 * sin(d * 40 - t * 3);
end

fc shade (float2 uv)
    float2 p = uv - 0.5;
    float d = length(p);
    float3 col = float3(0, 0, 0);
    loop i 0 to 3
        col = col + 0.25 * ring(d + i * 0.1, time);
    end
    return float4(col, 1);
end mf
```

## Language at a glance

| Write this | It means |
|---|---|
| `fc name (int a b)(float c) … end` | A function. Parameters are grouped by type. |
| `end mf` | Marks the main function, which is the shader that draws each pixel. |
| `float a b c;` | Declares several variables at once. |
| `loop i 0 to 10` / `loop k 10 to 0` / `loop x > 1` | Count up, count down, or loop while a condition holds. |
| `array a;` `scan a 10;` `a->3` | Arrays, and reading or writing an element. |
| `-6` `-bl` `-e` | Comment out the next 6 lines, up to the next blank line, or up to the next `end`. |
| `pref 2(x)` | Calls function number 2. |
| `wc` `fc` `lc` `fs` `gp` `gmf` | Word count, function count, line count, function size, function number, main function name. |
| `print x;` | Shows the value of `x` at the pixel under your mouse. |
| `time` `resolution` `pixel` | Built-in values the app provides. |

## Feedback

Found a bug or have an idea? Open an [issue](../../issues).

## Credits

- Language design: Saumya Lahera, *Malossa Programming Language*.
- [Departure Mono](https://departuremono.com) font, used under the SIL Open Font License.

© 2026 Saumya Lahera. All rights reserved.
