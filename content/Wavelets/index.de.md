---
title: Wavelets de
contributors:
  - Fherb
---

Todo-List / State:

- Translation: open
- Content completely cleared: open
- Expression and didactics checked: open
- Spelling checked: open

Ready for publishing: no

------------------------------------------------------------------------

The effects of this tool are visible at any zoom level. However, due to
the nature of the algorithm, only the 1:1 (or more) preview zoom will
match the saved image perfectly. The size of the image has a direct
impact on the perceived sharpness. In practice, this means that you
should use this tool at a zoom level similar to that of the desired
final size of the image in terms of viewing distance, screen or paper
size, etc. So if you intend to print a high resolution image on a
90x60cm canvas and view it from a distance of 30cm, then it is
reasonable to zoom in to 100% and adjust the "0 (Finest)" contrast
slider. However, in reality such large prints when hung on the wall are
observed from a good distance off - say, from a couch some meters away -
and at this distance adjustments to the finest detail level cannot be
distinguished; the eyes cannot perceive such fine details at this
distance. The same applies if your image will subsequently be resized,
e.g. for email attachments to friends or customers, for image sharing
websites, for social platforms, etc. Not only will the image resolutions
be lowered but the images may be viewed on devices with a lower
resolution, not even fullscreen, on laptops, tablets or smartphones.
Keep this in mind, so you do not waste time adjusting detail levels
which will be lost anyhow. Usually only Contrast sliders 2 and above
provide a useful effect.

------------------------------------------------------------------------

The wavelet tool is close to being finished (today being 2015-02-11).
The information contained herein should be mostly accurate for the
wavelet tool as available in version 4.2.217. Some information still
needs to be written or updated.

## What is a Wavelet?

