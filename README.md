# Computer Vision

## OpenFace landmarks

Under `data/`, there is a `.csv` file that contains basic coordinates and indices of [OpenFace landmarks](https://openface-api.readthedocs.io/en/latest/openface.html) that can be used to plot a schematic image of the output of OpenFace. 

For example, the following code can be used to plot all landmarks with their corresponding indices and connected into groups:

```r
library(tidyverse)

openface <- 
  read_csv("https://raw.githubusercontent.com/borstell/computer_vision/refs/heads/main/data/openface_landmarks.csv")

openface |> 
  ggplot() +
  geom_path(data = \(x) filter(x, shape == "line"), 
            aes(x, y, group = region)) +
  geom_polygon(data = \(x) filter(x, shape == "polygon"), 
               aes(x, y, group = region), 
               fill = NA, color = "black") +
  geom_point(aes(x, y), size = 3.5) +
  geom_text(aes(x, y, label = landmark), 
            color = "white", 
            vjust = 0.45, 
            size = 1.8, 
            hjust = .5) +
  scale_y_reverse() +
  coord_fixed() +
  theme_void(paper = "white")
```
The code above will generate something like:

![](openface_landmarks.png)
