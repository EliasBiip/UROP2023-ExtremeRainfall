# UROP2023-ExtremeRainfall
The fianl result of the UROP research under the supervison of Dr. Parsun Ray at ICL in Aug. 2023.

This is the result of the UROP team, including me, at ICL. HansonS37 is the original team member that responsible for providing this summary of our codes in his original repository. This repository is a copy of his with a sole purpose of display. 

The original repository is at https://github.com/HansonS37/UROP2023-ExtremeRainfall

# UROP2023-ExtremeRainfall
Contains revised code for "Complex networks reveal global pattern of  extreme-rainfall teleconnections"  


read_data.py  download_TRMM.py   
These two files are used for downloading TRMM precipitation data. 


all_ere_start.ipynb / extreme rainfall calculator.ipynb  
This file calculates the date of extreme rainfall events at all locations. We first calculate the 95 percentile of all wet days, and then delete consecutive days. 


fig1_data.ipynb  fig1.ipynb  
Prepare data for plotting figure 1 and plot figure 1 using cartopy. 

Comparison_ncep2.ipynb  Comparison_ncep2_2.ipynb   
These two files aims to compare the precipitation data from NCEP-reanalysis2 and TRMM. The way to compare is to find the common latitude included in both datasets and extract the data of that common latitude from 50N to 50S. Then, we plot these two sets of data on the same figure to compare them.


Event_sync.py  
This file aims to calculate the value of event synchronization between each two nodes using the ERE_start_date file. We first use calculate the threshold of each pair of extreme event between two nodes, and see how many pairs satisfy the thresholds. This number is the event synchronization value between these two nodes, and we only save the value if the ES value is larger than the 99.5% null model threshold. In this file, we use both Numba and parallel computation to enhance the calculation speed. 


distance_count.py  
We first use "pos" function to find the corresponding lon and lat of each node, and then use "Hav_distance" function to find the great circle distance between two positions. Then, we define several range for these distances and calculate how many pairs are there in each range. Note that instead of saving counting 1 distance between each two points, we actually save n pairs of such distance between two nodes, where n is the value of ES between these two nodes. We will then use this distance distribution to plot figure 2. 


distance.ipynb  
In this file, we calculates the distance between each two pair of these 576000 nodes. Note that the symmetric property can reduce the computational cost a lot. We save the distances in distance_list. 


distanceKDE.ipynb  
In this file, we first use "distance_list" and KernelDensity to calculate the great circle distance under KDE. We save the result in "logprob.npy". We then use the distance distribution computed using distance_count.py to plot the distritbution of links. We can plot the distribution of links and np.exp(logprob) in the same figure to compare them and find the power law fit for links that have short distances. 


fig3a&3b.py  
This file is about how we replot figure 3a and 3b. It shows how we select links and compute link bundles from SCA links we compute before and then plot them on a map. The file first reads all the data and randomly selects some links. Then the file uses scipy package to calculate the kernel density estimation(KDE) and compare the result with null Model computed to deduce link bundles.


link_bundles_null_model.py   
This file is about how we compute null model used in doing significant test and calculating link bundles. The file will use random package to generate links randomly according to total number of links, and then repeat for 600 times to get a randomly decided null model.


4a.ipynb  
We first find the corresponding indices for SCA and EU, and then compute two time series for these two regions. The n th position in each time series is the number of ERE happen in that region on date n. We then compute the lead-lag correlation between these two time series. 


4b_timeseries.ipynb  
In this file, we include two methods to calculate the time series. The first method is given by author, which is very slow but straightforward. The second method computes t21 and t12 with much less computational cost. Then, these time series are filtered and local maximums that are greater than 95 percentile of all JJA data are chosen. 


4b4c_final.ipynb  
We use the time series calculated in 4b_timeseries.ipynb and then find the dates of local maximum. The way to calculate anomalies is that we first compute the average value and subtract the average value from the selected ones. We first calculate the anomalies of precipitation of these local maximum dates and plot these anomalies as fig 4b. Afterwards, we calculate the anomalies of precipitation data of days that are three days later than the local maximum dates and plot these anomalies as fig 4c. 


4d4e_final.ipynb  
We obtain the data of wind speed. We use the same way to calculate anomalies. We first calculate the anomalies of wind speed of local maximum dates and plot them to obtain the Rossby-wave-like pattern in fig 4d. Then, we plot calculate the anomalies of wind speed of days that are three days later than local maximum dates to obtain fig 4e. 

