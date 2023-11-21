# EyeInfo Dataset

The EyeInfo Dataset is an open-source eye-tracking dataset created by [Fabricio Batista Narcizo](http://www.itu.dk/people/fabn), a research scientist at the [IT University of Copenhagen (ITU)](http://www.itu.dk) and [GN Audio A/S (Jabra)](http://www.jabra.com), Denmark. This dataset was introduced in the paper "_High-Accuracy Gaze Estimation for Interpolation-Based Eye-Tracking Methods_" (DOI: [10.3390/vision5030041](https://doi.org/10.3390/vision5030041)). The dataset contains high-speed monocular eye-tracking data from an off-the-shelf remote eye tracker using active illumination. The data from each user has a text file with data annotations of eye features, environment, viewed targets, and facial features. This dataset follows the principles of the General Data Protection Regulation (GDPR).

## Eye-Tracking Data

We have built a remote eye tracker with off-the-shelf components to collect the real eye-tracking data. The collected data contain binocular eye information from $83$ participants ($166$ trials), with the following annotations: frame number, target ID, timestamp, viewed target coordinates, pupil center, the major/minor axes and angle orientation of fitted ellipse, and four enumerated corneal reflections’ coordinates. We have extracted the eye features from recorded eye videos using a feature-based eye-tracking method (i.e., binarization+fitting ellipse), and the raw data are available on individual annotated text files (CSV). The raw dataset contains outliers due to blinks, light reflections, missing glints, and low contrast between the iris and pupil.

### The Remote Eye Tracker Apparatus

The prototype has used one Point Grey Grasshopper3 ([GS3-U3-41C6NIR-C](https://www.flir.eu/products/grasshopper3-usb3/?model=GS3-U3-41C6NIR-C&vertical=machine+vision&segment=iis)) integrated with an infrared global shutter sensor ([CMOSIS CMV4000-3E12 NIR](https://ams.com/cmv4000)), which allows us to collect high-definition images ($1600 \times 1200$, $4.1$ MP) in a frame rate of $150$ FPS. The distance between the eye-camera and the user’s eyes was about $20$ cm. The eye-camera has used a Navitar Machine Vision c-mount lens ([NMV-35M1](https://navitar.com/products/imaging-optics/low-magnification-video/navitar-machine-vision/nmv-1/)) of 35 mm (effective focal length) and $f/1.4$ (aperture). The lens had manual focus, an iris with locking screws, and a field angle of $20.9^\circ \times 15.8^\circ$. We attached an infrared narrow pass filter ([BP850 $830–850$ nm](https://midopt.com/filters/bp850)) between the lens and the camera sensor to improve the contrast of infrared eye images and block any noise from the visible spectrum (e.g., screen reflections). The eye tracker had a 24-inch AOC E2460PHU monitor ([240LM00010](https://aoc.com/in-en/products/monitors/e2460phu)) with $1920 \times 1080$ resolution, widescreen area of $531.36 \times 298.89$ mm, and pixel size of $0.27675$ mm. We attached a set of $870$ nm high-speed infrared emitting diodes ([TSFF5510](https://dk.rs-online.com/web/p/ir-lysdioder/1652451)) around each monitor corner. These LEDs helped increase the contrast between the pupil and the iris and create the corneal reflections used to compensate for the head movements.

### Participants

We have recruited a sample of $83$ volunteer participants ($55$ males and $28$ females) to collect data for this dataset. Fifty-five had normal vision, twenty-three wore glasses, and five wore contact lenses. Among the female participants, fifteen wore makeup on their faces or mascara in the eyelashes. The participants were free to blink during data collection, take a rest between the trials, or withdraw from testing at any stage. The participants have used a chin rest to reduce the head movements during the data collection.

### Data Collection

For each trial, the participant looked at targets arranged in a $5 \times 7$ grid in randomized order. The participant has sat approximately $450$ mm and orthogonal to the screen. Stimuli showed the target at the same positions and order for $2$ seconds. We have discarded the first and the last $500$ milliseconds to remove saccades movements between two targets, totaling $5250$ collected samples per participant/trial (i.e., $1$ second $\times$ $35$ viewed targets).

### Experiment Protocol

First, we have explained the experiment to the participant and obtained her/his signature on the consent document. Afterward, we have made the fine adjustments in the eye tracker components (i.e., infrared light sources, screen, eye-camera, and chin rest) before running the experiment trial. Each participant has experimented twice, the first trial to collect from the right eye and the second one for the left eye. In the end, we have checked the recorded eye-tracking data and interviewed the participant about fatigue or any physical discomfort during the experiment (no participant has made claims about that). On average, the experiment, including two trials, has lasted $7$ minutes and $58$ seconds.

## Usage

This project uses [Data Version Control (DVC)](https://dvc.org) to manage the dataset. The latest collected and processed eye-tracking data are available on the `main` branch of this GitHub repository.

### Requirements

- An active [Anaconda](https://anaconda.org) or [Miniforge](https://github.com/conda-forge/miniforge) installation added to your `$PATH`
- (Recommended) [Visual Studio Code](https://code.visualstudio.com) installed

### Installation

Create new environment called `eyeinfo`:

```bash
conda env create -f environment.yml
```

Activate the created environment:

```shell
conda activate eyeinfo
```

### Download the Dataset

The EyeInfo Dataset's raw data (videos, text, CSV, and JSON files) are available as a DVC resource on Google Drive. The dataset contains approximately $285$ MB of files.

Use [DVC](www.dvc.org) to download the raw EyeInfo Dataset. From the root folder, execute the following command:

```shell
dvc pull
```

This command will open the web browser automatically, and you must to sign-in using your Google account to allow DVC downloading the dataset. You must give full permission to DVC access the Google Drive resources.

DVC will create the folders called `01_dataset` with the raw data, `02_eye_feature` with the eye features extracted from each collected video, and `03_metadata` with the metadata of each processed video. The folder `01_dataset/0000` contains the $35$ videos of the right eye of the Participant #01. You can use these videos to understand how the dataset was created and organized.

## BibTex

If you want to cite the EyeInfo Dataset, you can use the [paper](https://doi.org/10.3390/vision5030041):

```text
@Article{Narcizo2021,
  author         = {Fabricio Batista Narcizo and Fernando Eust\'{a}quio Dantas dos Santos and Dan Witzner Hansen},
  date           = {2021-09-15},
  title          = {High-Accuracy Gaze Estimation for Interpolation-Based Eye-Tracking Methods},
  doi            = {10.3390/vision5030041},
  issn           = {2411-5150},
  number         = {3},
  url            = {https://dx.doi.org/10.3390/vision5030041},
  volume         = {5},
  abstract       = {This study investigates the influence of the eye-camera location associated with the accuracy and precision of interpolation-based eye-tracking methods. Several factors can negatively influence gaze estimation methods when building a commercial or off-the-shelf eye tracker device, including the eye-camera location in uncalibrated setups. Our experiments show that the eye-camera location combined with the non-coplanarity of the eye plane deforms the eye feature distribution when the eye-camera is far from the eye’s optical axis. This paper proposes geometric transformation methods to reshape the eye feature distribution based on the virtual alignment of the eye-camera in the center of the eye’s optical axis. The data analysis uses eye-tracking data from a simulated environment and an experiment with 83 volunteer participants (55 males and 28 females). We evaluate the improvements achieved with the proposed methods using Gaussian analysis, which defines a range for high-accuracy gaze estimation between -0.54$^\circ$ and 0.5$^\circ$. Compared to traditional polynomial-based and homography-based gaze estimation methods, the proposed methods increase the number of gaze estimations in the high-accuracy range.},
  article-number = {41},
  journal        = {Vision},
  pubmedid       = {34564339},
  year           = {2021},
}
```
