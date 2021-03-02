# Passo a passo de como usar o R para projeções 3D

# Exemplo 1 (https://rdrr.io/cran/plot3D/man/image3D.html)

Vá no RStudio
`
File - > New project -> New Directory -> New Project
`
Coloque qualquer nome no directory name

`
Create project
`

no console escreva

```
install.packages("plot3D")

```

Crie um R script(clica no papal com um + em baixo de file)

Copie esse código nele
```
library(plot3D)

# save plotting parameters
 pm <- par("mfrow")

## =======================================================================
## images in x, y, z plane
## =======================================================================

 par(mfrow = c(2, 2))

# images in x, y, z plane
# We use colkey = list(plot = FALSE) to create room for a color key
 image3D(y = seq(0, 1, 0.1), z = seq(0, 1, 0.1), x = 0.5, 
   col = "blue", xlim = c(0,1), colkey = list(plot = FALSE))
 image3D(x = seq(0, 1, 0.1), z = seq(0, 1, 0.1), y = 0.5, 
   add = TRUE, col = "red", alpha = 0.2)   # alpha makes it transparent
 image3D(x = seq(0, 1, 0.1), y = seq(0, 1, 0.1), z = 0.5, 
   add = TRUE, col = "green")
 colkey(col = c("green", "red", "blue"), clim = c(0.5, 3.5), 
   at = 1:3, labels = c("z", "y", "x"), add = TRUE)
#
 image3D(z = 100, colvar = volcano, zlim = c(0, 150),
   clab = c("height", "m"))
  
#
 image3D( x = 0.5, colvar = volcano, xlim = c(0, 1), 
   ylim = c(0, 1), zlim = c(0, 1))

 image3D( y = 0.5, colvar = volcano, add = TRUE)

#
 image3D( z = 1, colvar = volcano, 
   x = seq(0, 1, length.out = nrow(volcano)),
   y = seq(0, 1, length.out = ncol(volcano)), 
   xlim = c(0, 2), ylim = c(0, 2), zlim = c(0, 2))
 image3D(y = 2, colvar = volcano, add = TRUE, 
    shade = 0.2,
    x = seq(0, 1, length.out = nrow(volcano)),
    z = seq(1, 2, length.out = ncol(volcano)))
 image3D(x = 2, colvar = NULL, col = "orange", add = TRUE, 
    y = seq(0, 1, length.out = nrow(volcano)),
    z = seq(1, 2, length.out = ncol(volcano)))

# reset plotting parameters
 par(mfrow = pm)

```

Salve e aperte em run

Código pronto :D

- [x] ![alt text](https://github.com/LUCASRENAA/Atividade_Faculdade_Readme/blob/main/imgs/1.png?raw=true)

# Exemplo 2 (https://github.com/tylermorganwall/rayshader)

Vá no RStudio
`
File - > New project -> New Directory -> New Project
`
Coloque qualquer nome no directory name

`
Create project
`

no console escreva

```
# To install the latest version from Github:
install.packages("devtools")
devtools::install_github("tylermorganwall/rayshader")
install.packages("raster")
install.packages("rgdal")
```

Crie um R script(clica no papal com um + em baixo de file)

Copie esse código nele

```

library(rayshader)

#Here, I load a map with the raster package.
loadzip = tempfile() 
download.file("https://tylermw.com/data/dem_01.tif.zip", loadzip)
localtif = raster::raster(unzip(loadzip, "dem_01.tif"))
unlink(loadzip)

#And convert it to a matrix:
elmat = raster_to_matrix(localtif)

#We use another one of rayshader's built-in textures:
elmat %>%
  sphere_shade(texture = "desert") %>%
  add_water(detect_water(elmat), color = "desert") %>%
  add_shadow(ray_shade(elmat), 0.5) %>%
  add_shadow(ambient_shade(elmat), 0) %>%
  plot_map()




```

- [x] ![alt text](https://github.com/LUCASRENAA/Atividade_Faculdade_Readme/blob/main/imgs/2.png?raw=true)
