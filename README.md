![isovist_workflow_with_legend](https://github.com/user-attachments/assets/2d694aa3-8462-46a4-b46a-ddc38e5e4e61)![graphical_abstract](images/graphical_abstract.png)

# SVI Coverage and Bias
[![License: CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/80x15.png)](https://creativecommons.org/licenses/by-sa/4.0/)

Repository for releasing the code used in **Coverage and bias of street view imagery in mapping the urban environment**, developed by Zicheng Fan from [Urban Analytics Lab (UAL)](https://ual.sg/), National University of Singapore (NUS).

The journal paper can be found [here](https://doi.org/10.1016/j.compenvurbsys.2025.102253).


 ## SVI Coverage Estimation Workflow
In **SVI Coverage and Bias** project, focusing on the dual nature of Street View Imagery (SVI)—both as vector data with geographic location and orientation and as image data capturing and mapping real-world objects—we explore a computational workflow to estimate SVI's coverage of urban building elements.
![workflow](images/isovist_workflow_with_legend)

 ### Isovist Analysis




Apart from the nighttime images, luminosity of scene at the same location are measured with a light meter. The nighttime images are also paired with corresponding daytime SVI from Google Street View. <!-- Each image has been enriched with a wide range of geospatial, temporal, contextual, semantic, and perceptual information adding up to 346 unique features, as shown in the below illustration. -->

## Detecting Generic Lighting Patterns from Nighttime SVI

To reduce the effect from image quality issues, such as glare, jitter, blur and extract useful information, we apply a series of CV methods for processing the nighttime SVI. The methods include: (1) Re-project nighttime SVI from equiretangular view to fisheye view. (2) Convert images from RGB to grayscale. (3) Extract significant lighted spots based on the luninosity difference between pixels. (4) Calculate the area of lighted spots, distance from lighted spots to image centorids, total luminosity of images and other attributes, to represent the street-level lighting pattern reflected by the image.



With the k-means clustering method, we identified seven distinct street lighting patterns and map the patterns back to the collection points. It is found that some lighting patterns can be commonly observed in different functional areas. For example, Cluster 1 can frequently occurred in industrial parks, highways, and university campuses; while Cluster 5 is prevalent in low-rise and high-rise commercial areas. In addition, we can discern that each urban functional area can be typically described by one or two primary lighting patterns, and be distinguished from others by a secondary lighting pattern. Though some urban areas looks similar at a glance during nighttime, their components of lighting patterns can be significantly different. 

![kmeans](images/cls_workflow_result.png) 


## Inferring Street-level Luminosity at City Scale
To map the street level lighting condition at urban scale, we have bult a deep learning workflow with the daytime street view imagery as input and the nighttime luminosity values as output. The logic behind the workflow is that daytime and nighttime SVI are related and features covered in daytime SVI, like building facades, street lamps, and greens can be useful in inferring luminosity of the same scenario in the nighttime. The best trained model is used to infer luminosity based on the 50 thousand daytime svi we collected around singaproe. In this way, we are able to map the street-level lighting conditions at urban scale. As shown in the figure, we have further compared the svi predicted luminosity with the satellite derived luminosity. It turns out that the two lighting indicators show similar global distribution. but there is also significant local discrepancies.

![dl_workflow_result](images/dl_workflow_result.png) 

## Discrepancy Analysis

To detect where and how the lighting info represented in the two data source can be different, we built a linear regression model correlating SVI luminosity with satellite luminosity. We then examined the residual distribution of the model using Local Spatial Autocorrelation methods. Our findings indicate that in Central Business Districts (CBDs), ports, and airports—highlighted in red—SVI-based luminosity often underestimates the satellite-based luminosity. Conversely, in the rural northern areas, marked in blue, SVI-based luminosity tends to overestimate.

One possible explanation is that complex vertical lighting structures are perceived differently by SVI and satellite imagery due to their distinct imaging perspectives. For instance, in red-marked areas, façade or rooftop lighting in CBDs, as well as strong aviation and industrial lighting in ports and airports, are more easily captured by satellite imagery. However, these elevated light sources can obscure street-level lighting, leading to discrepancies in the lighting information sensed by the two data sources. We have also discussed other potential causes in the paper.

![discrepancy](images/local_moran.png) 



## Paper / Citation

If the project benefits your work, please cite the [paper](https://doi.org/10.1016/j.compenvurbsys.2025.102253): 

Fan, Z., Feng, C.-C. and Biljecki, F. (2025) ‘Coverage and bias of street view imagery in mapping the urban environment’, Computers, Environment and Urban Systems, 117, p. 102253. doi: [https://doi.org/10.1016/j.compenvurbsys.2025.102253](https://doi.org/10.1016/j.compenvurbsys.2025.102253)

BibTeX:
```
@article{fan_coverage_2025,
	title = {Coverage and bias of street view imagery in mapping the urban environment},
	volume = {117},
	doi = {10.1016/j.compenvurbsys.2025.102253},
	pages = {102253},
	journal= {Computers, Environment and Urban Systems},
	author = {Fan, Zicheng and Feng, Chen-Chieh and Biljecki, Filip},
 year = {20251},
}

```



