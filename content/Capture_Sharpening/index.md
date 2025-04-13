---
title: Capture Sharpening
contributors:
  - XavAL
---

<div class="pagetitle">

Capture Sharpening

</div>

## What is it

The Capture Sharpening tool helps recover details lost due to in-camera
blurring, which can be caused by
[diffraction](https://www.cambridgeincolour.com/tutorials/diffraction-photography.htm),
[the anti-aliasing
filter](https://en.wikipedia.org/wiki/Anti-aliasing_filter), or other
sources of [Gaussian-type
blur](https://en.wikipedia.org/wiki/Gaussian_blur).

It is applied to the raw file immediately after demosaicing and modifies
the data in linear gamma to limit halo generation. This means that it
will only work on raw files .

## Is it the definitive sharpening tool?

Even though you can get excellent results with the default settings, it
is not meant to be the only tool used for sharpening. Rather, it should
be considered as a necessary first step to improve the distinction
between noise and details prior to the image being processed by other
tools further down the line. It can therefore be used in conjunction
with other sharpening methods such as the Unsharp Mask or RL
Deconvolution. The combination of sharpening tools will depend on what
you are trying to achieve and what is acceptable by way of artifacts.

It will also depend on the final size of the image and whether it is
going to be printed or not. This is because in both situations you may
be able to apply stronger sharpening knowing that in the final image it
will not be so apparent.

Here are two typical sharpening tool combinations:

- with the Unsharp Mask: use a small radius and watch out for artifacts
  as you increase the amount of sharpening.
- with RL Deconvolution: find an appropriate radius value (through trial
  and error to avoid halos) and choose a high contrast threshold so that
  you only enhance the largest details and edges. This will allow you to
  keep artifacts (common with this tool) to a minimum. You will probably
  need to apply a higher amount of sharpening as well.

## How it works (settings)

Any changes in the settings are applied to the whole image, no matter
what the zoom level, so depending on your system, it may take some time
to process the changes. However, once any changes have been made, you
can zoom and pan without any further processing delay.

You can also use the *Sharpening Contrast Mask* to see which details
will be sharpened. Sharpening will occur in the white areas but not in
the black areas. The mask is visible both in the *Preview area* and in
the *Navigator panel*.

### Contrast Threshold

By default the tool analyzes the image and calculates a threshold to
prevent sharpening noise.

You can leave the automatic Contrast Threshold calculation on, or you
can turn it off and set it as required: moving the slider to the right
means that details will have to have higher contrast before they are
sharpened. Higher Contrast Threshold values also reduce the amount of
sharpening applied to noise, which tends to have lower detail contrast.

### Radius

When in-camera blurring occurs, the effective resolution is no longer
dependent on pixel size and instead, has a radius that increases in
proportion to the amount of blurring.

The purpose of this tool is to reduce this blurring by trying to
automatically guess the radius needed to counteract the effect.

<div>

- <figure>
  <img src="/images/Clematis_original.png" title="Clematis_original.png" />
  <figcaption>Clematis_original.png</figcaption>
  </figure>

- <figure>
  <img src="/images/Clematis_good_radius.png" title="Clematis_good_radius.png" />
  <figcaption>Clematis_good_radius.png</figcaption>
  </figure>

</div>

You can also choose to adjust the radius yourself bearing in mind that
if the value is too low, there will not be enough sharpening and if it
is too high, it will lead to strong haloing on the edges. Don’t forget
that you are only trying to undo the in-camera blurring.

<div>

- <figure>
  <img src="/images/Clematis_good_radius.png" title="Clematis_good_radius.png" />
  <figcaption>Clematis_good_radius.png</figcaption>
  </figure>

- <figure>
  <img src="/images/Clematis_bad_radius.png" title="Clematis_bad_radius.png" />
  <figcaption>Clematis_bad_radius.png</figcaption>
  </figure>

</div>

Even though the default radius is spot on most of the time, there may be
scenarios where you need to be extra careful to avoid noise and over
sharpening. For example when an image is going to be processed in
programs designed for focus stacking, astronomical images,
super-resolution images etc. In these cases, it may be better to turn
off the auto radius calculation and manually set the radius to a lower
value to avoid artifacts (check the result by zooming in on the image).
There will not be as much sharpening but there will be fewer or no
artifacts that could be enhanced by subsequent processing in other
software.

Note also that if you are editing a long-exposure raw file (with hot
pixels), the auto radius calculation works much better with the hot
pixel filter turned on (located in the *Raw tab*):

<div>

- <figure>
  <img src="/images/Renon_hotpixels.png" title="Renon_hotpixels.png" />
  <figcaption>Renon_hotpixels.png</figcaption>
  </figure>

- <figure>
  <img src="/images/Renon_nohotpixels.png" title="Renon_nohotpixels.png" />
  <figcaption>Renon_nohotpixels.png</figcaption>
  </figure>

</div>

### Corner Radius Boost

Often images are softer or more blurred in the corners than in the
center. The Corner radius boost slider allows you to compensate for this
by increasing or decreasing the radius in these areas.

Moving it to the right increases the sharpening in the outer areas and
sliding it to the left will reduce the sharpening.

### Iterations

Once the radii have either been automatically calculated or set
manually, the tool carries out a series of calculations to try and
compensate for any blurring. It is an iterative process, which will
produce artifacts if carried too far. Checking the ‘Auto limit
iterations’ checkbox will limit the number of iterations or you can do
it manually using the Iterations slider.

## Prerequisites

To get the best out of this tool, the camera white level needs to be
correct, especially if the image has sharp transitions between clipped
and non-clipped highlights. If you experience problems, please refer to
the section on *White Levels* in [Adding Support for New Raw
Formats](Adding_Support_for_New_Raw_Formats.md).
