# Simulation of road traffic scenario

Traffic Simulation for the paper "Bayesian dynamic linear model with adaptive parameter estimation for short-term travel speed prediction" Tai-Yu Ma, and Yoann Pigné.



## sumo

We use version 0.26 as it is compatible with the LUST dataset.

Download the archive from sourceforge as the svn Checkout of tag `v0_26_0` fails.


### Compilation on OSX


```bash
export CPPFLAGS="$CPPFLAGS -I/usr/local/include -I/opt/X11/include"
export LDFLAGS="$LDFLAGS -L/usr/local/lib -L/opt/X11/lib"

./configure CXX=clang++ CXXFLAGS="-stdlib=libc++ -std=gnu++11" --with-xerces=/usr/local --with-proj-gdal=/usr/local --with-fox-config=/usr/local/bin/fox-config -with-proj-gdal=/usr/local --with-xerces=/usr/local --prefix=/opt/sumo
make -j8
```


## LUST

We use the Luxembourg SUMO Traffic (LuST) Scenario as a base scenario for mobility scenario. 

```
git clone https://github.com/lcodeca/LuSTScenario.git
```

Then we artificially bloc road segments in order to simulate unpredicted traffic hazards. 



## Detectors map

Output data is generated from a set of detectors materialized in this map :

- https://www.scribblemaps.com/maps/view/Luxembourg_traffic/7tdzwHfuLz

Detectors are configured in the `mydetectors.xml` file in each scenario folder. 

http://sumo.dlr.de/wiki/Simulation/Output/Induction_Loops_Detectors_(E1)

Data are recorded between  7AM (25200s) and  9AM  (32400s)

## Scenarii

There are two scenarii. One with normal traffic. One where an accident occurs at 7.30AM and blocs the road for 30 minutes.

## Output 

Finally, results are presented in files : 

- `scenarios/results/lust.normal-taffic/lust.normal-traffic.out.xlsx`
- `scenarios/results/lust-accident-pt-duchesse/lust.accident-pt-duchesse.out.xlsx`

These table contains lane-by-lane speed time series on each detector defined earlier. This data is used as an input for the estimation method. 

