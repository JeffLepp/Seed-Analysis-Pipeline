# Seed Pipeline Source Repo

To evaluate overall success of an experimental plot, agricultural researchers often 
measure both plant growth and final seed yield. This pipeline is designed to make the 
latter as efficient as possible since tracking & analysis of many plots can be arduous.

## Pipeline Components

- LabelGen  
  https://github.com/JeffLepp/LabelGen  
  Sample labeling and metadata encoding for easy sample association with a future scan

- Parallel-Scanning  
  https://github.com/JeffLepp/Parallel-Scanning  
  Method for high-throughput, parallel flatbed scanning using metadata from LabelGen's QR codes

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


## Docs

- docs/architecture.md  
  Defines the system architecture of the seed analysis pipeline, describing each component
  (LabelGen, Parallel-Scanning, SeedSizer) in terms of inputs, startup requirements, processing,
  and outputs.

- docs/data-flow.md  
  Describes how data artifacts move through the pipeline, including file types, directory
  structure, naming conventions, and how outputs from one stage become inputs to the next.

- docs/constraints.md  
  Lists operational assumptions and non-negotiable constraints required for the pipeline to
  function correctly, including hardware, formatting, and cross-stage conventions.

- docs/prob-statements.md  
  Provides background motivation for the pipeline by outlining the practical lab problems each
  component was designed to address.

Detailed documentation for each component is located in its respective repository.


## Acknowledgements

Special thanks to Wilson Craine and Cody Willmore for their guidance and support.
