## Problem Statements and how this pipeline solves them

### LabelGen

    Problem:    Manually writing each label with a labelling machine is slow and arduous for
                large-scale sampling of field plots. This program saves you time and carpel-
                tunnel by reducing labeling to simple unpeeling a premade label and sticking
                it onto your seed-packet. 

    Solution:   A dynamic labelling system used to convert CSV/EXCEL files containing info
                of your plots into a specially formatted PDF file. This PDF file will then
                be printed onto Avery 5160 Easy-Peel label sheets. Then simply unpeel the 
                label and paste it into a seed-packet. Labels can be designed with QR codes,
                so with a QR reader you can instantly get a string with all the plot data 
                onto your computer as well.

### Parralel-Scanning

    Problem:    To quantify seed growth, the lab uses flatbed scanners to create high-
                resolution images for analysis. To increase data through-put, you can use
                multiple scanners on the same computer and control them with a simple script.
                But this will only allow for sequential scanner (one scanner to run at a time). 
                Each high-resolution scan takes ~2 mins, so **8 scanners would take 16 minutes 
                just for 8 scans.** 

    Solution:   A guide & source-code on how to orchestrate scanners running in parralel. Despite
                my attempts on making the steps as easy as possible, this will require some setup.
                When setup for 8 scanners, a maximum of 4 scanners can be run at the same time while
                the other 4 can be directly queued to excecute after - allowing some time to juggle
                unloading and loading seeds. As each scan takes ~2 mins, and some buffer time is
                forced to prevent power or data contention, **you can get 8 scans in 5 minutes.** 

### SeedSizer

    Problem:    After scanning, you are left with hundreds or thousands of raw, high-resolution images 
                of seeds. While these images visually show growth differences, they are not useful for 
                analysis without turning them into quantitative metrics.

    Solution:   An image-analysis program designed to extract quantitative metrics from scanned seed 
                images. Using basic computer-vision techniques, this tool segments individual seeds 
                and computes measurements such as size, count, and distribution statistics. The output 
                is structured data (CSV) that can be directly compared across plots, genotypes, or 
                treatments to assess crop performance.
