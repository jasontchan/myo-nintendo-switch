# Neuro-Breakout

Playing Breakout with sEMG and Myo Armband.

![Playing breakout with sEMG](media/Breakout.gif?raw=true "Breakout")

### Usage:
```
pip install pyomyo==0.0.2
python3 neuro_breakout.py
```
Will run a simple model I created using my own data, so it may not work well for you. 

**Myo Hello world**
```
python3 myo_raw.py
```
Uses pygame to plot each of the 8 myo channels, useful for debugging.  

### Gathering new data:
![Generate labels by swinging your hand left to right.](media/Training.gif?raw=true)

You can gather training data by running `` python3 neuro_training.py ``.  
Follow the paddle with your hand and the program will gather training data, for a default of 20 seconds before saving it to ``foo.csv``.  
**Note that sEMG data, the same kind gathered by the Myo is thought to be uniquely identifiable. Do not share this data without careful consideration of the future implications.**  

### Using a more generic model:
```
python3 neuro_testing.py
```
Neuro_testing is a simple program made to test out different simple models. 

### About
Made as a weekend project, it is rough around the edges.  
The sEMG sensor used was a Myo gesture control armband made by Thalmic Labs.   
[The Pygame breakout tutorial I used.](https://www.101computing.net/breakout-tutorial-using-pygame-getting-started/) Thanks 101 computing!    

The code is primarily developed on Linux and should work on Windows and MacOS.  

#### Getting data from the Myo
To communicate with the Myo, I used [pyomyo](https://github.com/PerlinWarp/pyomyo). 

emg_mode.PREPROCESSED (0x01)  
By default myo-raw sends 50Hz data that has been rectified and filtered, using a hidden 0x01 mode.  

emg_mode.FILTERED (0x02)  
Alvipe added the ability to also get filtered non-rectified sEMG (thanks Alvipe).  

emg_mode.RAW (0x03)  
Then I further added the ability to get true raw non-filtered data at 200Hz. This data is unrectified but scales from -128 and 127.  

Sample data and a comparison between data captured in these modes can be found in [MyoEMGPreprocessing.ipynb](Notebooks/MyoModesCompared/MyoEMGPreprocessing.ipynb). Also in this notebook is an explanation of the preprocessing done to the sEMG data and why we do it.  
