## M45 Workflow 
Processed using Pixinsight, Lightroom 
Telescope: Takahashi FSQ-106ED (with 0.73x focal reducer) 
Camera: FLI PL 16083
Mount: Paramount MX+
Filters:  Astrodon LRGB 2GEN
Total integration: 1hour 20 minutes
Location : IC Astronomy, Oria, Almaria, Spain
Data acquired via @telescope.live

* Type of data - LRGB -- using LRGB (luminance, red, green, blue) filters to
reduce the influence of light pollution from mercury, sodium vapor. 
1. Open the data and view it using blink
2. Use STF to autostretch 
3. If there are vertical edges that needs to be cleared out use pixel math to calulate the pixel and
clear out (follow Adam Block's tutorial in telescope live)
4. Use star alignment to align images, with luminance image as reference.
5. Use image integration for red, green, blue, luminance (separately) to calculate a mean stack of respective
groups
6. Use Dynamic crop to have common cropping for all groups. 
7. Use background extractor (I used Automatic BE), and used subtraction (target image correction) mode for all images. 
8. Use linear fit to have common background. Take L image and apply it to others. 
9. Use LRGB combination (with L off) to combine R G B images to restore their colors. 
9. (Optional) Use PhotoMetric Color calibration, to bring out realistic colors. PCC can be hit or miss - in this case MISS. **Not used here**
10.  Use background neutralization and color calibration with Pixinsights default settings. 
11. Noise reduction -- Use **Multiscale Linear Transform** to remove background noise at various levels - we use 5 levels with settings:
| Layer | Scale | Parameters      |
|-------|-------|-----------------|
| 1     | 1     | S(5.0,0.85,1)   |
| 2     | 2     | S(3.5, 0.75, 1) |
| 3     | 4     | S(2.5,0.5,1)    |
| 4     | 8     | S(0.75,0.33,1)  |
| 5     | 16    | S(0.5,0.28,1)   |
Take a linear mask, turn auto stretch off, preview mask, try zoom a preview and apply the changes to the preview, then extend your changes to the entire image. Always rename the images based on the changes you are making. 
12. Manual Stretching: Open Histogram transformation, turn on real time preview and lock it. Drag slider to left, apply changes, keep dragging but be careful to check if you are clipping darks, midtones. Avoid clipping as much as possible. 
13. Take luminance layer and run deconvolution to bring out the details, turn on deringing . 
14. Run Multi scale linear transform on Luminance layer.
15. Manually stretch Luminance layer like 12.
16. Combine Luminance channel NOW with the RGB image. 
17. Invert image, and use SCNR to remove green noisy signals.
18. Make a mask using Range Mask tool so that we can apply changes to the areas we want to; in this case the star cluster. 
19. Do curves transformation and increase saturation and vibrance. 
20. Invert mask and apply changes in background. Pull out the sky somewhat dark but should retain a fuzzy look because of the presence of dust. 
21. Export image in 16 bit tiff file and open lightroom to make some exposure and color adjustments. 
22. Use the processed image in topaz denoize to reduce some noise and preserve the detail. 

Resources : Adam Block, Joe's Astrophoto. 


