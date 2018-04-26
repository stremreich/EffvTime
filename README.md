# EffvTime

EffvTime.C is a ROOT macro for plotting per-chamber SEG/LCT efficiencies on a efficiency v time plot.

## Use (in ROOT's interactive shell)
### Before calling
Make sure to load the CMSStyle package before loading/calling EffvTime. This can be done in EffvTime by uncommenting the first 3 lines of the function or manually in ROOT. CMSStyle.C is included in this repository.

Depending on your ROOT version, you may also need to load vvloader.C, since EffvTime stores the various efficiency data in a 3D std::vector object, which may not be automatically recognized by ROOT as writable to a .root file.

### Calling EffvTime()
The EffvTime function has 5 parameters:
- The file name for a root file containing a plot of LCT efficiencies and their uncertainties. This file is produced by running the TnP process [here](https://github.com/stremreich/CSC_eff_9_2_3_patch2).
- The file name for the root file with the segment efficiencies.
- A TDatime object for the beginning of the data-taking period that you are plotting.
  - For example, if you are plotting data taken from Aug 9 - Sep 9, this would be the exact time and date that the first run on Aug 9 began.
- A TDatime object for the end of the data-taking period.
  - In the example, this would be the time when the last run on Sep 9 ended.
- A simple boolean to tell whether to produce plots. This is purely a time-saver, since it takes a bit of time to plot all few-hundred plots for each chamber.

### Specifics of Use
EffvTime functions additively, one "data point" at a time. So, if you want to plot 5 different data ranges on your Eff v Time plots, you would call the function 5 times.

NOTE: EffvTime will automatically open and add to the file EffvTime.root, which it produces when it is first called. There is no way to delete data points at present, so be very careful that any old EffvTime.root files are not in the working directory if you wish to start a new set of plots.

### Other files/output
EffvTime also outputs another file named DEffvTime.txt, which is intended to show chambers with a large efficiency change in between any two consecutive data points. For this to work, you must input all the data points in chronological order.

[Bug] There is currently a bug with the years that are output to DEffvTime. The months and days appear to work.

Also included in the repository is a macro (TeXouput.C) to output TeX frames (texout.txt) for displaying all of these plots.
