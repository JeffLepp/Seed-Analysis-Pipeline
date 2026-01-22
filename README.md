# Seed Pipeline Source Repo

To evaluate overall success of an experimental plot, researchers often measure 
both plant growth and final seed yield. this pipeline is designed to make the latter 
as efficient as possible since tracking & analysis of many plots can be arduous.

## Pipeline Components

- LabelGen  
  https://github.com/JeffLepp/LabelGen  
  Sample labeling and metadata encoding for easy sample association with a future scan

- Parallel-Scanning  
  https://github.com/JeffLepp/Parallel-Scanning  
  High-throughput, parallel flatbed scanning using metadata from LabelGen's QR codes

- SeedSizer  
  https://github.com/JeffLepp/SeedSizer  
  Image-based seed metric extraction for scans produced by parralel-scanning


## General Steps To Use Pipeline

```
        LabelGen            PIPELINE PART 1
            ↓
     Seed Collection
            ↓
    Parallel-Scanning       PIPELINE PART 2
            ↓
        SeedSizer           PIPELINE PART 3
            ↓
   Quantitative Metrics
            ↓
  Determine plot success
```

![Seed Pipeline Overview](assets/pipeline-flow.png)


