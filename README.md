# Heat gradient modelling
<p align="center">
<img src="https://drive.google.com/uc?export=view&id=1uscE8REcTzZlb71zcfHQ5r4c9YIu0m0G">
</p>
&emsp;This is a set of MATHCAD models, that allows predicting the behavior of the stochastic heating process during laser treatment.
Multiple models are developed in order to estimate the heat impact, cooling speed and resulting structure. 

## Summary
&emsp;[1. Introduction](#1-introduction)

&emsp;[2. Point heat source](#2-point-heat-source)

&emsp;[3. Gaussian heat source](#3-gaussian-heat-source)

&emsp;[4. Line-segment heat source](#4-line-segment-heat-source)

&emsp;[5. How to use](#5-how-to-use)

## 1. Introduction
&emsp; Concentrated heat sources are widely applied in manufacturing, medicine, space, measurement and other industries.

&emsp; Nowadays we often involve lasers as a particular case of concentrated heat sources. However, any micro-dimensional source of energy may be simulated according to the implied in this project models (and this is often the case in industry for plasma beams, arc current or even gas burners).

&emsp; From the functional point of view, concentrated heat sources are great, because they allow you heating some limited in terms of the spacial volume, keeping away the heat from the rest (you don't usually want to have a brain heatstroke during a laser eye surgery).

&emsp; However, as we apply even a couple of Watts of energy, concentrated in a volume of 50 um3, the physical processes in the nearest region of the source become so difficult, stochastic and non-differentiable, so we are struggling to
simulate the behavior of the material.

&emsp; Fortunately, I am not going to dive so deep inside. I am just going to apply some conduction laws to the cases of different moving heat sources.

&emsp; ***up-date***

&emsp; We made a comparison of the simulated results with the real-world measurements and they are very close. The models are not bullsh*t at all! :)

https://www.sciencedirect.com/science/article/abs/pii/S0890695518300464

### Model schema
The simplified model of laser processing may be represented as follow:

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=1ulH1sSqcYqQZy4bODRFWHeTsRREZU9pR">
</p>

The laser heats and moves, the material melts and becomes hot. Not a big deal in a general case.

As I take into account the conductivity physics and only it, the isotherms on each graph will be cut at the material's melting point (this is the parameter of the model).

## 2. Point heat source
&emsp;This is the simplest case of the concentrated energy source. The energy is distributed uniformly all over the diameter of the source. Thus, the energy density is uniform.

### Physical grounding
&emsp;The temperature distribution equation for this kind of heating source is as follows:

$$T(z,y,t)=\frac{A\cdot P}{2\cdot \pi \cdot \lambda\cdot V\cdot t }\cdot e^{\frac{-(y^{2}+z^{2})}{4\cdot a\cdot t}}$$

In terms of our model, this source is represented as a moving, flat 2D circle on the surface of a semi-infinite body. This circle generates the energy and the semi-infinite body dissipates it.

### What to simulate
- You may simulate the heat impact history in a certain point (which can be moved freely by adjusting the x,y and z coordinates) collected after any amount of laser passes. For example:
this point was centered between 10 laser passes (the fifth crest is the largest, laser passes over the point), the Sum1(t, 0) curve shows the thermal history of this point, the Sum1(t, 5) curve demonstrates how these laser passes influenced at the depth of 5 x *h* (where *h* is another parameter, allowing control the z coordinate of the point).
You can also add singular potential thermal exponents (pink T curve). Compare the green-dotted and the pink curves, the green takes into account previous thermal impacts, and the pink doesn't.
![fields1](https://drive.google.com/uc?export=view&id=1HUC9Gdy5h5k8H4W465_c2W6CDXYzTE9g)

- You may simulate the cooling speed history.
 ![cooling1](https://drive.google.com/uc?export=view&id=1HdkIUc5i_EFy2rv9nm1oPsJ3zu_x0XCU)
Actually, this is the main issue that we usually have with concentrated heat sources. If you cool something at 10<sup>6</sup> °C, you shouldn't await any nice crystallized structure.
These damn atoms (we are consisting of) need some time to form great crystals, if they have not enough, they stay frozen in some un-optimal state. That's why the welding bead breaks, the laser cut brittles the material near the profile and your skin hurts after tattoo removal.


## 3. Gaussian heat source

### Physical grounding

Real-life approximation of the circle heat sources is not bad. Why? Well concentrated heat sources are circular at 90% of time. What do you need elsewhere?
I would like to have a corresponding energy distribution of our beam! For that, the equation of a point heat source should be modified as follows:

$$T(z,y,t)=\frac{A\cdot P}{V\cdot \lambda\ }\cdot \frac{e^{\frac{-z^{2}}{4\cdot a\cdot t}}}{\sqrt{2\cdot \pi \cdot t}}\cdot \frac{e^{\frac{-y^{2}}{4\cdot a\cdot (t_{0}+t)}}}{\sqrt{2\cdot \pi \cdot (t_{0}+t)}}$$

where *t<sub>0</sub>* is a representation of a fictive energy source and it equals to:
$$t_{0}=\frac{r^{2}}{4\cdot a}$$

What happened? We just added an exponential representation of the energy distribution (Gaussian-type).
### What to simulate
- Same story as for the point heat source. Try thermal history:
![fields2](https://drive.google.com/uc?export=view&id=1Hgn1oSKoj0qmVkdvLwQh7zRtTpjbqL1y)
Compare these results to the point model. Similar, but different. This works better. But slower.
- Cooling rates:
  ![cooling2](https://drive.google.com/uc?export=view&id=1HqIsvCvZ4XZgqEjBjvWdUpf68jUSHtE3)
- Additionally, you can simulate the size of the molten pool.

  The x-y isotherms:
  ![size_x](https://drive.google.com/uc?export=view&id=1HbIZa498mHeRVZmT5iOYQq0D_D-oB_sT)
  The x-z isotherms:
  ![size_z](https://drive.google.com/uc?export=view&id=1He9PYrLoc5dvS8583AdkFH4t88BaY_B7)
  The closest to the center isoline represents the size of the molten pool (remember, I have cut the exponents at it, and the melting point is a known property for a material).

## 4. Line-segment heat source

### Physical grounding
&emsp;Line-segment heat source was inspired by thin-wall welding modelling. In the case of thin walls, you should care about the thickness of your sheets and we presume that the heat energy uniformly distributed over this direction.

&emsp;The temperature function for the line-segment heat source is as follow:
$$T(x,z)=\frac{2\cdot A\cdot P}{2\cdot \pi \cdot \lambda\ \cdot \delta }\cdot K0\left [\sqrt{x^{2}+z^{2}}\cdot \sqrt{\frac{2\cdot \alpha}{\lambda \cdot \delta }+\frac{v^{2}}{4\cdot a^{2}}}  \right ]\cdot e^{\frac{-V\cdot x}{2\cdot a}} $$

Here the *K0(n)* is the modified Bessel function of the second kind of the 0-th order.

### What to simulate
- You can visualize your heat source in 3D space, where the height corresponds to the temperature of the static heat source:
![segment](https://drive.google.com/uc?export=view&id=1H_ZG7A70oJC2JeE2gB5lCNKiC4PvUScs)
- Also you can visualize the thermal history at some point. In this case, you do not need the Z coordinate, as our line-segment source isn't changing in this direction.
  ![segment](https://drive.google.com/uc?export=view&id=1HZi_iO21dWSGbLoYxHce3HdXzPSAunbF)

You may ask, why should I apply this model if Gauss works great? Glory to uncle Carl! Just integration of the gauss model is slow. And welding of 2 thin sheets is usually damn fast.

## 5. How to use
&emsp;This is not stand-alone scripts!

&emsp;Please, use MATHCAD v.14+ to execute calculations. Alternatively, you may use MATHCAD Prime of any version, in this case you should convert the provided .xmcd files to the .mcdx native format. The file converter is a build-in plugin of the MATHCAD Prime package.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=1EcatK6k1x1eAOipwHPjGshz9XuQDADj8">
</p>

### Parameters dictionary
{   

*P* - source power, [W]

*V* - source speed, [cm/s]

*D* - single pass length, [cm/s]

*d* - hatch distance, [cm]

*λ* - thermal conductivity, [W/cm*°C]

*a* - thermal diffusivity, [cm2/s]

*c* - thermal capacity, [J/kg*°C]

*N* - amount of single passes, [-]

*Tm* - melting point, [°C]

*A* - material absorptibity, [%]

*x0, y0, z0* - coordinates of the simulated point, [cm]

*Vp* - maximum speed of the source, [cm/s]

*r* - radius of the heating source, [cm]

*Ti* - ambient temperature, [°C]

*h* - layer height, [cm]

}
### Credentials
&emsp;Developed by Alexis D. [LinkedIn](https://www.linkedin.com/in/dmshnkff/)

&emsp;As a part of the thesis project: [theses.fr](http://www.theses.fr/2016LYSEE004)

&emsp;*The author imposes no restrictions to reproduction, modification or copying.*