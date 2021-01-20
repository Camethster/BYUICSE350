# Data Visualization
 
## ggplot2

###The grammar of graphics

Formatting goes as followsw: 

ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))
  
Mappings include
- aes(x)
- aes(y)
- color
- shape
- size
- alpha (Transparency)

### Specific Color
<GEOM_FUNCTION>(mapping = aes(<MAPPINGS>),color="Specific color")


### Commonn Problems

Your a wimp and need help ?function_name and it will tell you about it.

Every + has some code
otherwise you keep getting +'s

This:
ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))
  
Not This:
ggplot(data = <DATA>)  
  + <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))
  
### Facets

ggplot(data = <DATA>) +
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>)) +
  facuet_wrap(~ some discrete value)
  
ggplot(data = <DATA>) +
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>)) +
  facuet_grid(some discrete value ~ by some other discrete value)


### Geom  Functions

- Smooth
- Point
- Bar

### Transformations
Make sure to overide the default stat.
ggplot(data = <DATA>) +
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>),stat="identity")
  

- stat_count() (Histogram)
- stat(prop) (Proportional)
- stat_summary() (Gives summary statistics)


### Positonal Adjustments

- fill vs color
- X mapping the same as fill or color vs different(stacked bar chart)
- identity (overlapping bar chart)
- dodge (side by side)
- fill (Makes all the charts the same height)
- geom_jitter (different from point. Shows a slight alteration to the data to make it more readable)

### Coordinated Systems

- coord_flip() (Switch x or y axis)
- coord_quickmap() (gives a great ratios)
- coord_polar() (Bar char and Coxcomb chart relations)