A [wavelet](http://en.wikipedia.org/wiki/Wavelet), or more specifically
a [wavelet transform](http://en.wikipedia.org/wiki/Wavelet_transform),
is a mathematical function very useful in image processing as it enables
one to split the signal into various levels of detail so that you may
work on the levels which are of interest to you. The English term
"wavelet" was introduced in the early 1980s by French physicists Jean
Morlet and Alex Grossman. They used the French word "ondelette", which
means "small wave". Afterwards, this word was transferred to English by
translating "onde" into "wave" giving "wavelet". The wavelet transform
is fairly similar to a Fourier transform, the general difference being
that wavelets are localized in both time and frequency whereas the
standard Fourier transform is only localized in frequency.

Decomposition in RawTherapee currently uses the L\*a\*b\* space. This
decomposition produces two kinds of fundamentally different products:

1.  Several levels of detail. Choosing the number of levels depends on
    your needs. The first level corresponds to an area of 2x2 pixels,
    the tenth level corresponds to a region of 1024x1024 pixels. The
    more levels, the more processing time and memory is required. Each
    level contains only the "variations" (positive or negative, for
    example the contrast that gives data type 0+D1, 0-D2). If a picture
    is absolutely uniform in luminance and color, each level will
    contain no information. Thus, one can act separately on each of the
    levels, but with specific algorithms that take this feature into
    account. The "quality" of information present in each level is a
    function of the mother wavelet used: either it is simple as is the
    case with the "[Mexican hat
    wavelet](http://en.wikipedia.org/wiki/Mexican_hat_wavelet)" as used
    in [dcraw](https://en.wikipedia.org/wiki/Dcraw) and
    [GIMP](http://en.wikipedia.org/wiki/GIMP), or it is more complex and
    powerful as is the case with the "[Daubechies
    wavelet](http://en.wikipedia.org/wiki/Daubechies_wavelet)" as used
    in RawTherapee.
2.  A residual image. This image corresponds to the difference between
    the source image and the combined details of all level scales. The
    residual image has the same characteristics - in terms of its
    treatment - as the source image, and lacks the details which are
    present in the other levels. Modifying the characteristics
    (contrast, chroma, etc.) of a level has no effect on the residual
    image, and vice versa.

Depending on our needs, we will need to look either at an individual
level of detail, at several levels of detail, at the residual image, or
at all of these at once. RawTherapee makes this so easy it's ridiculous.

After decomposition it is possible to use wavelets for different
purposes:

- Image compression,
- Noise processing,
- [Secret
  watermarking](http://www.intechopen.com/books/discrete-wavelet-transforms-algorithms-and-applications/application-of-discrete-wavelet-transform-in-watermarking),
- Specific treatment for astronomy, separating the background (residual
  image) from the planets and stars, or separating stars from dust
  clouds.
- etc.

Wavelet decomposition is used to separate each luminance level
(contrast), the chromaticity of each of the a\* and b\* channels, and
the residual image. This action enables you to apply different
treatments to the luminance detail levels, the chrominance detail
levels, and the residual image which depends to the selected number of
luminance detail levels. It is possible (for software developers) to
extend the existing processes to others. For example, each level
corresponds in fact to the equivalent of a layer; by having suitable GUI
tools, it is possible to edit the details (stains, spots, etc.) only in
the levels they appear in, and therefore preserve better image quality.
Similarly, it is theoretically possible to apply treatments available in
other RawTherapee tools to the residual image (L\*a\*b\* Adjustments,
Color Toning, etc.). Their implementation may require increased memory
requirements and processing time.

You can change the type of mother wavelet used by going to Preferences
\> Performance & Quality:

- Check the option "Use Wavelet Daubechies D6 instead of D4" to increase
  the number of coefficients of the wavelet.
- This action has no or little effect on the residual image or high
  levels (5..10)
- **((can't make sense of this))** On the other hand it (it what? it=D4
  or it=D6?) can reduce unnecessary stress effects **((what is this?))**
  for low detail levels (0..1) under undesirable areas that D6 is more
  discriminating than D4 (skies, high values of initial contrast, etc.),
  for example when using high values of "Edge Sharpness".
- There is virtually no difference in processing time or memory
  requirements between D4 and D6.

Once the "treatments" have been applied (to the levels and residual
image), the image is re-composed.

RawTherapee has a tool called [Contrast by Detail
Levels](Contrast_by_Detail_Levels.md) - it "looks" like this
Wavelet Levels tool but has several differences:

- CbDL has fewer levels,
- **((did I get this right?))**CbDL lets you only work on the levels'
  luminance, while Wavelet Levels lets you also modify the chromaticity,
- CbDL has no residual layer.

Having said that, there is nothing preventing you from using both
Contrast by Detail Levels and Wavelet Levels together. CbDL is located
upstream in the toolchain pipeline, **((what does this mean?))**and can
interfere on levels 0-5.

## Utilities

### Total Levels

This slider allows you to select the number of detail levels the image
should be decomposed to. The greater the number, the more processing
time and memory will be required.

Choosing a low number of levels, 5 for example, will limit the system to
details of a scale of 32 pixels. The residual image will contain all the
detail the image has except for that contained in levels 0-5.

Choosing a high number of levels, 9 for example (the 10th level is
called "Extra"), will allow you to change the details of a scale of 512
pixels (level 8) or 1024 pixels (level "extra", whose effects are only
visible if your preview size is large enough). The residual image will
differ significantly from the original image as levels 0-10 contain all
of the details, so what is left in the residual image is a blurry mask.

The residual image is what is left after all the detail levels have been
removed, as many as you have chosen to use via the Max Levels slider.
For example if you decompose the image into 7 detail levels (set Max
Levels to 7), but you only use the contrast slider on the first three
levels (on levels 0-2), the residual image is still whatever is left
after the details of levels 0-6 have been removed from it, not just
levels 0-2.

Important! RawTherapee uses as many levels as it can unless the size of
the level is larger than the size of the image. That is to say, if you
are working on a photo larger than 1024x1024px, then changes made even
to the 1024px level will be visible in the saved image. If the photo is
smaller than that, then the 1024px level will be skipped. This is
important to keep in mind, as the same principle applies to the preview:
if the photo is larger than 1024x1024px but the preview area is smaller
than 1024x1024px, then the 1024px level will be skipped in the preview,
though it will be used when saving the full image. This may lead to
significant differences between the preview and saved image, so it is
worth committing this caveat to memory. You may expand the size of the
preview area by shrinking or hiding the left and right panels (shortcut
"m") and you gain a few more pixels by making the RawTherapee window
fullscreen (shortcut "F11"). The interface informs you how many levels
are used in the preview under the contrast sliders, "Preview maximum
possible levels=9" for instance.

### Full Image vs Tiles

A selection box allows you to choose between:

- Full image,
- Big tiles,
- Little tiles.

It is always preferable to use "full image" as it avoids quality issues
in the transition zones between tiles. If you do not have enough RAM
or/because you are processing huge images then tiles may need to be
used.

#### Memory requirements

Memory requirements, in bytes, for "full image" mode, assuming 9 levels
are used, with examples given for two cameras:

1.  Pentax K10D (10.2MP) 3888 x 2608
2.  Nikon D810 (36.3MP) 7360 × 4912

Baseline  
Minimal requirement for opening an image in RawTherapee, when all tools
are off/neutral

`width*height*12`

K10D: 116MiB

D810: 414MiB

When using level contrast, chromaticity or hue targetting/protection  
`levels*width*height*3 + width*height*7`

K10D: 329MiB

D810: 1172MiB

Additionally when using Avoid Colour Shift  
`width*height*4`

K10D: 39MiB

D810: 138MiB

Total  
K10D: 483MiB

D810: 1724MiB

## Show wavelet levels

This panel has three combobox menus which allow you to refine what you
see in the main preview. It serves to teach you, to help you understand
how to work with the wavelet system. Changes made to this panel affect
only the main preview, not the processed image.

The first combobox lets you choose to preview:

1.  One wavelet level,
2.  Below or equal to the level,
3.  Above the level + residual,
4.  All levels & directions.

The second combobox lets you specify the reference level for the above
options, from "level 0" to "level 8".

The third combobox lets you choose to see the following wavelet
directions for the first three preview options:

1.  Vertical,
2.  Horizontal,
3.  Diagonal,
4.  All.

For example you can choose 'one wavelet level' mode to find the wavelet
which contains the scale of details you want to work on (e.g. the level
containing the scale of skin blemishes but not skin texture) and to see
the effects of your adjustments on that level.

Another example, you could choose to preview "above the level +
residual" with "level 8" selected to see the residual image and the
influence upon it of the tweaks you make in the "Residual image" panel,
explained further on.

## Contrast

### Contrast Levels

By default, seven levels appear in this menu (starting from level 0).
You can reduce or increase this number by changing the Total Levels
slider.

Reminder that the fewer levels you use, the less RAM and processing time
is required, and the more the residual image matches the source image
because fewer detail levels are removed from it.

The "Contrast -" and "Contrast +" buttons provide an easy way of
tapering off the level values in a gentle slop. Of course, these buttons
aid in adjustments where small levels are most significant, but often
one may want to adjust the high levels too, for instance so that the
small levels increase contrast while the large levels decrease it.

Each level corresponds to a scale of details. Action on a given level is
only possible if that level contains contrasting areas to begin with. If
a level is uniform in contrast, the slider will have no effect.

Levels:

1.  Level 0: 2x2 pixels
2.  Level 1: 4x4 pixels
3.  Level 2: 8x8 pixels
4.  Level 3: 16x16 pixels
5.  Level 4: 32x32 pixels
6.  Level 5: 64x64 pixels
7.  Level 6: 128x128 pixels
8.  Level 7: 256x256 pixels
9.  Level 8: 512x512 pixels
10. Extra: 1024x1024 pixels

Remember what you read in the "Total levels" section above: the preview
area must be at least as big as the level in order for it to be visible
in the preview.

The residual image is not listed above because it is not a level - it is
whatever is left over from the original image after the detail levels
are taken away from it.

Changes to a level can be applied in a straightforward manner, or only
to highlights and shadows. The same is true for changes to chromaticity.
Read on.

### Apply to

This module allows you to focus the sliders' action on a luminance
range, for example increasing the contrast of fine details for high
luminance, and reducing the contrast of coarse details for low
luminance.

#### All Luminance

If you select "All Luminance", each slider has the same action
regardless of the luminance of the area.

#### Shadows/Highlights

If you select "Shadows/Highlights" more controls appear in order to
customize the action:

- A luminance range for shadows,
- A slider which allows you to select how many levels should only have a
  darkening effect, always starting from "level 8", even when you use
  less levels than that.
- A luminance range for highlights,
- A slider which allows you to select how many levels should only have a
  lightening effect, always starting from "level 0".

For example if you only use 7 levels, which makes the highest level be
"level 6" (the count starts from 0), and you want "level 6" to only have
a darkening effect and levels 0 and 1 to have a lightening effect, then
set the Shadow Levels slider to 3 and the Highlight Levels slider to 2.

Changes to levels which are not targetted by these two adjusters apply
evenly to their whole luminance range.

## Chromaticity

The construction of this module is similar to that of the contrast
module. You have the following choices:

1.  All chroma: in this case, the whole chromaticity range is affected
    by each level's change, independent of contrast levels.
2.  Pastel/Saturated: here you can choose two limiting ranges for
    pastels and saturated colors, independent of contrast levels.
3.  Link contrast levels: here chromaticity changes are directly related
    to those of contrast.

### All Chroma

If you select "All Chroma", the whole chromaticity range of each
affected wavelet level is modified, regardless of how saturated it is.

Chromaticity = sqrt(a\*a + b\*b) is a wide open, but I limited it to
0..140, which should satisfy almost all cases.

The chromaticity curve:

- The *x*-axis represents the wavelet levels, from the finest on the
  left end to the coarsest on the right end. Its effect is therefore not
  continuous, but discrete: the vertical values are sampled in 9 points
  equally spaced out along the *x*-axis, starting at the very left edge
  of the curve, and ending at the very right edge. If you use less than
  9 wavelet levels, say 7 points, the rightmost 2 sampled points would
  be ignored.
- The *y*-axis represents the force of the action for each level. If the
  curve is above the equator, chromaticity for the affected wavelet
  levels is increased. If below - decreased.

The same remark applies here as that for the contrast levels: action on
a given level is only possible if that level contains varying
chromaticity to begin with. If a level's chromaticity is uniform (does
not vary), the curve will have no effect for that level.

### Pastel/Saturated

You can treat the chromaticity in three ways:

1.  All chroma - Evenly apply the change in chromaticity (*y*-axis)
    regardless of what chromaticity the levels already have.
2.  Pastel/Saturated - Apply the change in chromaticity with respect to
    the pastel/saturated threshold value, default at 5, so the limiting
    range of saturated tones will be effective for the first 5 levels
    and the limited range of pastel tones for the remaining levels.
3.  Link contrast levels - Here the action on the chromaticity - insofar
    as it varies in the original image - will be directly proportional
    to the slider settings for contrast levels. This proportionality is
    achieved using the "chroma link" slider: 0 has no effect on the
    chromaticity, 100 has maximum effect.

## Split Toning

This "partial color shift" (toning) is perhaps not the best name, but it
must do...

We can not act directly on the color (hue) in the levels because the a\*
and b\* channels are decomposed and it is near impossible to chart an
accurate mathematical relationship between the chosen hue and such
decomposed channels.

Nevertheless, we propose two curves built on the same principle as the
chromaticity curve, where the *x*-axis represents the (discrete) number
of levels (0-8), and the *y*-axis the force of the action with a
positive effect above the equator and a negative one below it:

- The a\* curve, which acts on the red-green tones,
- The b\* curve, which act on the blue-yellow tones.

Note: if you apply identical adjustments to both a\* ad b\* curves, the
end result will be identical to that which you would get had you used
the chromaticity curve.

## Edge Sharpness

This control is an addition to RawTherapee's existing arsenal of
sharpening tools, including Unsharp Mask, RL Deconvolution, Edges, etc.
Its principle is naturally based on the use of the wavelet
decomposition. From a distance it vaguely resembles the Unsharp Mask to
the extent that the wavelet decomposition creates a residual image which
can be likened to a mask. But there the comparison ends. The wavelet
decomposition of levels using the "Daubechies" method is a kind of
direct recognition of contours as it scans each level of detail. The
first level, level 0, uses every second pixel to act on details of a
"radius" of about 2 pixels; the second details of a "radius" of 4
pixels, etc.

If the algorithm is interested only in the smallest details **((??? we
can select the radius in the UI, so this "smallest details" doesnt
really make sense))**, and if a value is placed in reference**((???))**
(I called "Radius") and compare it to the current level, we are able to
adjust the increase in contrast only for these levels, with a
significantly higher increase values to those obtainable with the 10
sliders "Contrast".**((this whole paragraph needs rewriting, I can't
make interesting/useful sense of it))**

There are 3 sliders:**((this section is a direct copy, i did not rewrite
it because its meaning is unclear to me))**

1.  Radius may need to call it otherwise?**((why?))** Its size will
    allow to increase the effect of perspective**((perspective?))**. The
    increase is not linear. Its action is not zero if the cursor is at
    zero. Discriminant action is maximum (for low wavelet levels), for
    low radius values, without being able to predict the level of
    action.**((???))**
2.  Value controls the strength**((then why dont we call it
    strength?))**. Setting it to 0 effectively turns sharpening off.
3.  Threshold (Threshold) allows different breakdown levels higher
    (distribution) for low levels (0, 1..2) when moving the cursor to
    the right.**((???))**

The edge sharpness tool is very sensitive to Maximum Levels setting
because in principle it is interested only in the smallest levels, which
are always decomposed.

## Gamut - Controls

### Reduce Artifacts in Blue Sky

Digital images often have some mottle noise in the blue sky. The wavelet
process, because it increases local contrast, can generate or amplify
small artifacts. This checkbox introduces a median filter to reduce
these artifacts.

Do not forget to use the [Noise Reduction](noise_reduction)
tool which is called upstream in the toolchain pipeline.

### Hue Targetting/Protection

This control is linked to the Contrast and Chromaticity wavelet
controls. Toning is not affected. Moving the slider to the left will
target the effects of these linked tools at the selected hue range.
Moving it to the right will target the effects at all hues other than
the chosen range.

The threshold selector widget below the slider lets you specify which
hues to target (or protect). By default, a range of skin hues is
selected. The selection is in the L\*a\*b\* space: 100\*PI, + 100\*PI.

### Avoid Color Shift

Applies an action on the chrominance and luminance of the recomposed
image in order to take into account the working colorspace and deliver
the data via a relative intent within the gamut of the working space.

## Residual Image

As a reminder:

- The residual image uses the same data format as the original image
  (source) before decomposition.**((what does this mean really, of what
  use to the user is this?))**
- It corresponds to the difference between the original image and the
  sum of the decomposed levels (the action on each level has no effect
  on the residual image).
- The more levels are used, the more the residual image deviates from
  the original image.

Modifying the residual image is one of the key points of the wavelet
processing. It allows one to:

1.  Work on the shadows and highlights independently of details,
2.  Reduce contrast (and chroma) overall, to better perceive
    micro-contrast,
3.  Change chrominance to reduce artifacts which result from excessive
    action of the levels (e.g. to the skies),
4.  etc.

### Shadows/Highlights

Moving the Shadows and Highlights sliders to the right increases
luminance in these areas; to the left - decreases. This action is
comparable to that of the
[Shadows/Highlights](shadows/highlights) tool in the Exposure
tab. Beware though that it does not invoke the principle of [highlight
reconstruction](Exposure#Highlight_Reconstruction.md).

The action of these sliders is influenced by the two threshold sliders:

1.  Shadows Threshold, it is set to 30 by default (on the 0-100 L\*
    scale), which means that only luminance values around 30 and below
    will be influenced by the Shadows slider.
2.  Highlights Threshold, it is set to 70 by default (on the 0-100 L\*
    scale), which means that only luminance values around 70 and above
    will be influenced by the Highlights slider.

Read the L\* value from the Navigator panel to help you decide the
correct threshold values.

You could use the Shadows/Highlights adjusters to:

1.  add bloom to bright objects,
2.  prevent highlights from clipping,
3.  lift shadows,
4.  etc.

### Contrast

This is one of the key points of the treatment made possible by
wavelets. It allows you to change the contrast of the featureless
residual image (remember, the residual image has no details, as those
are handled by the contrast sliders) while letting you adjust the
contrast of the detail levels using the contrast sliders above. For
example by moderately reducing the contrast of the residual image, this
leaves more room to accentuate that of each level, and thus increase the
perception of depth and relief.

### Chromaticity

The same principle as for contrast slider above applies to the use of
the chromaticity slider, but in addition you can act selectively on
colors by use of the Hue slider in conjunction with the Hue
Targetting/Protection slider. By default a typical blue sky-colored hue
range is selected, but of course you can change it to anything you like,
for example to match the colors of a flower, or skin. The Hue
Targetting/Protection slider lets you choose how you want the
chromaticity change to affect the selected hue range:

1.  By moving it to the left, only the chosen hues will be affected by
    your chromaticity change, e.g. select green grass hues, increase the
    Chromaticity slider, and move this Hue Targetting/Protection slider
    to the left to increase the chromaticity of only grass-colored in
    the residual image.
2.  By moving it to the right, your chromaticity change will apply too
    all hues except those chosen by the Hue selector. So in the example
    in the previous point, if you were to move the slider to the right,
    the chromaticity of all hues except the grass-colored ones would
    increase.

This control is very useful in the prevention of over-saturation of
human skin, a carrot look which our eyes are used to noticing.
