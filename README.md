## gnome-scale-chooser

### Why?

Starting with GNOME 49, it restricts fractional scaling to fractions with a maximum denominator of 4 (e.g., 125%, 133%, 150%), which excludes several necessary scales, such as 160%.

This program allows you to set various scales.

### Why?

If you set arbiturary 150% or non-dividing scales, it will cause GTK programs to be blurry. 

Wayland's fractional scale is sent to applications via N/120 value, and scale information is stripped to that value.

In non-dividing scales such as 2496x1664@1.5, GNOME automatically adjusts scale to output integer pixels. (In this situation, 1664/1.5 = 1109.33, so actual scale will be 1.499099 to be 1665x1110)

That scale is represented as 180/120 == 1.5 to wayland clients. So for 800 px logical window, GNOME expects 800 * 1.499099 = 1199px, but GTK sends 800 * 1.5 = 1200px buffer, resulting a need for resample, thus blur.

So, we need to use a scale which is well represented as N/120 *after* adjustment, which allows denomiator of 2, 3, 4, 5, and so on.

### Screenshot

<img width="400" alt="img" src="https://github.com/user-attachments/assets/0ca0bcb0-d322-41c3-9cc6-00d783041031" />
